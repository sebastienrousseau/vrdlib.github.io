---
name: "vrd"
short_name: "vrd"
title: "Performance: published timings per backend | vrd"
description: "Measured vrd timings for u32 and u64 draws per backend, the Ziggurat normal, SIMD byte fills, split and quasi-random points, the machine they were measured on, and how to reproduce them."
keywords: "vrd benchmark, Rust rng performance, Xoshiro256++ speed, PCG speed, SIMD fill_bytes"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Performance"
headline: "How long each operation takes"
lead: "Published measurements from the vrd repository, with the machine and release they came from."
nav_docs: "true"
---
## How fast is each backend?

These are the figures in the repository's
[doc/BENCHMARKS.md](https://github.com/sebastienrousseau/vrd/blob/main/doc/BENCHMARKS.md),
recorded on 28 May 2026 for vrd 0.0.12 with
`cargo bench --features simd,pcg,quasirandom --bench benchmark`: the Criterion
median, through the `Random` type, lower is better.

| Operation | Backend or path | Time |
| :--- | :--- | ---: |
| `rand()` (`u32`) | Xoshiro256++ | 3.09 ns |
| | MT19937 | 3.12 ns |
| | PCG32 | 2.72 ns |
| | PCG64 | 4.26 ns |
| `u64()` | Xoshiro256++ | 3.10 ns |
| | MT19937 | 4.68 ns |
| | PCG32 | 3.72 ns |
| | PCG64 | 4.21 ns |
| `normal(0, 1)` | Ziggurat | 3.71 ns |
| `try_fill_bytes`, 1 KiB | scalar | 138 ns |
| | `simd` | 63.3 ns |
| `try_fill_bytes`, 16 KiB | scalar | 2,188 ns |
| | `simd` | 736 ns |
| `split()` | Xoshiro256++ | 326 ns |
| Halton point, 2 dimensions | | 20.7 ns |
| Sobol point, 2 dimensions | | 1.07 ns |

## What machine was that?

The repository records an Apple Silicon (M-series) machine running macOS 25.5
with stable Rust, in the release profile (`opt-level = 3`, `lto = true`,
`codegen-units = 1`). It does not name the exact chip. Numbers on another
machine will differ; compare runs made on the same one.

## What about statistical quality?

The repository has a harness that pipes each backend's output into the
PractRand test suite (`cargo run --release --example crush --features crush`),
but no results are recorded yet, and CI does not run it. Xoshiro256++,
MT19937, PCG and ChaCha20 are published algorithms; vrd has not published its
own test results for them.

## How do I reproduce them?

From a clone of the repository:

```bash
cargo bench --features simd,pcg,quasirandom --bench benchmark
```

The same suite also times `fastrand` and `rand::rng()` on the same machine.
