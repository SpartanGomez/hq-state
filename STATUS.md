# STATUS — launchpad mission, 2026-08-25

Mission complete: 12 live surfaces ground-truthed by fetching them, PRODUCTS.md
created as the live-surface registry, the dashboard upgraded to a phone-first
LAUNCHPAD (live products front and center, repo-state behind a tab, reading
only this repo's two files same-origin), the private end-user tour delivered to
the ops directory, and the PRODUCTS.md refresh wired into CLAUDE.md as a
standing rule.

Ground-truth surprises worth knowing: the audience product's original subdomain
still serves a stale duplicate homepage with no redirect; the agent fleet's
assumed identity domain does not resolve at all (its work-order assumption A1
is unconfirmed until the domain is registered and pointed); the portfolio site
returns 403 to automated fetchers but renders fine in a real browser; and the
meditation app's live service worker confirms the weekend's audio-cache fix is
built but not yet deployed.

## Every NOT-YET-LIVE item and its one-click ship action
*(ranked by the dossier's almost-done order — ascending hours to ship)*

1. **Audience product's last launch gate** — one two-minute console visit sets
   the model-spend cap. Ships: the product fully gated at last.
2. **Voice loop** — create the router's local env file from its example with
   the project key, run one dry-run, eyeball the lines. Ships: spoken memo →
   desk inbox, live.
3. **Domain product's indexing** — five signed-in browser minutes:
   search-console verification + sitemap submission. Ships: accelerated
   discovery + the reporting console.
4. **Meditation app's audio-cache fix** — merge the branch, run the one
   self-verifying deploy command. Ships: every future audio re-render reaches
   warm clients automatically.
5. **Audience product's Phase 2 shape** — hold the 30-minute kill/keep call
   (evidence pack is mission B7 in the ops queue). Ships: a decided channel
   plan instead of a four-week stall.
6. **Portfolio cleanup** — give the delete-ritual go order (both staged
   folders, salvage list first). Ships: ~13 dead repos gone.
7. **Household project** — fund its own model account (minutes of hands,
   small spend), run the two live safety evals, read the answers. Ships: the
   merge/deploy/install-day chain unblocks.
8. **Automation engine's deployed surface** — run the owner provisioning pass
   scripted end-to-end in its deploy runbook, then fire the credential-free
   surface check at the new URL. Ships: the engine exists in production,
   dry-run and disarmed.
9. **Renewal Sentinel** — after item 8: hand the doorway credential across,
   set two secrets, flip two variables, deploy, watch the first night. Ships:
   the triangle's first real standing workload.
10. **Audience product's overdue episode + Sunday send** — one logged-in media
    session (re-render, upload, wire, schedule). Ships: the first flagship
    week since early July — and the send moves onto the engine's rails right
    after (mission B4).

Deliverable record: PRODUCTS.md (+ dashboard copy) · hq-dashboard/index.html
(LAUNCHPAD, verified rendering locally before commit) · the private tour in
the ops directory · CLAUDE.md standing-rule amendment · this file. One commit
per deliverable; sanitize grep run clean including email-shaped strings.

## Second pass + full account sweep, 2026-08-25

All surfaces re-verified at the header level, and the owner's entire code-host
account walked: every repository's visibility, freshness, and local↔remote
mapping recorded in the private dossier.

Corrections and finds:
- The audience product's pre-rename domain serves the SAME current site (the
  first pass wrongly called it stale); the gap is a missing canonical
  redirect, one rule to add. The www hostname resolves for neither that
  product nor the domain product — two DNS records fix both.
- The live portfolio site's deployed source is NOT in its repository (last
  commit months before the relaunch) — a salvage commit protects it.
- The meditation app has a store-launch branch on the remote that no local
  file mentions (signing work done); its audio-fix branch is local-only.
- The automation engine's weekend work sits as one open draft PR, confirmed.
- The sweep found three recent private repos absent from the local workspace
  — a chat-side ops board with eight open decisions (one carries a real
  invoice amount), a private client-page mock, and a small voice utility —
  plus roughly a dozen dormant pre-2026 repos worth a batch archive pass.
  Specifics live in the private dossier only.
- The staged local delete ritual is confirmed safe: everything it removes
  survives in the account's private repositories.
