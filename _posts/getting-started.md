---
name: "vrd"
short_name: "vrd"
title: "Getting started with vrd: add the crate and draw a first number | vrd"
description: "Add vrd to a Rust project, draw integers, floats and choices, seed it for a reproducible sequence, pick a backend, and build it for no_std."
keywords: "vrd getting started, cargo add vrd, Rust random number example, seeded rng Rust"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Getting started"
headline: "Your first random numbers"
lead: "From an empty Rust project to seeded, reproducible random numbers in one file."
nav_docs: "true"
---
## What do I need?

Rust 1.85 or newer. vrd's manifest declares 1.70, but the `rand` 0.10 crate
it depends on needs 1.85: on Rust 1.80 the build stops while reading
`rand_core`'s manifest, and on 1.85 it succeeds.

## How do I add it?

```bash
cargo add vrd
```

or in `Cargo.toml`:

```toml
[dependencies]
vrd = "0.0.12"
```

0.0.12 is the latest release on crates.io. The default feature is `std`,
which turns on `alloc`.

## How do I draw numbers?

```rust
use vrd::Random;

fn main() {
    let mut rng = Random::new();           // Xoshiro256++, seeded by the OS

    println!("u32:        {}", rng.rand());
    println!("u64:        {}", rng.u64());
    println!("[1, 100]:   {}", rng.int(1, 100));
    println!("[0.0, 1.0): {}", rng.float());
    println!("choice:     {:?}", rng.choose(&[10, 20, 30]));
}
```

`Random::new()` asks the operating system for a seed and may panic if none is
available; `Random::from_seed` never does.

## How do I get the same numbers every run?

Seed the generator yourself:

```rust
use vrd::Random;

let mut rng = Random::from_u64_seed(0xCAFE_BABE);
let first = rng.rand(); // 2783027749 with vrd 0.0.12
```

`Random::from_seed([u8; 32])` takes a 32-byte seed instead. Neither
allocates.

## How do I use another backend?

Call its constructor; the methods stay the same.

```rust
use vrd::Random;

let mut mt = Random::new_mersenne_twister(); // MT19937
let mut pcg = Random::new_pcg32();           // needs the pcg feature
let mut secure = Random::new_secure();       // ChaCha20, needs the crypto feature
let token = secure.base64_token(32);
```

```toml
[dependencies]
vrd = { version = "0.0.12", features = ["pcg", "crypto"] }
```

## How do I build for an embedded target?

Turn off the default features and seed manually:

```toml
[dependencies]
vrd = { version = "0.0.12", default-features = false }
```

```rust
use vrd::Random;

let mut rng = Random::from_seed([0x42u8; 32]);
let n = rng.rand();
```

## Where next?

- The [API guide](/documentation/) for every method and Cargo feature.
- The [migration guide](/migration/) if you are coming from `rand`,
  `fastrand` or an older vrd.
- The full API reference on [docs.rs](https://docs.rs/vrd).
