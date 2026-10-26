<!-- SPDX-License-Identifier: Apache-2.0 OR MIT -->

# Changelog

All notable changes to vrdlib.com are documented here.

## [0.0.2] - Unreleased

### Changed

- Rebuilt the site with Static Site Generator 0.0.69 and the Prism theme,
  coloured from the vrd logo, replacing the 2024 Shokunin site.
- Rewrote every page from the vrd repository at version 0.0.14 and the
  0.0.12 release on crates.io: the site now describes the Xoshiro256++
  default and the optional PCG, ChaCha20, SIMD and quasi-random backends,
  instead of the Mersenne Twister-only 0.0.6 API, and no longer suggests
  the default generator for cryptography.
- `make build` checks colour contrast (WCAG AAA), requires ssg's quality
  gate at 10/10, verifies every `#fragment` and SRI hash, renders one social
  image per page and runs `ssg audit`; the Pages workflow builds and deploys
  the result instead of uploading committed output.
- Removed Google Analytics, reCAPTCHA and the third-party scripts the old
  pages loaded; the site sets no cookies.

## [0.0.1] - 2026-10-26 (merged, not tagged)

### Changed

- Licensed the site's source under Apache-2.0 OR MIT.
- Deployed GitHub Pages with GitHub Actions instead of from a branch.
