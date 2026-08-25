# HQ-STATE

Machine-state snapshot of the Projects workspace. Generated 2026-08-23 by a read-only recon pass; regenerated at the end of every mission so this file always shows current state.
Sanitized for public hosting: no credentials, no env values, no personal or client data — sensitive facts are described by shape, not contents.

---

## STRATEGY — portfolio verdicts + the fridge page, sanitized (2026-08-24)

1. Portfolio thesis: one triangle sharing rails (the automation engine, the domain product, the audience product), one household project, one personal operating system — everything else feeds a front, parks with a written wake condition, or dies this month.
2. The binding constraint is owner-click time, not code: a five-item, roughly forty-minute gate queue is holding back five otherwise-finished lines.
3. SHIP verdicts with weeks attached: the domain product's two parked owner steps and the meditation app's one-command deploy and the voice loop's key (this week); the automation engine's provisioning pass, the notice loop's go-live flip, and the household project's fund-evals-deploy sequence (next week); the operations-role decision and the research erratum (the week after).
4. The audience product keeps shipping, but its recurring send moves off manual sessions onto the automation engine's rails — four stalled distribution weeks are the portfolio's one repeated failure, and the fix is structural, not motivational.
5. FEED verdicts: the daily companion, the kanban board, the archive-mining tool (whose dogfood run is a mission, with a written graduation condition), the dashboards, the thinking instruments.
6. PARK verdicts, each with a wake condition: the agent fleet (the go order), the compliance-gated game project (its own same-day verdict ran green and named ship-the-fallback — the portfolio layer still parks the launch decision with the owner, with a dated conversion to KILL), the consulting kit (the identity decision), two creative projects (their seasons).
7. KILL verdicts with salvage-first lists: the superseded overlay, four overlapping job-search tools (the weekly scan survives), a morning-ritual spec, the empty and absorbed folders — the long-staged delete ritual executes them.
8. Where a verdict contradicts sunk cost, the dossier says so plainly: the largest build has the weakest founder-fit, and a long-planned migration is judged by its monthly bleed, not its documentation.
9. Anti-synergy named: three unrelated audiences must never multiply manual distribution — rails are shared, audiences are not, and no fourth audience starts this quarter.
10. The standing rule this quarter: no new builds while the gate queue is non-empty; automate a channel or drop it. Full reasoning lives in the private dossier; the operating law is public in HQ-DOCTRINE.md in this repo.

---

## ACTIVE

### RelayFlow (dir: SpargoEmailAutomations) — section regenerated 2026-08-25 (freestyle round 3, timeboxed)

**What it is:** Diagram-first email/SMS automation builder carrying a real execution engine underneath the demo: a scheduled sequence runner, approval-gated broadcast sends, full deliverability rails, and an internal doorway through which other first-party services request single compliant transactional sends — built to run a six-email welcome flow for the K² newsletter and to carry SpargoDomains' renewal notices.

**Stack:** Next.js 16 (App Router) + React 19 + TypeScript strict, Tailwind v4, React Flow 12 + dagre, Zustand, Zod v4. Supabase (Postgres, 10 migrations) for send-side data AND scheduling (pg_cron calling an authenticated tick endpoint), with a zero-config local file fallback behind every store. Transactional email provider behind a signed inbound webhook with a full event ledger; mock providers plus an engine-wide dry-run mode by default; one shared rate limiter paced at 2 requests/second. Vercel hosting with a code-level "public surface only" deploy gate. 34 Vitest suites (287 tests).

**Git:** three mission phases, an amendments pass, a contract-reconciliation pass, and two justify-first freestyle rounds sit as one open draft PR of per-deliverable commits; base `main` last moved 2026-08-18. Round 3 (timeboxed, operator-risk picks): a deployed-surface verifier and a stuck-work detector.

**Runs today:** Yes — zero config: the builder demo, plus the whole execution loop in dry-run against local file stores. One-command sequence rehearsal on an injected clock, a step-preview renderer, a 15-check health command, a dispatch rehearsal that proves the Sentinel agreement over live localhost HTTP against the production build, and — new — a one-command, credential-free, read-only smoke check runnable against any DEPLOYED URL: the operator surface must answer 404, every public endpoint must fail closed (naming any missing config), and the unsubscribe surface must be served on the links host (12/12 against a local production boot). The health command now also catches work that rots while the scheduler stays green: held or abandoned notices and overdue enrollments, with thresholds tunable by env. Real sending stays deliberately unprovisioned AND deliberately hard to reach: broadcast mode off by default with per-batch operator approval; notices held unsent until the brand row carries a real postal address; double-sends refused by construction; auto-suppression on hard bounce, complaint, or repeated soft bounces.

