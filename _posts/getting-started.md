---

# Front Matter (YAML)

author: "The Random (VRD) Team"
banner_alt: "MacBook Pro on white surface"
banner_height: "100vh"
banner_width: "100vw"
banner: "https://kura.pro/stock/images/banners/tianyi-ma-WiONHd_zYI4.webp"
cdn: "https://kura.pro"
changefreq: "weekly"
charset: "utf-8"
cname: ""
copyright: "© 2024 Random (VRD). All rights reserved."
date: "Mar 10, 2024"
description: "Step-by-step guide on setting up Random (VRD) in Rust for high-quality random numbers using the Mersenne Twister algorithm."
download: ""
format-detection: "telephone=no"
hreflang: "en"
icon: "https://kura.pro/shokunin/images/favicon.ico"
id: "https://vrdlib.com/about/index.html"
image_alt: "Image of Random (VRD)"
image_height: "100vh"
image_width: "100vw"
image: "https://kura.pro/vrd/images/logos/vrd.webp"
keywords: "rust random number, Mersenne Twister Rust, Random (VRD) guide, rust programming, cargo package manager, rust random generator, rust API documentation, rust code examples, generating random numbers in rust, rust project setup"
language: "en-GB"
layout: "getting-started"
locale: "en_GB"
logo_alt: "Logo of Random (VRD)"
logo_height: "44"
logo_width: "44"
logo: "https://kura.pro/vrd/images/logos/vrd.webp"
menu: "active"
measurementID: "G-5QHNYC1FEJ"
name: "Random (VRD)"
permalink: "https://vrdlib.com/about/index.html"
rating: "general"
referrer: "no-referrer"
revisit-after: "7 days"
robots: "index, follow"
short_name: "random (vrd)"
subtitle: "Exploring the World of High-Quality Random Numbers with VRD"
tags: "Rust, Random, VRD, Mersenne, Twister, Cargo, Programming, Documentation, Examples, Setup"
theme-color: "167, 42, 0"
title: "Mastering Random (VRD): Your Rust Guide to Random Numbers"
url: "https://vrdlib.com/about/index.html"
viewport: "width=device-width, initial-scale=1, shrink-to-fit=no"

# RSS - The RSS feed front matter (YAML).

atom_link: "https://vrdlib.com/about/rss.xml"
category: "Software, Static Site Generator, Rust"
docs: "https://validator.w3.org/feed/docs/rss2.html"
generator: "Shokunin SSG (version 0.0.26)"
item_description: "Step-by-step guide on setting up Random (VRD) in Rust for high-quality random numbers using the Mersenne Twister algorithm."
item_guid: "https://vrdlib.com/about/rss.xml"
item_link: "https://vrdlib.com/about/rss.xml"
item_pub_date: "Sun, 10 Mar 2024 06:06:06 +0100"
item_title: "Mastering Random (VRD): Your Rust Guide to Random Numbers"
last_build_date: "Sun, 10 Mar 2024 06:06:06 +0100"
managing_editor: "contact@vrdlib.com"
pub_date: "Sun, 10 Mar 2024 06:06:06 +0100"
ttl: "60"
type: "website"
webmaster: "contact@vrdlib.com"

# Apple - The Apple front matter (YAML).

apple_mobile_web_app_orientations: "portrait"
apple_touch_icon_sizes: "192x192"
apple-mobile-web-app-capable: "yes"
apple-mobile-web-app-status-bar-inset: "black"
apple-mobile-web-app-status-bar-style: "black-translucent"
apple-mobile-web-app-title: "Mastering Random (VRD): Your Rust Guide to Random Numbers"
apple-touch-fullscreen: "yes"

# MS Application - The MS Application front matter (YAML).

msapplication-config: "https://vrdlib.com/browserconfig.xml"
msapplication-tap-highlight: "no"
msapplication-TileColor: "167, 42, 0"
msapplication_tile_image: "https://kura.pro/vrd/images/logos/vrd.webp"

# Twitter Card - The Twitter Card front matter (YAML).

twitter_card: "summary"
twitter_creator: "@wwdseb"
twitter_description: "Step-by-step guide on setting up Random (VRD) in Rust for high-quality random numbers using the Mersenne Twister algorithm."
twitter_image: "https://kura.pro/vrd/images/logos/vrd.webp"
twitter_image_alt: "Image of Random (VRD)"
twitter_site: "@wwdseb"
twitter_title: "Mastering Random (VRD): Your Rust Guide to Random Numbers"
twitter_url: "https://vrdlib.com/about/index.html"

# Humans.txt - The Humans.txt front matter (YAML).

