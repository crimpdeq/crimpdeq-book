[![Deploy Book](https://github.com/crimpdeq/crimpdeq-book/actions/workflows/ci.yml/badge.svg)](https://github.com/crimpdeq/crimpdeq-book/actions/workflows/ci.yml)
[![Documentation](https://img.shields.io/badge/Documentation-Book-orange.svg)](https://book.crimpdeq.com)

# Crimpdeq Book

This repository contains the source of the ["Crimpdeq" book](https://book.crimpdeq.com).

## Quickstart

This book is generated using `mdbook`. To install it:

```
cargo install mdbook
```

With `mdbook` installed, you can clone the repository and start a development server by running:
```
git clone https://github.com/crimpdeq/crimpdeq-book
cd crimpdeq-book/
mdbook serve
```

Pushes to `main` build the book and deploy it to [book.crimpdeq.com](https://book.crimpdeq.com).

## Content

- Introduction: What is Crimpdeq?
- Build Your Crimpdeq: PCB, 3D-printed case, and prototype assembly
- Firmware & Flashing: web tools, local setup, and firmware internals
- Calibration: with the Crimpdeq app or nRF Connect
- Battery and Status LED

## Contributing
- Fixes and improvements are welcome. Please open an issue or submit a pull request.
- For small text changes, use the "Edit this page" link on any page, or edit the files under `src/` and run `mdbook serve` to preview.