**Top 3 gaps (docs vs code):**
1. The Renewal Sentinel loop's two halves speak one written agreement (SpargoDomains' dispatch document, adopted verbatim into the shared coordination log after a full diff) and the doorway answers it synchronously, proven in-process and over real localhost HTTP. What has never happened is a live cross-service call between the two deployed products: both deployments and the shared credential are owner-hands steps, and the Sentinel's nightly job stays in its no-network rehearsal mode until they exist.
2. Everything is built but nothing is provisioned or merged: the draft PR awaits review, and the dedicated database project, hosting environment, webhook registration, and the five-minute schedule are owner-hands steps, scripted end to end in the deploy runbook — which now ends every deploy with the credential-free surface check, so the riskiest go-live misconfigurations are machine-detectable from any machine. The six-email welcome copy in the seed is still draft.
3. The canvas demo and the execution engine remain parallel systems: compiled canvas workflows (branches, wait-for-event) do not feed the runner — only linear sequences, broadcasts, and single notices execute — and the demo's core domain is still per-browser localStorage.

**Highest-leverage next move:** The owner provisioning pass from the deploy runbook — including handing the doorway's shared credential to the Sentinel and pointing its dispatch address at the live endpoint — then the credential-free surface check plus a cross-service dry-run soak before either side goes live. That turns both products' halves into the first real standing workload: compliant renewal notices, end to end.

---

### Mira

**What it is:** A private, Spanish-language "answer machine" PWA for one older adult: she speaks a question or photographs a letter, gets one plain-language card back, and the app remembers her ongoing topics so she never re-explains them.

**Stack:** TypeScript monorepo. Client: Vite + React 19 PWA (7 screens, service worker, strict same-origin CSP). Server: Express 5 + SQLite, SSE streaming, in-process cron (nightly backup, timed purges). Claude models via the official SDK, model-routed (cheap text model + stronger vision/escalation model, env-configurable), plus a flag-gated server-dictation layer speaking the OpenAI-compatible transcription protocol with zero added dependencies. Vitest (101) + Playwright (90, WebKit iPhone + Chromium). Railway hosting via Dockerfile with a persistent volume and healthcheck.

**Git:** branch `master`, last commit 2026-07-30 — "Verification suite, gate runner, and fixes found by running it." The install-day worktree branch is now 20 commits ahead (last 2026-08-23) across two same-day missions plus a cofounder decision pass, and is **held from merging by decision** until both live safety evals are green. Aboard it: gap audit, auth route-inventory pinning, server-side string table with untranslated-copy gates, the one-command install-day check, deploy runbook, a shell-serving fix the gates caught, a reverse-engineered SPEC.md the repo can audit itself against, and the built server-dictation fallback.

**Runs today:** Yes, immediately, in mock-AI mode (`npm run dev`, mock answers watermarked, no credentials needed). On the worktree branch, `npm run install-day` is one command: build, a 12-check smoke run driving the real letter fixtures through the live HTTP pipeline, then the printed phone runbook with five ~5-minute on-phone test scripts. Deploying is one documented command; nothing is deployed yet.

**Top 3 gaps (docs vs code):**
1. The original spec documents still do not exist anywhere on the machine. The worktree branch now carries SPEC.md — every referenced requirement reverse-engineered from its enforcing code and tests, self-contradictions recorded with the safer reading chosen — but one requirement number is referenced nowhere and half the law numbering is reconstruction; only the original file can settle those.
2. The two live-model safety evals (one-question discipline, hostile-letter red-team) remain **parked awaiting funding of the project's own model-provider account** — decided: eval spend runs on that account only, human-funded via the provider console (~US$1 per round, procedure in the repo's EVAL-RESULTS.md). Everything else automatable is green: 10/10 runnable gates, zero test failures.
3. Spanish dictation on her actual phone is still untested — but every branch of that unknown now ends warm: first-class typing path, printed fallback card, and the built server-dictation exit, so a bad mic verdict on install day is a two-variable config flip and a redeploy.

**Highest-leverage next move:** Fund the project account and run one eval round green — by decision, nothing merges or deploys before that. At fund-time also fill the already-locked dictation-fallback config (an OpenAI-compatible transcription endpoint; values chosen then, shipped defaults until). Then merge, deploy with the one command, and the install-day visit — its five on-phone scripts (repo GATE-STATUS.md) are all that remains unverifiable by machine.

