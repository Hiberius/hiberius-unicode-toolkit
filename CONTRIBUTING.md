# Contributing to HIBERIUS

Thanks for your interest! Contributions are welcome.

## Ground rules

1. **Keep it a single file.** The tool must stay one self-contained `index.html` with no runtime dependencies and no network requests.
2. **No `innerHTML` / `eval` / `document.write`** on user input. Build DOM with `createElement` + `textContent`.
3. **Preserve privacy.** Nothing may be fetched from or sent to any external origin.
4. **Accessibility matters.** Keep ARIA roles, labels, keyboard support and focus states working.

## Local checks

No build is required to use the tool. To run the same checks CI runs:

```bash
npx --yes htmlhint index.html
npx --yes markdownlint-cli2 "**/*.md"
npx --yes prettier --check "**/*.{md,json,yml,yaml,css}"
```

## Pull requests

- Keep changes focused and describe the motivation.
- Update `README.md` and the in-app **Library** if you add characters.
- Make sure CI is green before requesting review.

## Reporting bugs / requesting features

Use the [issue templates](https://github.com/Hiberius/hiberius-unicode-toolkit/issues/new/choose).
