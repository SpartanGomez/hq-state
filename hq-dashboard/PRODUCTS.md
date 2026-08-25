# PRODUCTS — live surfaces, ground-truthed

Regenerated 2026-08-25 by the launchpad mission: every URL below was fetched live that day; status reflects what the server actually returned, not what the repo intends. Sanitized for public hosting. Standing rule: any mission that changes a product's live state refreshes its block here in the same push (see CLAUDE.md).

Format contract for the dashboard: one `## Name` block per product; `- key: value` fields; `- shipped:` carries up to three dated sub-bullets; blocks ordered LIVE first, most recently updated first. A final `## SHIPS NEXT` section lists one-line items as `- action — ships what`.

## SpargoDomains
- url: https://spargodomains.com
- status: LIVE
- checked: 2026-08-25 — serving the full launch kit; title "SpargoDomains — buy domains at cost in your own Cloudflare account"; private app hostname correctly bounces to the edge login
- shipped:
  - 2026-08-23 — public launch: 28 prerendered routes live (compare + guide pages confirmed serving), honest 404s, privacy page
  - 2026-08-23 — free DNS resilience checker live and working at /tools/dns-checker
  - 2026-08-23 — pricing page live (free tier + founding annual, clearly marked draft); Renewal Sentinel deployed dark behind its kill switch
- next: five signed-in minutes — search-console verification + sitemap submission — then the announcement drafts go out

## K² — KnowledgeSquared
- url: https://k2knowledge.com/today
- status: LIVE
- checked: 2026-08-25 — calm redesign confirmed live (three-item nav, single link per trending card); today's content dated the same day — the daily automation is still unbroken
- shipped:
  - 2026-08-23 — calm redesign merged and deployed: three-item nav, 30-second reader scan, calm Browse, keyboard lenses; verified in EN and RU
  - daily — the Morning Paper self-updates on schedule (fresh again on 2026-08-25, streak unbroken since early July)
- next: one two-minute console visit sets the model-spend cap — the last launch gate; then the recurring send moves onto the automation engine's rails
- note: an older duplicate of the site still answers on its original subdomain with stale content and no redirect — worth one redirect rule

## Sember
- url: https://app.sembermeditation.com
- status: LIVE
- checked: 2026-08-25 — PWA serving; landing page live at sembermeditation.com; the service worker still carries the OLD un-hashed audio cache name, so the weekend's stale-audio fix is NOT live yet
- shipped:
  - 2026-08-12 — PWA live on its own domain with the marketing site beside it; old origin still answers and hands visitors over in-page
  - 2026-08-24 — stale-audio fix BUILT and verified on a branch (content-hashed cache name, startup purge, self-gating deploy) — awaiting the one deploy command
- next: merge the branch + one self-verifying deploy command ships the audio fix to every warm client

## HQ Dashboard
- url: https://spartangomez.github.io/hq-state/hq-dashboard/
- status: LIVE
- checked: 2026-08-25 — page loads and fetches state; this launchpad update is its biggest change since launch
- shipped:
  - 2026-08-25 — LAUNCHPAD: live products front and center with URLs and freshest changes; repo-state view moved behind a tab
  - 2026-08-23 — built and served on GitHub Pages, reading the public state file live
- next: nothing — it regenerates itself from this repo's files

## Operator portfolio
- url: https://spartangomez.com
- status: LIVE
- checked: 2026-08-25 — live and rendering the operations-leader portfolio (evidence tiles, selected work); note: it answers a plain browser fine but returns 403 to unauthenticated bots — deliberate or provider default, worth knowing when sharing links with tools
- shipped:
  - 2026-08-11 — the produced site launched: operator positioning, five sourced evidence numbers, three case decisions
- next: the standing identity decision (operator vs research vs advisory) — the site currently answers it in favor of operator

## RelayFlow
- url: none yet
- status: NOT-YET-LIVE
- checked: 2026-08-25 — nothing provisioned, nothing deployed, by design; the whole engine runs locally in dry-run with a credential-free surface check ready to point at the future URL
- shipped:
  - 2026-08-24 — scheduled sequence runner, approval-gated broadcasts, deliverability rails, internal send doorway — all dry-run proven, 287 tests
  - 2026-08-25 — deployed-surface verifier + stuck-work detector (freestyle round 3)
- next: the owner provisioning pass from the deploy runbook — database, hosting, webhook, schedule — then the surface check proves the deployment from any machine

## Renewal Sentinel (SpargoDomains × RelayFlow)
- url: rides the two products above
- status: NOT-YET-LIVE
- checked: 2026-08-25 — deployed dark on the domain product's side; dispatch rehearsed over live local HTTP; no cross-service call between deployed halves has ever happened
- shipped:
  - 2026-08-23 — nightly notice derivation (30/7/1 days), dedupe by construction, dispatch adapter, templates, end-to-end proof
- next: after RelayFlow deploys — hand the doorway credential across, flip two variables, watch the first night

## Mira (private)
- url: private by design — never listed
- status: NOT-YET-LIVE
- checked: 2026-08-25 — nothing deployed; the branch that would deploy is held by decision until two live safety evals run green
- shipped:
  - 2026-08-23 — install-day build + reverse-engineered spec + server-dictation fallback; 10/10 runnable gates green on the branch
- next: fund the project's own model account (minutes), run the two evals, then merge → one-command deploy → install day

## Voice-to-Desk (local)
- url: none — runs on the desk
- status: NOT-YET-LIVE
- checked: 2026-08-25 — built and tested (26/26), wired into the transcription batch; zero live classification calls yet
- shipped:
  - 2026-08-23 — voice memo → transcript → one model call → the daily companion's inbox, crash-safe, capped, dry-run default
- next: create the router's local env file with the project key, eyeball one dry run — then forget it exists

## SHIPS NEXT
- Set the model-spend cap (2 min, console) — ships K²'s last launch gate
- Create the router env file + one dry run (5 min) — ships the voice loop live
- Search-console verify + sitemap submit (5–15 min, signed-in browser) — ships SpargoDomains' indexing + reporting
- Merge + one self-verifying deploy command (30 min) — ships Sember's stale-audio fix
- Hold the 30-minute kill/keep call — ships K² Phase 2's shape
- Give the delete-ritual go order (1 h) — ships the portfolio cleanup
- Fund the household project's model account + run two evals (~2–4 h) — unblocks its merge, deploy, and install day
- Run the owner provisioning pass (1–3 h, runbook-scripted) — ships RelayFlow's deployed surface
- Two secrets + two variables after that — ships the Renewal Sentinel live
- One logged-in media session (2–3 h) — ships K²'s overdue episode and Sunday send
