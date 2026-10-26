---
name: "vrd"
short_name: "vrd"
title: "Changelog: vrd releases up to 0.0.14 | vrd"
description: "What changed in vrd's recent releases, from the Xoshiro256++ rewrite in 0.0.10 to 0.0.14, with links to the full changelog."
keywords: "vrd changelog, vrd releases, vrd 0.0.12, vrd 0.0.11, vrd 0.0.10"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Changelog"
headline: "vrd releases up to 26 October 2026"
lead: "The recent releases, summarised from the project's CHANGELOG.md, dated by crates.io and GitHub."
---
## 0.0.14, 11 October 2026 (GitHub only)

- Dependency update: `rand` 0.10.3. Not published to crates.io.

## 0.0.13 (not released)

- Security updates to the transitive dependencies `anyhow` and
  `crossbeam-epoch`. Recorded in the CHANGELOG; there is no tag or
  crates.io release.

## 0.0.12, 28 May 2026

- No API changes. Every public item is documented, enforced with
  `#![deny(missing_docs)]`, and private items carry doc comments too.
- Six fuzz targets, packaging templates, and long-form documentation in
  `doc/`: architecture, testing, policies, user guide and migration guides.

## 0.0.11, 28 May 2026

- New backends and features: PCG32 and PCG64 (`pcg`), ChaCha20 (`crypto`),
  Halton, Sobol and Van der Corput sequences (`quasirandom`), SIMD byte fills
  (`simd`), the `Distribution<T>` trait, `Random::split()` and
  `Random::fill_array`.
- `normal()` uses the Ziggurat method, about four times faster, and its
  output changes for a given seed.
- `Random` no longer derives `Eq`, `Hash`, `Ord` or `PartialOrd`.

## 0.0.10, 29 April 2026

- Xoshiro256++ becomes the default generator.
- `no_std` without an allocator, checked in CI on Cortex-M and WebAssembly.
- rand 0.10's traits, unbiased ranges, 24-bit and 53-bit floats, UUIDs,
  hex and base64 tokens, and iterator adapters.
- The `logging` feature and the serialisation helpers are removed.

## Where is the full history?

Every change is in
[CHANGELOG.md](https://github.com/sebastienrousseau/vrd/blob/main/CHANGELOG.md),
and the releases are on
[GitHub](https://github.com/sebastienrousseau/vrd/releases) and
[crates.io](https://crates.io/crates/vrd/versions).
