---
name: "vrd"
short_name: "vrd"
title: "API guide: methods, backends and Cargo features | vrd"
description: "A guide to vrd's API: constructors, the methods on Random grouped by job, the backends and their state sizes, every Cargo feature, and where the full reference lives."
keywords: "vrd api, vrd Random methods, vrd cargo features, vrd backends"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "API guide"
headline: "How the vrd API fits together"
lead: "The constructors, methods and features you choose between, with the full reference on docs.rs."
nav_docs: "true"
---
## Constructors

| Constructor | Backend | Seed |
| :--- | :--- | :--- |
| `Random::new()` | Xoshiro256++ | The operating system |
| `Random::from_u64_seed(u64)` | Xoshiro256++ | Yours |
| `Random::from_seed([u8; 32])` | Xoshiro256++ | Yours |
| `Random::new_mersenne_twister()` | MT19937 | The operating system |
| `Random::new_mersenne_twister_with_seed(u32)` | MT19937 | Yours |
| `Random::new_pcg32()`, `new_pcg64()` | PCG (`pcg` feature) | The operating system |
| `Random::new_pcg32_with_seed(..)`, `new_pcg64_with_seed(..)` | PCG (`pcg` feature) | Yours |
| `Random::new_secure()` | ChaCha20 (`crypto` feature) | The operating system |
| `Random::from_secure_seed([u8; 32])` | ChaCha20 (`crypto` feature) | Yours |

## Methods by job

| Job | Methods |
| :--- | :--- |
| Raw values | `rand` (`u32`), `u64`, `i64`, `bool(p)`, `char` |
| Ranges, unbiased | `int(low, high)`, `uint(low, high)`, `random_range`, `bounded`, `range` |
| Floats | `float` (`f32`, 24 bits), `double` and `f64` (`f64`, 53 bits), `uniform(low, high)` |
| Distributions | `normal`, `exponential`, `poisson`, and the `Distribution<T>` trait |
| Slices | `choose`, `shuffle`, `sample`, `sample_with_replacement`, `rand_slice` |
| Bytes and text | `bytes`, `string`, `fill_array`, `iter_u32`, `iter_u64`, `iter_bytes` |
| Identifiers | `uuid_v4_bytes`, `uuid_v4`, `hex_token`, `base64_token` |
| Streams | `split` (Xoshiro256++ only), `backend` |

Methods that return a `Vec` or a `String` need the `alloc` feature.

## Cargo features

| Feature | Default | What it adds |
| :--- | :---: | :--- |
| `std` | yes | Seeding from the operating system; `std::error::Error` for the error types |
| `alloc` | through `std` | `bytes`, `string`, `sample`, `shuffle`, `uuid_v4`, the tokens and the Mersenne Twister |
| `serde` | no | `Serialize` and `Deserialize` for the public types, including the generator state |
| `simd` | no | Byte fills on AArch64 NEON and x86-64 AVX2, with a different byte stream from the scalar path |
| `pcg` | no | The PCG32 and PCG64 backends |
| `crypto` | no | The ChaCha20 backend: `new_secure` and `from_secure_seed` |
| `quasirandom` | no | Halton, Sobol and Van der Corput sequences |
| `crush` | no | An example that pipes output into the PractRand test suite |

## Errors and panics

Bounded sampling panics when `low >= high`, and the distributions panic on
non-finite parameters, with messages that name the parameter; both are
programming errors. `Random::new()` can panic if the operating system has no
entropy to give. The other constructors do not fail.

## Threads

A `Random` holds mutable state: use one per thread, each with its own seed,
or derive streams with `split()` on the default backend.

## Where is the full reference?

Every public item is documented, which the crate enforces with
`#![deny(missing_docs)]`. The rendered reference is on
[docs.rs/vrd](https://docs.rs/vrd), and the repository's
[doc/](https://github.com/sebastienrousseau/vrd/tree/main/doc) folder has the
user guide, architecture and policies.
