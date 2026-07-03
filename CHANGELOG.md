# Changelog

All notable changes to this project are documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [3.0.0] - 2026-07-03

### Added

- **Scan / Detect** tool: reveals every invisible or suspicious character inline
  with code point, name, category and counts; extracts hidden steganographic messages.
- **Clean / Sanitize** tool: removes zero-width, bidirectional and control
  characters with toggles for whitespace normalization, collapsing and Unicode NFC.
- **Character Library**: searchable, copyable reference of special and useful Unicode characters.
- Zero-width steganography: hide and extract short secret messages.
- Strict Content-Security-Policy, offline-first (no network requests), full keyboard/ARIA support.
- SEO metadata, Open Graph tags and JSON-LD structured data.
- CI: HTMLHint, markdownlint, Prettier, CodeQL, link check and GitHub Pages deploy.

### Changed

- Renamed the project from **SPECTRIX** to **HIBERIUS**.
- Rebuilt as an accessible, multi-tool interface with a shared character dataset.
- Removed the external Google Fonts dependency for a fully self-contained, offline file.

[3.0.0]: https://github.com/Hiberius/hiberius-unicode-toolkit/releases/tag/v3.0.0
