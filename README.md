# HIBERIUS — Unicode Toolkit

> Inspect, watermark and sanitize hidden Unicode characters. Free, offline, single-file. No install, no tracking, no data ever leaves your browser.

[![CI](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/ci.yml/badge.svg)](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/ci.yml)
[![CodeQL](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/codeql.yml/badge.svg)](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/codeql.yml)
[![Pages](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/pages.yml/badge.svg)](https://github.com/Hiberius/hiberius-unicode-toolkit/actions/workflows/pages.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-39FF14.svg)](LICENSE)
[![Built with Claude Fable 5](https://img.shields.io/badge/Built%20with-Claude%20Fable%205-8A2BE2.svg)](https://www.anthropic.com/)

**▶ Live demo:** <https://hiberius.github.io/hiberius-unicode-toolkit/>

---

## What is HIBERIUS?

HIBERIUS is a self-contained web tool for working with **invisible and special Unicode characters**. Text can carry characters you can't see — zero-width spaces, bidirectional overrides, exotic whitespace, control codes. They are used for good (watermarking documents to trace leaks) and for harm (hiding payloads, spoofing source code, smuggling data). HIBERIUS lets you **see them, remove them, and add them on purpose** — all in one page that runs entirely in your browser.

It ships as a **single HTML file**. Open it, and it works — even with no internet connection. Nothing is uploaded anywhere.

### Four tools in one

| Tool | What it does |
|------|--------------|
| **01 · Inject / Watermark** | Insert an invisible character at a chosen interval to fingerprint a piece of text, so you can later prove which copy leaked. Optionally hide a short secret message with zero-width steganography. |
| **02 · Scan / Detect** | Paste any text to reveal every hidden or suspicious character inline, listed with its exact code point, name and category. Also extracts any hidden steganographic message. |
| **03 · Clean / Sanitize** | Strip zero-width, bidirectional and control characters from untrusted input before you store, publish or commit it. Defends against *Trojan Source* attacks. |
| **04 · Character Library** | A searchable reference of special and useful Unicode characters with one-click copy. |

---

## Who it's for

- **Security engineers & developers** — sanitize untrusted input and detect [Trojan Source](https://trojansource.codes/) bidirectional-override attacks hidden in code and commits.
- **Writers, journalists & legal teams** — invisibly watermark confidential documents so a leaked copy can be traced back to its recipient.
- **Support & moderation teams** — spot text that has been tampered with using invisible characters.
- **Anyone** — clean messy text pasted from PDFs, chat apps or design tools that carries stray non-breaking spaces and control codes.

---

## How it works

HIBERIUS is **100% client-side JavaScript**. There is no backend, no build step, no dependencies and no telemetry.

- A single, curated dataset of special Unicode code points is the source of truth for all three engines (detect / clean / reference) — one list, no drift.
- **Detection** classifies each code point into `zero-width`, `bidi-control`, `unusual-space` or `control`, then rebuilds the text safely in the DOM using `textContent` only (never `innerHTML`), so pasted text can never execute.
- **Sanitization** filters the string by category with toggles for whitespace normalization, collapsing and Unicode `NFC` normalization.
- **Steganography** encodes a secret into UTF-8 → binary → zero-width bits (`U+200B` = 0, `U+200C` = 1), delimited by Word Joiners (`U+2060`), and reverses the process to extract it.
- Astral characters (emoji, etc.) are handled correctly via `Array.from` / code-point iteration.

The page makes **zero network requests** — verify it yourself in your browser's Network tab.

---

## Download & run

Pick whichever is easiest:

**1. Use it online (nothing to install)**
Open the live demo: <https://hiberius.github.io/hiberius-unicode-toolkit/>

**2. Download the single file**
Download [`index.html`](https://raw.githubusercontent.com/Hiberius/hiberius-unicode-toolkit/main/index.html) → double-click it → it opens in your browser and works offline forever. You can rename it to anything (e.g. `hiberius.html`).

**3. Clone the repo**

```bash
git clone https://github.com/Hiberius/hiberius-unicode-toolkit.git
cd hiberius-unicode-toolkit
open index.html      # macOS
# or: xdg-open index.html   (Linux) · start index.html   (Windows)
```

No Node, no npm, no dependencies. The tooling in this repo (linters, CI) is only for contributors.

---

## Usage guide

### 01 · Inject / Watermark

1. Paste your text into **Input**.
2. Choose **Inject every N chars** and the **character type** (default: `U+200C` ZWNJ).
3. *(Optional)* Type a **secret message** to embed invisibly.
4. Click **Inject** (or press <kbd>Ctrl/Cmd</kbd>+<kbd>Enter</kbd>). Copy or download the result.

The output looks identical to the input but carries an invisible fingerprint. Give each recipient a different interval/character and you can later identify the source of a leak by scanning their copy.

### 02 · Scan / Detect

1. Paste suspicious text into **Input**.
2. Click **Scan**. Every hidden character is shown as a colored chip (`U+XXXX`), listed with name and count, and any embedded secret message is extracted automatically.

A green verdict means the text is clean; an amber verdict lists exactly what was found.

### 03 · Clean / Sanitize

1. Choose your **sanitization rules** (sensible defaults are pre-selected).
2. Paste text into **Input** and click **Clean**. Copy or download the sanitized output.

### 04 · Character Library

Search by name, code point or category, then click **Copy** to grab any character.

---

## Special Unicode characters reference

A selection of the characters HIBERIUS knows about (the in-app **Library** is searchable and copyable):

| Code point | Name | Category |
|-----------|------|----------|
| `U+200B` | Zero Width Space (ZWSP) | Zero-width |
| `U+200C` | Zero Width Non-Joiner (ZWNJ) | Zero-width |
| `U+200D` | Zero Width Joiner (ZWJ) | Zero-width |
| `U+2060` | Word Joiner | Zero-width |
| `U+FEFF` | Zero Width No-Break Space (BOM) | Zero-width |
| `U+00AD` | Soft Hyphen | Zero-width |
| `U+202D` | Left-to-Right Override (LRO) | Bidi control |
| `U+202E` | Right-to-Left Override (RLO) | Bidi control |
| `U+2066`–`U+2069` | Directional Isolates (LRI/RLI/FSI/PDI) | Bidi control |
| `U+00A0` | No-Break Space (NBSP) | Unusual space |
| `U+2003` | Em Space | Unusual space |
| `U+3000` | Ideographic Space | Unusual space |
| `U+2028` / `U+2029` | Line / Paragraph Separator | Unusual space |

The full list (invisible formatters, all bidi controls, every unusual space and a set of handy symbols) lives in the app.

---

## Security & privacy

- **No network requests.** No fonts, scripts, images or analytics are fetched from anywhere.
- **Strict Content-Security-Policy** meta tag blocks external connections.
- **No `innerHTML` with user data** — pasted text is always inserted as text, never parsed as HTML.
- **No dependencies** — nothing to audit, nothing to get a CVE.
- Scanned by **CodeQL** on every push (see [Actions](https://github.com/Hiberius/hiberius-unicode-toolkit/actions)).

See [SECURITY.md](SECURITY.md) to report a vulnerability.

## Responsible use

HIBERIUS is a defensive and productivity tool. The watermarking and steganography features are intended for legitimate uses such as tracing document leaks, security research and education. **Do not** use it to bypass content filters, deceive people, or facilitate academic dishonesty. You are responsible for how you use it and for complying with the laws and policies that apply to you.

---

## Built with Claude Fable 5

This project was designed and built with **[Claude Fable 5](https://www.anthropic.com/)** (ultracode). The full engineering pipeline — architecture, hardening, accessibility, SEO and CI — was orchestrated with an AI agent workflow.

## 💼 Need a custom tool for your business?

**I build tools like this one — and I build them for companies.**

HIBERIUS went from a single prompt to a finished, hardened, SEO-ready, CI-green product. That's how I work: fast, and production-grade — not throwaway demos. Give me a problem, I hand you the tool that solves it.

**What I can build for you:**

- ⚡ **Web apps & SaaS** — Next.js / React end to end, authentication, billing (Stripe), multi-tenant architecture, shipped on Vercel or Cloudflare.
- 🤖 **AI-powered tools & agents** — LLM features that actually ship: assistants, chatbots, document processing, automations that replace hours of manual work.
- 📊 **Marketing & ads automation** — I'm also a performance marketer, so I build what marketers really need: tracking, attribution, reporting dashboards, and campaign automation across Meta, Google & TikTok.
- 🔧 **Internal tools & automation** — scrapers, data pipelines, CRMs and back-office utilities that save your team real time.
- 🌐 **Single-file & browser tools** — like HIBERIUS: zero-install, offline, private by design.
- 🛒 **Websites, e-commerce & WordPress** — Shopify stores, WordPress builds, and landing pages that convert.

**Why work with me:**

- I ship in **days, not months** — full-stack and AI-accelerated, with no agency overhead.
- Everything is **production-ready**: secure, accessible, tested, documented.
- I think like your **business**, not just like an engineer — I come from performance marketing.
- Based in **Italy 🇮🇹**, GDPR-aware by default.

**Let's talk.** [Open an issue](https://github.com/Hiberius/hiberius-unicode-toolkit/issues/new/choose) with what you need, reach me on [GitHub](https://github.com/Hiberius), or read the full pitch in [ABOUT.md](ABOUT.md).

> Have an idea or a process to automate? Tell me what you're trying to do — I'll tell you how I'd build it.

---

## Contributing

PRs welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). Please keep the tool a single dependency-free HTML file.

## License

[MIT](LICENSE) © Hiberius