---

### SpargoDomains — section regenerated 2026-08-23 (launch executed)

**What it is:** A single-user, safety-first domain search-and-purchase tool over the official Cloudflare Registrar API — invent a name, verify live availability and price, register it at cost in your own Cloudflare account — now publicly launched: the crawler-indexable marketing site, credential-free demo, free DNS resilience checker, draft pricing page, and 20 comparison/guide content pages are live on the production domain, with the Renewal Sentinel notice loop deployed dark behind its kill switch.

**Stack:** React 19 + Vite + TypeScript, Tailwind + shadcn-style UI, TanStack Query. Hono API on Cloudflare Workers — one Worker serves the API, the private SPA, and a build-time-prerendered public site (28 routes, hostname-aware, sitemap + robots). Drizzle ORM on Cloudflare D1 (now including a deduped, append-only renewal-notices table). Cloudflare Access JWT auth gated to a single admin identity. Money as decimal strings via big.js. Nightly cron: read-only reconciler + notice derivation/dispatch. 192 Vitest cases + 11 Playwright tests.

**Git:** branch `main`, last commit 2026-08-23 — `launch-kit` (both completed missions: the launch kit and Renewal Sentinel) merged on the owner's go order and deployed to production the same night; the code now also lives in a private GitHub repository. Production migrations applied additively; rollback is one revert plus a redeploy.

**Runs today:** Yes — live and verified in production: the public pages serve real prerendered HTML (marketing title confirmed, comparison pages answering 200, robots and sitemap advertised), the DNS checker runs real checks on the live site, and the private app hostname still bounces unauthenticated visitors to the edge login. The public contact mailbox named on the privacy page now receives mail: email routing is enabled with MX and SPF records live, forwarding to the owner's personal inbox — the site's own DNS checker immediately noticed and honestly reports every layer concentrated on one provider, as designed. Production remains purchase-disabled and dry-run; the notice loop ships dark behind its own kill switch.

**Top 3 gaps (docs vs code):**
1. Renewal Sentinel is built and proven end to end but dark: dispatch defaults to dry-run behind a kill switch, and going live needs the counterpart internal-send endpoint on RelayFlow's side (the contract is written and paste-ready) plus a deliberate two-variable flip. The pricing page's retention promise now has code behind it, but no customer has seen an email.
2. Search-engine property verification and sitemap submission are parked as blocked: they need the owner's own account session in a browser, which no tool could reach tonight. The live robots file already advertises the sitemap, so discovery happens regardless — submission only accelerates it and unlocks the reporting console.
3. The checklist expected the private hostname's robots file to answer with a disallow, but the edge access gate intercepts the request before the Worker can respond — harmless in practice (every URL there redirects off-domain to a login), fixable with a deliberate bypass rule for that one path if wanted.

**Highest-leverage next move:** Owner completes the parked search-console step (about five minutes in a signed-in browser), then runs the announcement plan on the owner's own schedule — the drafts are ready and nothing has been posted, by explicit instruction. Meanwhile RelayFlow's side of the dispatch contract is what turns the retention promise real.

---

## EVERYTHING ELSE

**KnwoeldgeSquaredClaude (K² / KnowledgeSquared)** — Next.js 15 + Supabase trilingual web app that translates research papers into plain language ("Science, translated"), live at its custom domain. Verdict mission 2026-08-23: `feat/calm-redesign` passed the repo's full definition-of-done with zero fixes, and on the owner's explicit order was **merged and deployed the same day** — the calm redesign (three-item nav, single-link trending, reader keyboard + hand-off, calm Browse) is verified live in EN and RU. The spend-cap card (0008) was attempted on order but stays owner-only: no browser session to drive, and the paid translate step has provably been running capless for weeks.
Next: owner sets the Anthropic monthly cap (~2 minutes, console → Limits, ~$30/mo on record) — now the only launch gate standing.

