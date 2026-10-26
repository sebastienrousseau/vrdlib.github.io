---
name: "vrd"
short_name: "vrd"
title: "Features: backends, distributions, reproducible and quasi-random sequences | vrd"
description: "What vrd does: Xoshiro256++ by default, Mersenne Twister, PCG and ChaCha20 backends, unbiased ranges, four distributions, reproducible sequences, tokens, quasi-random sequences, SIMD byte fills, no_std and WebAssembly."
keywords: "vrd features, Xoshiro256++ Rust, Mersenne Twister Rust, PCG Rust, ChaCha20 Rust, Sobol sequence Rust, no_std rng"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Features"
headline: "What vrd does, and where it stops"
lead: "Each section says what the feature is, which Cargo feature turns it on and what it does not do."
nav_features: "true"
---
## Xoshiro256++ by default

**`Random::new()` creates a Xoshiro256++ generator seeded from the operating
system.** Its state is 32 bytes and its period is 2<sup>256</sup> - 1; seeds
go through SplitMix64 first, so even a poor seed gives a well-mixed state.

```rust
use vrd::Random;

let mut rng = Random::new();
let n: u32 = rng.rand();      // any u32
let die = rng.int(1, 6);      // i32 in [1, 6]
let x = rng.double();         // f64 in [0.0, 1.0)
let coin = rng.bool(0.5);     // true half the time
```

Ranges are unbiased: `int`, `uint`, `random_range` and `bounded` use Lemire's
nearly-divisionless method rather than a plain remainder. `float` fills all 24
bits of an `f32` mantissa and `double` all 53 bits of an `f64`.

## Choosing a backend

**Every backend sits behind the same `Random` type.** Pick one with its
constructor:

| Backend | Constructor | State | Cargo feature | Suitable for secrets |
| :--- | :--- | ---: | :--- | :---: |
| Xoshiro256++ | `Random::new()` | 32 B | default | no |
| Mersenne Twister (MT19937) | `Random::new_mersenne_twister()` | 2,488 B | `alloc` | no |
| PCG32 | `Random::new_pcg32()` | 16 B | `pcg` | no |
| PCG64 | `Random::new_pcg64()` | 32 B | `pcg` | no |
| ChaCha20 | `Random::new_secure()` | heap-allocated | `crypto` | yes |

The Mersenne Twister is there to reproduce existing MT19937 output, such as
reference data from older tools; use it when you need its exact sequence.
The ChaCha20 backend wraps `rand_chacha`, the rand project's implementation,
rather than a cipher written for vrd.

## Distributions

**Four distributions are built in**: `uniform(low, high)`, `normal(mean,
std_dev)`, `exponential(rate)` and `poisson(mean)`. `normal` uses the
Ziggurat method. The `Distribution<T>` trait lets you add your own:

```rust
use vrd::{Distribution, Random};

struct Bernoulli { p: f64 }

impl Distribution<bool> for Bernoulli {
    fn sample(&self, rng: &mut Random) -> bool {
        rng.double() < self.p
    }
}

let mut rng = Random::from_u64_seed(1);
let heads = Bernoulli { p: 0.5 }.sample(&mut rng);
```

The distributions panic on invalid parameters, such as a non-finite mean,
with a message naming the parameter. For gamma, binomial, log-normal and the
rest, use `rand_distr`.

## Reproducible sequences

**The same seed gives the same sequence.** `Random::from_u64_seed(u64)` and
`Random::from_seed([u8; 32])` are deterministic and allocate nothing:

```rust
use vrd::Random;

let mut a = Random::from_u64_seed(0xCAFE_BABE);
let mut b = Random::from_u64_seed(0xCAFE_BABE);
assert_eq!(a.rand(), b.rand()); // 2783027749 both times with vrd 0.0.12
```

With the `serde` feature, a generator serialises and restores with its full
state, so a run can resume where it stopped. For parallel work,
`Random::split()` returns a second Xoshiro256++ stream 2<sup>128</sup> draws
ahead of the first; on the other backends it returns `None`, so give each
worker its own seed instead.

## Slices, tokens and identifiers

**Common jobs are methods on `Random`**: `choose`, `shuffle`, `sample` and
`sample_with_replacement` on slices; `bytes`, `string`, `fill_array` and
iterators over `u32`, `u64` and bytes; and identifiers:

| Method | Returns |
| :--- | :--- |
| `uuid_v4_bytes()` | A version 4 UUID as `[u8; 16]`, with no allocation |
| `uuid_v4()` | The same UUID as a hyphenated string |
| `hex_token(n)` | `n` random bytes as `2n` lowercase hex characters |
| `base64_token(n)` | `n` random bytes as URL-safe base64 without padding |

These come from whichever backend the `Random` uses. For a session token or
an API key, call them on `Random::new_secure()`.

## Quasi-random sequences

**The `quasirandom` feature adds low-discrepancy sequences** for Monte Carlo
integration and sampling, which cover a space more evenly than random points:

```rust
use vrd::quasirandom::{HaltonSequence, SobolSequence, VanDerCorputSequence};

let mut vdc = VanDerCorputSequence::new(2);  // 0.5, 0.25, 0.75, ...
let mut halton = HaltonSequence::new(2);     // up to 32 dimensions
let mut sobol = SobolSequence::new(6);       // up to 6 dimensions

let x = vdc.next_point();
let p = halton.next_point::<2>();
let q = sobol.next_point::<6>();
```

Sobol stops at six dimensions: going further needs direction numbers vrd
does not ship yet.

## SIMD byte fills

**The `simd` feature fills byte buffers several streams at a time**: two
Xoshiro256++ states on AArch64 NEON, four on x86-64 AVX2. In the published
benchmarks it was 2.18 times faster than the scalar path for 1 KiB and 2.97
times for 16 KiB. Its output for a seed differs from the scalar path's, so
keep it off where you need a reproducible byte stream.

## no_std, embedded and WebAssembly

**With default features off, vrd needs neither the standard library nor an
allocator:**

```toml
[dependencies]
vrd = { version = "0.0.12", default-features = false }
```

Seed it yourself with `Random::from_seed` or `Random::from_u64_seed`, since
there is no operating system to ask. The `alloc` feature adds the methods
that return a `Vec` or `String` and the Mersenne Twister. CI checks both
builds for `thumbv7em-none-eabihf` (Cortex-M4F and M7F) and
`wasm32-unknown-unknown`. In WebAssembly, seed manually or enable entropy
through `getrandom` in your own crate.

## Works with rand

**`Random` and each backend implement rand 0.10's `TryRng` and
`SeedableRng` traits**, and so `Rng`, so you can pass a vrd generator to code
written for the rand traits. The [migration guide](/migration/) maps rand's
calls to vrd's.

## Command-line tool

**`cargo install vrd` installs a small `vrd` command** that prints random
`u32` values, one per line:

```bash
vrd            # one number
vrd 16         # sixteen numbers
vrd 8 0xCAFE   # eight numbers from the seed 0xCAFE
```