author_website: "https://vrdlib.com/about/index.html"
author_twitter: "@wwdseb"
author_location: "London, UK"
thanks: "Thanks for reading!"
site_last_updated: "2024-03-10"
site_standards: "HTML5, CSS3, RSS, Atom, JSON, XML, YAML, Markdown, TOML"
site_components: "Shokunin SSG, Shokunin CLI, Shokunin Templates, Shokunin Themes, Kaishi SSG, Kaishi CLI, Kaishi Templates, Kaishi Themes"
site_software: "Shokunin, Rust"

---

Learn how to seamlessly integrate Random (VRD), a Rust library utilising the Mersenne Twister algorithm for generating high-quality random numbers, into your Rust projects. This guide covers everything from installation and setup to generating various types of random numbers. Enhance your Rust applications with efficient and predictable random number generation techniques.

## Getting Started with Random (VRD)

Random (VRD) is a Rust library for generating high-quality random numbers based on the Mersenne Twister algorithm. This guide will walk you through the process of setting up Random (VRD) in your Rust project and generating random numbers using its APIs.

![divider][divider].class="m-10 w-100"

## Prerequisites

Before getting started with Random (VRD), ensure that you have the following prerequisites:

- Rust programming language (version 1.x or higher)
- Cargo package manager

![divider][divider].class="m-10 w-100"

## Installation

To use Random (VRD) in your Rust project, you need to add it as a dependency in your `Cargo.toml` file. Open your project's `Cargo.toml` file and add the following lines under the `[dependencies]` section:

```toml
[dependencies]
vrd = "0.0.6"
```

Save the `Cargo.toml` file, and Cargo will automatically download and install Random (VRD) the next time you build your project.

![divider][divider].class="m-10 w-100"

## Importing Random (VRD)

To start using Random (VRD) in your Rust code, you need to import the necessary modules. Add the following line at the top of your Rust file:

```rust
use vrd::random::Random;
```

This line imports the `Random` struct from the `vrd::random` module, which provides the main functionality for generating random numbers.

![divider][divider].class="m-10 w-100"

## Creating a Random Number Generator

To generate random numbers, you first need to create an instance of the `Random` struct. You can do this by calling the `new()` method:

```rust
let mut rng = Random::new();
```

This creates a new random number generator with a default seed value. You can also provide a custom seed value by passing it to the `new_with_seed()` method:

```rust
let seed = 12345;
let mut rng = Random::new_with_seed(seed);
```

![divider][divider].class="m-10 w-100"

## Generating Random Numbers

With the random number generator created, you can now generate random numbers of various types. Here are a few examples:

### Generating Random Integers

To generate a random integer within a specific range, use the `int()` method:

```rust
let min = 1;
let max = 10;
let rand_int = rng.int(min, max);
println!("Random integer between {} and {}: {}", min, max, rand_int);
```

### Generating Random Floats

To generate a random float between 0.0 and 1.0, use the `float()` method:

```rust
let rand_float = rng.float();
println!("Random float: {}", rand_float);
```

### Generating Random Booleans

To generate a random boolean value, use the `bool()` method:

```rust
let rand_bool = rng.bool();
println!("Random boolean: {}", rand_bool);
```

These are just a few examples of the random number generation capabilities provided by Random (VRD). For more advanced usage and additional random number types, refer to the [API documentation](https://docs.rs/vrd).

![divider][divider].class="m-10 w-100"

## Examples and Documentation

Random (VRD) provides a set of examples and detailed documentation to help you make the most of its features. Here are some resources to explore:

- [Examples](https://github.com/sebastienrousseau/vrd/tree/main/examples): Check out the example code snippets demonstrating different use cases and techniques with Random (VRD).
- [API Documentation](https://docs.rs/vrd): Explore the complete API reference for Random (VRD) to learn about all the available methods and configurations.
- [GitHub Repository](https://github.com/sebastienrousseau/vrd): Visit the GitHub repository to explore the source code, report issues, and contribute to the development of Random (VRD).

![divider][divider].class="m-10 w-100"

## Next Steps

Congratulations! You have successfully set up Random (VRD) in your Rust project and learned the basics of generating random numbers using its APIs. You can now explore the various features and capabilities provided by Random (VRD) to enhance your random number generation needs.

If you have any questions or need further assistance, check our [**FAQs**](/faqs/index.html) and feel free to reach out to the  Random (VRD) community or open an issue on the [**GitHub repository**](https://github.com/sebastienrousseau/vrd).

Happy random number generation with Random (VRD)!

![divider][divider].class="m-10 w-100"

[divider]: https://kura.pro/common/images/elements/divider.svg "Divider"
