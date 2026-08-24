# hq-dashboard — STATUS

Built 2026-08-23, autonomous mission from the _harvest-2026 ops directory.

## What this is

One self-contained static page ([index.html](index.html)) that fetches the public
`https://raw.githubusercontent.com/SpartanGomez/hq-state/main/HQ-STATE.md`
and renders it live. No build step, no backend, no analytics, no credentials.
The only dependency is `marked` 12.0.2 from cdnjs, SRI-pinned; if the CDN is
unreachable the page still renders with a built-in minimal formatter.

## Where it serves

- **Live:** https://spartangomez.github.io/hq-state/hq-dashboard/
- GitHub Pages was enabled from the CLI (`gh api --method POST repos/SpartanGomez/hq-state/pages`,
  build_type `legacy`, source `main` / root) — no web-UI clicks were needed.
  Pages config lives in repo Settings → Pages if it ever needs touching.

## What renders

- **ACTIVE** → cards up top: name, staleness badge, dir + section-regenerated line,
  what-it-is, top gaps as a numbered list, highest-leverage next move highlighted,
  stack/git/runs-today folded into a collapsible drawer.
- **EVERYTHING ELSE** → compact table (project / last activity / next); tap a name
  for its one-line description; stacks into cards under 640px.
- **NEW BUILDS WORTH STARTING** → numbered list with effort badges.
- **Any other section** (present or future) → rendered as plain markdown instead of breaking.
- Staleness by newest date in each entry (Git field preferred for active projects):
  green under 7 days, amber under 30, red at 30+, unmarked when no date appears.
- Refresh button, fetched-at timestamp, and an offline state that shows the last
  successfully fetched copy (kept in localStorage) under a visible error banner.

## Verified 2026-08-23

- Renders the real file: 3 active cards, 15 shelf rows, 5 new-build items, all
  three staleness colors present, zero console errors.
- Fetch-failure path: error banner + cached copy + clean recovery on refresh.
- Unknown-section tolerance: synthetic `## MYSTERY SECTION` renders as markdown.
- Phone (375px): single column, table stacked, no horizontal overflow.

## Boundaries (by design)

Reads exactly one public URL and nothing else. Contains nothing that is not
already in HQ-STATE.md. Writes nothing anywhere except a local cached copy of
the fetched file in the viewer's own browser.