**MeditationApp (Sember)** — Offline meditation app: Tauri 2 + React desktop plus installable PWA, pre-rendered neural-TTS audio, no accounts, no telemetry; shipping. Mission 2026-08-24: the known stale-audio issue is fixed on a worktree branch (4 commits ahead of main) — the service-worker audio cache name is now a content hash of the shipped audio corpus, injected into both places that must agree from one source; a startup purge drops caches from earlier deploys; an 8-check proof script (changed clip ⇒ changed name, plus built-output verification) gates the deploy command itself; verified end to end at runtime against the production build in a real browser. Deliberately frozen internal identifiers untouched — the old cache name survives as the frozen prefix. Nothing deployed, per mission order.
Next: merge the worktree branch, then `cd app && npm run deploy:web` — the deploy now self-verifies, and every future audio re-render invalidates warm clients automatically.

**Personal Note Taker (DailyReflect)** — Electron daily companion (one markdown file per day, hand-of-five todos with carry-forward, pomodoro widget, ceremonies) at v9.17; actively shipped, stable, runs with plain `npm start`.
Next: maintenance mode — split the single giant design doc and confirm backup rotation stays healthy.

**ThreadWork** — Electron + React + SQLite local-first control plane that imports ChatGPT/Claude export archives and reconstructs projects (decisions, open loops, delegation to a worker or the Claude API); youngest project (one day of git history), runs today.
Next: dogfood one real export ZIP end to end (import → reconstruct → confirm) before adding features.

**KanBanBoard** — Zero-dependency Python local kanban (markdown card files are the source of truth) that doubles as the K² product + marketing task board; complete and stable since June, runs with `python board.py`.
Next: use it, don't develop it.

**LeagueClimbOS** — First-generation League-coaching overlay dashboard (Node + React + Electron), idle since mid-July and superseded by the compliance-hardened rewrite in LeagueClimber; its old self-contained installer was built for personal use only and must never be shared.
Next: confirm retirement in favor of LeagueClimber and archive.

**LeagueClimber (RANK ONE)** — Compliance-first League coaching monorepo (Fastify API, Tauri 2 overlay, web simulator, policy/analytics packages). Verdict mission 2026-08-24: the repo is now under local git, and the full verify + compliance suites ran green in mock mode — 1610 TypeScript tests, the 77-test policy gate, 29 Rust tests, both build-time scanners, plus a runtime smoke of the simulator and API — after two small fixes (doc formatting drift, and a secret-scanner regex bug that failed every correctly configured machine). VERDICT.md is on record: everything enabled sits in the platform's permitted tier, the five gated differentiators stay off pending written approval either way, and the named pick is **ship-fallback-now** — run it as v1 on a personal development key while the five written policy questions go out in parallel; approval blocks nothing v1 needs.
Next: owner reads VERDICT.md and, on agreement, starts the v1 pilot (personal dev credential into the local env, adapters flipped to live) and submits the Q1–Q5 letter the same week.

**PrincipleFirstJobber** — Tauri 2 + SvelteKit + SQLite/Drizzle job-search desktop app with AI-assisted tooling; last touched 2026-05-19, runs with setup, but the README is still scaffold boilerplate so actual scope is undocumented.
Next: skim the routes and smoke-test to establish what's actually built.

**brand-os** — Personal branding/positioning doc system (strategy boards, scorecards, launch runbook) whose produced site launched 2026-08-11; not an app, and its audit flags private ops actions still owed.
Next: clear its own flagged security items; keep the audit catalog private.

**buzz-bridge** — Working Node bridge that runs five Claude-backed agents as members of a Nostr-based team-chat workspace (mention-gated, loop-guarded, daily reply caps); tested 5/5 on 2026-07-31, runs with setup, has never run live. The v1 build plan is now written (2026-08-24): a five-mission burn day attaching per-charter tools, a public agent-identity domain, and OS-credential-store key storage, with a red-team acceptance gate.
Next: owner reads the work order in the ops directory, confirms its assumptions (the setup decisions it plans around were never recorded on this machine), and calls the burn day.

**voice-inbox (+ Voice-to-Desk router)** — Drop-audio-in-folder voice capture, now a closed loop (built 2026-08-23): the batch script feeds the local whisper-based transcriber, then auto-launches a small Node router that classifies each new transcript with one Claude API call and appends correctly-shaped lines (todo / journal / note, project-tagged) to DailyReflect's drainable inbox file — spoken in the car, on the desk within 30 seconds of transcription, zero new UI. Crash-safe at-most-once appends, a daily API-call cap, dry-run mode, no transcript content in logs, its own per-project key in a local untracked env file; 26/26 offline tests including two that assert the line grammar against DailyReflect's real parser. Repo initialized (local, per-deliverable commits).
Next: operator setup — put the project's API key in the router's local env file and eyeball one dry run (OPERATOR-GUIDE steps 4–5); no live call has been made yet.

