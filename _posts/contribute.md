---
name: "vrd"
short_name: "vrd"
title: "Contributing to vrd | vrd"
description: "How to contribute to vrd: the four checks every pull request passes, test coverage, signed commits, commit conventions and how contributions are licensed."
keywords: "contribute to vrd, vrd pull request, vrd contributing guide"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Contributing"
headline: "Contributing to vrd"
lead: "A summary of the project's contributing guide; the guide in the repository is the reference."
---
## What every pull request passes

```bash
cargo fmt --check
cargo clippy --all-targets --all-features -- -D warnings
cargo test
cargo build --no-default-features
```

The contributing guide also recommends `cargo audit`,
`cargo run --example all` to run every example, and the Cortex-M check
`cargo check --target thumbv7em-none-eabihf --no-default-features`.

- New behaviour comes with new tests in the same pull request, and every
  file stays at or above 98% region coverage (`cargo llvm-cov`).
- A new dependency needs a reason in the pull request.
- The pull request body has `## Summary` and `## Test Plan` sections, and the
  title stays under 70 characters.

## Signed commits and conventions

Sign every commit (`git commit -S`). Commit messages follow
[Conventional Commits](https://www.conventionalcommits.org/), with `!` for a
breaking change, and each commit holds one logical change. Report a bug as an
[issue](https://github.com/sebastienrousseau/vrd/issues) with a few lines
that reproduce it, the expected and actual output, and your Rust version.
Security problems go through the private channel on the
[security page](/security/). The full guide is
[CONTRIBUTING.md](https://github.com/sebastienrousseau/vrd/blob/main/CONTRIBUTING.md).

## Licence of contributions

By contributing you agree that your work is dual-licensed under Apache-2.0 or
MIT, matching the crate.

## Improving this website

The source of vrdlib.com is in the
[vrdlib.github.io repository](https://github.com/sebastienrousseau/vrdlib.github.io).
Report a mistake on the site there, or through the [contact page](/contact/).
