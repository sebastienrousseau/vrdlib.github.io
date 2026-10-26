---
name: "vrd"
short_name: "vrd"
title: "About vrd and its author, Sebastien Rousseau | vrd"
description: "Who builds vrd, and the facts about the project: its crate, licence, Rust version, latest release, versioning policy and where its source and security policy live."
keywords: "vrd author, sebastien rousseau, vrd licence, vrd versions"
author: "Sebastien Rousseau"
date: "2026-10-26"
news_publication_date: "2026-10-26"
layout: "page"
language: "en-GB"
schema: "page"
changefreq: "monthly"
eyebrow: "About"
headline: "About vrd"
lead: "vrd is an open-source project by Sebastien Rousseau and its contributors."
---
## Who builds vrd?

vrd is written by [Sebastien Rousseau](https://sebastienrousseau.com/) and
its contributors, credited as "The vrd Contributors". He is on
[GitHub](https://github.com/sebastienrousseau) as sebastienrousseau. Version
0.0.1 was published on crates.io in February 2023, and version 0.0.10 in
April 2026 replaced the Mersenne Twister default with Xoshiro256++.

## Project facts

| | |
| :--- | :--- |
| **Crate** | `vrd` on crates.io, with a small `vrd` command |
| **Language** | Rust, 2021 edition |
| **Rust version** | 1.85 or newer in practice; the manifest declares 1.70 |
| **Licence** | Apache-2.0 or MIT, at your option |
| **Latest release on crates.io** | [0.0.12](https://crates.io/crates/vrd/0.0.12), 28 May 2026 |
| **Latest tag** | [v0.0.14](https://github.com/sebastienrousseau/vrd/releases/tag/v0.0.14), 11 October 2026, dependency updates only |
| **Source** | [github.com/sebastienrousseau/vrd](https://github.com/sebastienrousseau/vrd) |
| **API reference** | [docs.rs/vrd](https://docs.rs/vrd) |
| **Security policy** | [SECURITY.md](https://github.com/sebastienrousseau/vrd/security/policy) |

## How is it versioned?

vrd is pre-1.0 and follows Semantic Versioning. Its
[policies](https://github.com/sebastienrousseau/vrd/blob/main/doc/POLICIES.md)
aim to keep the output for a given seed the same between patch releases and to
name any method whose output changes in the CHANGELOG. While the version is
0.0.x, read every release's notes before upgrading: 0.0.10 and 0.0.11 both
changed outputs.
