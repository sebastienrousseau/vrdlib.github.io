---
name: "vrd"
short_name: "vrd"
title: "Frequently asked questions about vrd | vrd"
description: "Answers about vrd: what it is, cryptographic security, the Mersenne Twister, the Rust version, reproducible runs, threads, no_std, output stability, versions and the licence."
keywords: "vrd faq, is vrd secure, vrd mersenne twister, vrd msrv, vrd no_std"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "FAQ"
headline: "Frequently asked questions"
lead: "Short answers first; each links to the page with the detail where there is one."
nav_faqs: "true"
---
## What is vrd?

vrd is a free, open-source random number generator library for Rust. It uses Xoshiro256++ by default and adds Mersenne Twister, PCG, ChaCha20 and quasi-random sequences behind Cargo features. See the [features](/features/).

## Is vrd cryptographically secure?

Only with the `crypto` feature and `Random::new_secure()`, which uses ChaCha20. The default Xoshiro256++ generator, the Mersenne Twister and PCG are predictable and must not be used for secrets. See the [security page](/security/).

## Does vrd still use the Mersenne Twister?

Not by default. Since 0.0.10, `Random::new()` uses Xoshiro256++. The Mersenne Twister is still available through `Random::new_mersenne_twister()` for code that needs MT19937's exact output. See the [migration guide](/migration/).

## Which Rust version do I need?

Rust 1.85 or newer. vrd's manifest says 1.70, but the rand 0.10 crate it depends on needs 1.85.

## Can I get the same numbers on every run?

Yes. Seed the generator with `Random::from_u64_seed` or `Random::from_seed` and it produces the same sequence every time. See [reproducible sequences](/features/#reproducible-sequences).

## Can I share one generator between threads?

No. A Random holds mutable state. Use one per thread, each with its own seed, or `split()` streams from the default backend.

## Does it work without the standard library?

Yes. With default features off, the core builds without std or an allocator; CI checks it for a Cortex-M target and for WebAssembly. Seed it yourself there.

## Is the output stable between versions?

The project aims to keep the output for a seed the same between patch releases and lists any change by method in the CHANGELOG. Releases 0.0.10 and 0.0.11 changed the output of int, uint, random_range and normal.

## Why is crates.io at 0.0.12 when the repository says 0.0.14?

Versions 0.0.13 and 0.0.14 updated dependencies only and were tagged on GitHub but not published to crates.io. 0.0.12 has the same API.

## What does it cost, and under which licence?

Nothing. vrd is free software under the Apache License 2.0 or the MIT licence, at your option.

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is vrd?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "vrd is a free, open-source random number generator library for Rust. It uses Xoshiro256++ by default and adds Mersenne Twister, PCG, ChaCha20 and quasi-random sequences behind Cargo features."
      }
    },
    {
      "@type": "Question",
      "name": "Is vrd cryptographically secure?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Only with the crypto feature and Random::new_secure(), which uses ChaCha20. The default Xoshiro256++ generator, the Mersenne Twister and PCG are predictable and must not be used for secrets."
      }
    },
    {
      "@type": "Question",
      "name": "Does vrd still use the Mersenne Twister?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Not by default. Since 0.0.10, Random::new() uses Xoshiro256++. The Mersenne Twister is still available through Random::new_mersenne_twister() for code that needs MT19937's exact output."
      }
    },
    {
      "@type": "Question",
      "name": "Which Rust version do I need?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Rust 1.85 or newer. vrd's manifest says 1.70, but the rand 0.10 crate it depends on needs 1.85."
      }
    },
    {
      "@type": "Question",
      "name": "Can I get the same numbers on every run?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. Seed the generator with Random::from_u64_seed or Random::from_seed and it produces the same sequence every time."
      }
    },
    {
      "@type": "Question",
      "name": "Can I share one generator between threads?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "No. A Random holds mutable state. Use one per thread, each with its own seed, or split() streams from the default backend."
      }
    },
    {
      "@type": "Question",
      "name": "Does it work without the standard library?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. With default features off, the core builds without std or an allocator; CI checks it for a Cortex-M target and for WebAssembly. Seed it yourself there."
      }
    },
    {
      "@type": "Question",
      "name": "Is the output stable between versions?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "The project aims to keep the output for a seed the same between patch releases and lists any change by method in the CHANGELOG. Releases 0.0.10 and 0.0.11 changed the output of int, uint, random_range and normal."
      }
    },
    {
      "@type": "Question",
      "name": "Why is crates.io at 0.0.12 when the repository says 0.0.14?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Versions 0.0.13 and 0.0.14 updated dependencies only and were tagged on GitHub but not published to crates.io. 0.0.12 has the same API."
      }
    },
    {
      "@type": "Question",
      "name": "What does it cost, and under which licence?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Nothing. vrd is free software under the Apache License 2.0 or the MIT licence, at your option."
      }
    }
  ]
}
</script>
