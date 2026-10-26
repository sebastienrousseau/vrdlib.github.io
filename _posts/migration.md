---
name: "vrd"
short_name: "vrd"
title: "Migrate to vrd from rand, fastrand or an older vrd | vrd"
description: "How to move from the rand crate or an older vrd release to vrd 0.0.12: the matching calls, the rand traits vrd implements, and the changes that alter output for the same seed."
keywords: "vrd migration, rand to vrd, fastrand to vrd, vrd 0.0.6 upgrade"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "Migration"
headline: "Moving to vrd, or to a newer vrd"
lead: "The calls that change when you switch from rand, and what changed in vrd since the old site was written."
nav_migration: "true"
---
## From rand 0.10

| rand 0.10 | vrd |
| :--- | :--- |
| `let mut rng = rand::rng();` | `let mut rng = Random::new();` |
| `rng.random::<u32>()` | `rng.rand()` |
| `rng.random_range(0..n)` | `rng.uint(0, n - 1)` |
| `rng.fill_bytes(&mut buf)` | `rng.try_fill_bytes(&mut buf).unwrap()` |
| `slice.choose(&mut rng)` | `rng.choose(slice)` |
| `slice.shuffle(&mut rng)` | `rng.shuffle(slice)` |
| `StdRng::seed_from_u64(s)` | `Random::from_u64_seed(s)` |
| `ChaCha20Rng::from_seed(s)` | `Random::from_secure_seed(s)` (`crypto`) |
| `ChaCha20Rng::from_os_rng()` | `Random::new_secure()` (`crypto`) |

You do not have to change every call at once: `Random` implements rand's
`TryRng` and `SeedableRng`, so it can be passed to code that takes those
traits. `try_fill_bytes` needs rand's `TryRng` trait in scope. `uint` takes
an inclusive upper bound, hence `n - 1`.

## From an older vrd

The site you may have read before described vrd 0.0.6, built around the
Mersenne Twister. Versions 0.0.10 and 0.0.11 changed that:

- `Random::new()` is Xoshiro256++, not the Mersenne Twister. Use
  `Random::new_mersenne_twister()` to keep MT19937.
- `int`, `uint` and `random_range` are unbiased, so they return different
  values for the same seed than before 0.0.10.
- `normal()` uses the Ziggurat method since 0.0.11, which also changes its
  output for a seed.
- The generic `fill()` method is gone: use `try_fill_bytes` from rand's
  `TryRng`, or build values from `rand()` and `u64()`.
- The `logging` feature and the serde_json, YAML and TOML helpers are gone;
  use `serde` directly with the `serde` feature.
- `Random` no longer derives `Eq`, `Hash`, `Ord` or `PartialOrd`.

The [CHANGELOG](https://github.com/sebastienrousseau/vrd/blob/main/CHANGELOG.md)
lists every change, release by release.
