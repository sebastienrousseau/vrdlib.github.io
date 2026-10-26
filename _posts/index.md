---
name: "vrd"
short_name: "vrd"
title: "vrd: a small, no_std random number generator for Rust"
description: "vrd is a random number generator library for Rust: Xoshiro256++ by default, with optional Mersenne Twister, PCG, ChaCha20 and quasi-random backends, unbiased ranges, four distributions, and builds for std, no_std and WebAssembly."
keywords: "vrd, Rust random number generator, Xoshiro256++, Mersenne Twister, PCG, ChaCha20, no_std RNG, quasi-random, Sobol, Halton"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "index"
language: "en-GB"
schema: "page"
changefreq: "weekly"
eyebrow: "Open-source Rust library"
headline: "Random numbers for Rust, from microcontrollers to Monte Carlo"
lead: "vrd generates random numbers with Xoshiro256++ by default, and adds Mersenne Twister, PCG, ChaCha20 and quasi-random sequences when you need them."
---
## What is vrd?

vrd is a free, open-source random number generator library for Rust. Its
`Random` type gives you integers in a range, floats, booleans, choices from a
slice, shuffles, tokens and samples from four distributions. The default
generator is Xoshiro256++, seeded from the operating system; Cargo features
add a Mersenne Twister, PCG32 and PCG64, a ChaCha20 generator for secrets,
SIMD byte fills and quasi-random sequences. It is dual-licensed under
Apache-2.0 or MIT.

## Can I use it for passwords and tokens?

Only with the `crypto` feature and `Random::new_secure()`. The default
generator, like the Mersenne Twister and PCG backends, is not
cryptographically secure: anyone who sees enough of its output can predict
the rest. The [security page](/security/) explains where the line is.

## Does it need the standard library?

No. With default features off, the core builds without the standard library
or an allocator, and CI checks it for a Cortex-M target and for WebAssembly.
The [features page](/features/#no-std-embedded-and-webassembly) shows how.

## Who makes it?

vrd is written by [Sebastien Rousseau](https://sebastienrousseau.com/) and
its contributors. The source, the issue tracker and every release are on
[GitHub](https://github.com/sebastienrousseau/vrd); the crate is on
[crates.io](https://crates.io/crates/vrd). Read more on the
[about page](/about/).
