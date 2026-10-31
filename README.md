# ai-news

Per-date, per-language AI news data for the personal homepage.

Layout:

- `index.html` — standalone shell, the GitHub Pages entry point. It holds
  structure + styling + logic only (no news data embedded); it fetches
  `news/manifest.json` first, then loads only the selected date + language
  file, with a jsDelivr mirror fallback. No localStorage (language/theme
  state is session-only).
- `news/manifest.json` — the only trusted date list: latest date, update time,
  all dates (newest first), editions.
- `news/<date>.<lang>.json` — one file per date per language (`zh` / `en` /
  `ja`), flat single-language shape:
  `{"date","edition","items":[{"title","summary","url","source","category"}]}`.
- `radar/` — the "Play Radar" column: a daily scout for concrete, hands-on
  plays and projects (AI remote control, multi-agent orchestration,
  networking, local models and home compute). Same layout pattern as the
  news shell: `radar/index.html` (standalone shell, no embedded data),
  `radar/manifest.json` (trusted date list), and
  `radar/<date>.<lang>.json` in three languages with shape
  `{"date","items":[{"title","summary","url","source","outside"}]}`.
  The shell shows the latest three days up front and tucks older dates
  into a dropdown. Public copy only — what it is and where it comes from,
  no personal-fit commentary.

The homepage shell fetches `manifest.json` first, then loads only the
selected date + language file. This repo is intended to be public (GitHub
Pages serves the files); it contains only already-published news summaries —
no secrets, no credentials.
