# Security Policy

## Design guarantees

HIBERIUS is a single, static HTML file with:

- **No backend** and **no network requests** — it cannot exfiltrate data.
- **No third-party dependencies** — no supply-chain surface.
- **A strict Content-Security-Policy** meta tag that blocks external connections.
- **No `innerHTML`/`eval`/`document.write`** on user-supplied data — pasted text is inserted as text only.

## Supported versions

The latest version on the `main` branch is supported.

| Version | Supported |
|---------|-----------|
| 3.x     | ✅        |
| < 3.0   | ❌        |

## Reporting a vulnerability

If you find a security issue, please report it privately using GitHub's
[**Report a vulnerability**](https://github.com/Hiberius/hiberius-unicode-toolkit/security/advisories/new)
feature, or open a minimal issue that does not disclose exploit details publicly.

Please include:

- A description of the issue and its impact.
- Steps to reproduce (a minimal input string is ideal).
- The browser and version you used.

You can expect an initial response within a few days.
