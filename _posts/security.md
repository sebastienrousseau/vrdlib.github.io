---
name: "vrd"
short_name: "vrd"
title: "Security: reporting, which backend to trust, and what vrd promises | vrd"
description: "How to report a vulnerability in vrd, why the default generator must not be used for secrets, when to use the ChaCha20 backend, where unsafe code is allowed, and what vrd does not guarantee."
keywords: "vrd security, secure random Rust, ChaCha20 vrd, predictable rng, vrd vulnerability report"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Security"
headline: "Which generator to trust with what"
lead: "vrd is fast by default and secure only when you ask. This page says where the line is."
nav_security: "true"
---
## How do I report a vulnerability?

Privately, by the email address in vrd's
[security policy](https://github.com/sebastienrousseau/vrd/security/policy),
with the subject `vrd security:`, or through
[GitHub's advisory form](https://github.com/sebastienrousseau/vrd/security/advisories/new).
Please do not open a public issue. The policy aims to acknowledge a report
within 72 hours and to give a timeline for a fix within a week. If a
published version is affected, it is yanked from crates.io and a fixed
release follows within 7 days.

## Which generator can I use for secrets?

Only ChaCha20, from the `crypto` feature:

```rust
use vrd::Random;

let mut rng = Random::new_secure();     // ChaCha20, seeded by the OS
let token = rng.base64_token(32);       // 256 bits
```

Xoshiro256++, the Mersenne Twister, PCG32 and PCG64 are deterministic
functions of their seed: anyone who sees enough of their output can predict
what comes next. Do not use them for session tokens, API keys, password-reset
links, CSRF tokens, nonces or initialisation vectors. vrd's ChaCha20 backend
wraps `rand_chacha` from the rand project rather than implementing the cipher
itself.

## What does vrd not promise?

- **Constant-time execution.** The backends are not designed to resist
  timing side channels, and vrd's code paths have not been audited for it.
- **Cryptographic security on any backend but ChaCha20.**
- **A third-party audit.** vrd has not had one.

## Where is unsafe code allowed?

The crate denies `unsafe` code. The one module allowed to use it is
`xoshiro_simd`, for the NEON and AVX2 intrinsics behind the `simd` feature,
with a `SAFETY:` comment on each block.

## What is checked?

- Fuzzing: six cargo-fuzz targets cover seeding each backend, array fills,
  bounded ranges and quasi-random sequences. They run locally
  (`make fuzz-quick`), not in CI.
- CI builds the `no_std` core for Cortex-M and WebAssembly, tests the optional
  features on Linux and the SIMD path on Linux and macOS, and runs
  `cargo audit`.
- `cargo deny` checks licences and advisories (`make deny`).

## How do I check what I downloaded?

Cargo records the SHA-256 of every crate it downloads in `Cargo.lock` and
checks it against the registry. To compare by hand:

```bash
curl -s https://crates.io/api/v1/crates/vrd/0.0.12 | jq -r '.version.checksum'
```

vrd releases are not signed yet; the repository's
[pkg/VERIFY.md](https://github.com/sebastienrousseau/vrd/blob/main/pkg/VERIFY.md)
describes the signing it plans.