**OWP-EMAIL-V2** — Documentation/deliverables bundle for a nonprofit's email-marketing rebuild (migration specs, an HTML email template, a carrier-registration resubmission package, onboarding decks); not an app, last touched 2026-06-30.
Next: the blockers are all external/ops (carrier registration, ESP automation-tier ceiling, missing email-auth DNS records, survey routing) — execute that checklist; nothing to build here.

**OWP-Email-Marketing** — Earlier planning stage of the same effort: journey diagrams, audit/dedupe/migration gameplans, plus raw audience exports (real-person data that must never leave this machine); last touched 2026-05-13.
Next: fold decisions into V2 and relocate the personal-data exports out of any synced or publishable path.

**_harvest-2026** — Private ops working directory: command-center dashboards, the mission queue (regenerated to v3 on 2026-08-24, reflecting the whole weekend burn), the agent-fleet v1 work order, portfolio dossier, dated harvest notes, safe-to-delete lists, ~11 project sub-buckets; not an app. Now a local-only git repo tracking just the mission documents.
Next: leave as-is; when cleaning, act on its own safe-to-delete lists.

**_to_delete-2026-07-30** — Staging folder for a pending delete ritual (retired project copies).
Next: execute the deletion pass already queued in the mission log.

---

## NEW BUILDS WORTH STARTING

**1. Renewal Sentinel — the SpargoDomains notification loop, sent through RelayFlow's rails.** Both active products are one build apart from each other's missing half: SpargoDomains has a nightly cron reconciler and portfolio-health data but no way to email anyone; RelayFlow has production-proven compliant sending (suppression, signed unsubscribe, send log) but no recurring real-world sender to justify it. A small Worker-to-RelayFlow hook that turns "domain expires in 30/7/1 days" into a compliant transactional email closes SpargoDomains' only named revenue blocker and gives RelayFlow its first standing production workload. Effort: ~12–18 hours.

**2. Voice → Desk router.** Realized 2026-08-23: built as `router/` inside voice-inbox and wired into the existing transcription batch script — see the voice-inbox entry above. What remains of this idea is the operator's five-minute key setup and one real-memo dry run; after that, using it.

**3. Buzz fleet v1 — give the five agents hands.** Planned in full 2026-08-24: the ops directory now holds the complete work order — five missions (~14 hours, one burn day) attaching per-charter tools behind default-deny allowlists and a sandboxed draft-outbox, moving agent keys into the OS credential store, publishing verified public identities on the fleet's own domain, and ending in a red-team acceptance gate. Hard laws carried in writing: mention-gated, loop-guarded, daily caps, no money/email/calendar, silence is never consent. What remains of this idea is the owner's GO: read the order, confirm its assumptions (the setup decisions it plans around were never recorded on this machine), and call the burn day.

**4. K² launch sequence as RelayFlow's first real workflow.** Largely realized as of 2026-08-24: the sequence runner now exists and ships with the six-step K² welcome flow seeded, rehearsable, and dry-run-verified end to end. What remains of this idea is the owner provisioning pass, the approved welcome copy, and — longer term — the bridge that lets compiled canvas workflows (branches, wait-for-event) feed the runner. Effort remaining: provisioning is under an hour; the canvas bridge is its own project.

**5. HQ dashboard that reads this file.** Realized 2026-08-23: built as `hq-dashboard/` in this repo and served by GitHub Pages — see the DASHBOARD section below. Nothing remains of this idea except using it.

---

## DASHBOARD

**What it is:** A live rendering of this file — one self-contained static page (`hq-dashboard/index.html`, no build step, no backend) that fetches the raw HQ-STATE.md on open and on demand, so the current state is readable from any device without cloning anything.

**Where:** https://spartangomez.github.io/hq-state/hq-dashboard/ (GitHub Pages, enabled 2026-08-23 from the CLI, serving `main` root; the page itself reads only the raw public URL of this file).

**How it renders:** ACTIVE as cards up top (top gaps, highest-leverage next move, the rest folded away), EVERYTHING ELSE as a compact table, NEW BUILDS as a numbered list, staleness color-coded by last-commit age (green under 7 days, amber under 30, red past 30). Sections this file grows later render as plain markdown rather than breaking, and a fetch failure falls back to the viewer's last cached copy — so regenerating this file per the standing rule is the only maintenance the dashboard needs. Build record: `hq-dashboard/STATUS.md`.
