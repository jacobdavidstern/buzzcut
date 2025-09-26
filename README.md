# Buzzcut

## Overview

**Buzzcut** is a minimal, modular concept stub showcasing layout philosophy, semantic scaffolding, and audit-friendly configuration. It models reproducible development environments and onboarding clarity for future maintainers.

This repo preserves the build environment and config philosophy behind Jacob Stern’s portfolio projects. It is not a course artifact, but a standalone showcase of stewardship-driven tooling.

## Intent

Buzzcut is designed to:

- Demonstrate semantic HTML and modular CSS layout patterns
- Showcase multi-file ESLint and Prettier configurations
- Provide validation scaffolds for formatting and linting
- Serve as a reproducible base for future concept projects

## Technologies

- Semantic HTML5, Modular CSS
- ESLint (multi-file config with overrides)
- Prettier (base config + validation scripts)
- HTML validation: htmlhint, html-validate
- Git & GitHub, `.gitattributes` and `.gitignore` stewardship

## Development Environment

This repo uses a multi‑file configuration for style and linting.

### Prettier

- `prettier.base.cjs` — shared formatting rules
- `prettier.config.js` — imports base config
- Validation scripts in `package.json`:
  - `prettier:testfile` — verify config resolution
  - `prettier:force` — force‑apply formatting to test file
  - `prettier:checkfile` — check formatting on test file
  - `prettier:checkall` — check formatting across repo
  - `prettier:validate` — run all Prettier checks

### ESLint

- `eslint.base.cjs` — core linting rules
- `eslint.config-overrides.cjs` — targeted overrides
- `eslint.config.js` — imports base and overrides
- Validation script: `check:eslint` — lint all `.js`/`.cjs` files

### HTML Validation

- `htmlhint` — expanded ruleset
- `html-validate` — structural HTML checks
- Script: `lint:html` — run validation across repo

## Stewardship Notes

- `.gitattributes` and `.gitignore` are configured to privatize `/labs` while preserving folder structure
- `CHANGELOG.md` documents all notable changes with audit clarity
- `TESTING.md` scaffolds future validation strategies

## License

This repository is dedicated to reproducible environments and personal development.
Unless otherwise noted, all content is released under [The MIT License](https://mit-license.org/).

&copy; Jacob Stern, 2025–2026
