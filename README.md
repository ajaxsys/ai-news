# ai-news

Per-date, per-language AI news data for the personal homepage.

Layout:

- `news/manifest.json` — the only trusted date list: latest date, update time,
  all dates (newest first), editions.
- `news/<date>.<lang>.json` — one file per date per language (`zh` / `en` /
  `ja`), flat single-language shape:
  `{"date","edition","items":[{"title","summary","url","source","category"}]}`.

The homepage shell fetches `manifest.json` first, then loads only the
selected date + language file. This repo is intended to be public (GitHub
Pages serves the files); it contains only already-published news summaries —
no secrets, no credentials.
