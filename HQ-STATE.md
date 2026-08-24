# HQ-STATE

Machine-state snapshot of the Projects workspace. Generated 2026-08-23 by a read-only recon pass; regenerated at the end of every mission so this file always shows current state.
Sanitized for public hosting: no credentials, no env values, no personal or client data — sensitive facts are described by shape, not contents.

---

## ACTIVE

### RelayFlow (dir: SpargoEmailAutomations) — section regenerated 2026-08-24 (later)

**What it is:** Diagram-first email/SMS automation builder carrying a real execution engine underneath the demo: a scheduled sequence runner, approval-gated broadcast sends, full deliverability rails, and now an internal doorway through which other first-party services request single compliant transactional sends — built to run a six-email welcome flow for the K² newsletter and to carry SpargoDomains' renewal notices.

**Stack:** Next.js 16 (App Router) + React 19 + TypeScript strict, Tailwind v4, React Flow 12 + dagre, Zustand, Zod v4. Supabase (Postgres, 9 migrations) for send-side data AND scheduling (pg_cron calling an authenticated tick endpoint), with a zero-config local file fallback behind every store. Transactional email provider behind a signed inbound webhook with a full event ledger; mock providers plus an engine-wide dry-run mode by default; one shared rate limiter paced at 2 requests/second. Vercel hosting with a code-level "public surface only" deploy gate. 35 Vitest suites (278 tests).

**Git:** three mission phases plus an amendments pass (execution engine → deliverability/broadcasts/templates/hardening → ledger, soft-bounce escalation, flow simulator → bulk-send philosophy retrofit + the internal send doorway) sit as one open draft PR of per-deliverable commits; base `main` last moved 2026-08-18.

**Runs today:** Yes — zero config: the builder demo, plus the whole execution loop in dry-run against local file stores. One-command sequence rehearsal on an injected clock, a step-preview renderer, and a 13-check health command. Real sending stays deliberately unprovisioned AND deliberately hard to reach: broadcast mode is off by default and every real batch needs an individual operator approval; internal transactional notices are held unsent until the brand row carries a real postal address; the engine refuses double-sends by construction and auto-suppresses on hard bounce, complaint, or repeated soft bounces.

**Top 3 gaps (docs vs code):**
1. The two halves of the Renewal Sentinel loop have not shaken hands: RelayFlow's internal send doorway is built, tested end to end in dry-run, and idempotent per (service, request identifier) — but it was shaped without sight of the dispatch contract SpargoDomains wrote (that file lives only on the owner's machine), so contract reconciliation and the Sentinel's own acceptance test are parked until the contract is pasted into the shared coordination log or the repo becomes reachable.
2. Everything is built but nothing is provisioned or merged: the draft PR awaits review, and the dedicated database project, hosting environment, webhook registration, and the five-minute schedule are owner-hands steps, scripted end to end in the deploy runbook. The six-email welcome copy in the seed is still draft.
3. The canvas demo and the execution engine remain parallel systems: compiled canvas workflows (branches, wait-for-event) do not feed the runner — only linear sequences, broadcasts, and single notices execute — and the demo's core domain is still per-browser localStorage.

**Highest-leverage next move:** Paste the Sentinel dispatch contract into the coordination log and reconcile the doorway to it exactly — that plus the owner provisioning pass turns both products' halves into the first real standing workload: compliant renewal notices, end to end.

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

### SpargoDomains

**What it is:** A single-user, safety-first domain search-and-purchase tool over the official Cloudflare Registrar API — invent a name, verify live availability and price, register it at cost in your own Cloudflare account — with a public, crawler-indexable marketing site, a credential-free demo, a free DNS resilience checker, a draft pricing page, and now a renewal-notice loop (Renewal Sentinel) that turns approaching expiry dates into compliant emails through RelayFlow's rails.

**Stack:** React 19 + Vite + TypeScript, Tailwind + shadcn-style UI, TanStack Query. Hono API on Cloudflare Workers — one Worker serves the API, the private SPA, and a build-time-prerendered public site (28 routes, hostname-aware, sitemap + robots). Drizzle ORM on Cloudflare D1 (now including a deduped, append-only renewal-notices table). Cloudflare Access JWT auth gated to a single admin identity. Money as decimal strings via big.js. Nightly cron: read-only reconciler + notice derivation/dispatch. 192 Vitest cases + 11 Playwright tests.

**Git:** branch `main`, last commit 2026-08-17 — "Act on the marketing handoff: hero, screener, and the demo's honest ending." Branch `launch-kit` now holds 13 unmerged commits across two completed missions: the launch kit (SEO prerendering, DNS checker, audit fixes, stubbed-checkout pricing, 20 content pages, post drafts, go-live checklist) and Renewal Sentinel (notification engine, RelayFlow dispatch adapter with a documented contract, calm 30/7/1-day templates with rendered previews, an end-to-end dry-run integration test, and a doc-sync pass that fixed the stale counts and marketing copy). Nothing merged, nothing deployed, nothing sent.

**Runs today:** Yes — `npm run dev` after a one-time local DB migration; the full product works with zero credentials (mock provider + dry-run defaults). Verify suite green (typecheck, lint, 192 tests, build) plus 11 e2e. Production still ships purchase-disabled and dry-run; the notice loop additionally ships behind its own kill switch in dry-run dispatch mode.

**Top 3 gaps (docs vs code):**
1. Renewal Sentinel is built and proven end to end but dark: dispatch defaults to dry-run behind a kill switch, and going live needs the counterpart internal-send endpoint on RelayFlow's side (the contract is written and paste-ready) plus a deliberate two-variable flip. The pricing page's retention promise now has code behind it, but no customer has seen an email.
2. The launch is parked one approval away: `launch-kit` contains the entire go-live kit with a checklist scripted to about 25 minutes, but stays unmerged until the owner signs off on the pricing default, the competitor-claim citations, and the post drafts.
3. The domain's public contact mailbox named on the privacy page still can't receive mail — wiring it up is a five-minute checklist step that also feeds the notice loop's reply path.

**Highest-leverage next move:** Approve and run the launch checklist (merge, migrate, deploy — under 30 minutes); in parallel, build RelayFlow's side of the documented dispatch contract so Renewal Sentinel can leave dry-run and the first retention email becomes real.

---

## EVERYTHING ELSE

**KnwoeldgeSquaredClaude (K² / KnowledgeSquared)** — Next.js 15 + Supabase web app that translates research papers into plain language ("Science, translated"), with a versioned-prompt LLM pipeline; last commit 2026-08-03, runs with setup, but the whole calm-redesign sits unmerged on `feat/calm-redesign` amid ship-in-progress docs.
Next: run its own definition-of-done (typecheck, tests, e2e, seed), then merge or kill the branch.

**MeditationApp (Sember)** — Offline meditation app: Tauri 2 + React desktop plus installable PWA, pre-rendered neural-TTS audio, no accounts, no telemetry; shipping, last commit 2026-08-12. Known live issue: re-rendered audio never reaches returning web clients until the service-worker cache name is bumped.
Next: wire the cache-name bump into the audio-deploy step; leave the deliberately frozen internal identifiers alone.

**Personal Note Taker (DailyReflect)** — Electron daily companion (one markdown file per day, hand-of-five todos with carry-forward, pomodoro widget, ceremonies) at v9.17; actively shipped, stable, runs with plain `npm start`.
Next: maintenance mode — split the single giant design doc and confirm backup rotation stays healthy.

**ThreadWork** — Electron + React + SQLite local-first control plane that imports ChatGPT/Claude export archives and reconstructs projects (decisions, open loops, delegation to a worker or the Claude API); youngest project (one day of git history), runs today.
Next: dogfood one real export ZIP end to end (import → reconstruct → confirm) before adding features.

**KanBanBoard** — Zero-dependency Python local kanban (markdown card files are the source of truth) that doubles as the K² product + marketing task board; complete and stable since June, runs with `python board.py`.
Next: use it, don't develop it.

**LeagueClimbOS** — First-generation League-coaching overlay dashboard (Node + React + Electron), idle since mid-July and superseded by the compliance-hardened rewrite in LeagueClimber; its old self-contained installer was built for personal use only and must never be shared.
Next: confirm retirement in favor of LeagueClimber and archive.

**LeagueClimber (RANK ONE)** — Compliance-first League coaching monorepo (Fastify API, Tauri 2 overlay, web simulator, policy/analytics packages); runs in mock mode today, but every headline differentiator ships disabled behind feature flags awaiting written platform approval.
Next: run its verify + compliance suites, then decide — pursue approval or ship the fallback experience as v1.

**PrincipleFirstJobber** — Tauri 2 + SvelteKit + SQLite/Drizzle job-search desktop app with AI-assisted tooling; last touched 2026-05-19, runs with setup, but the README is still scaffold boilerplate so actual scope is undocumented.
Next: skim the routes and smoke-test to establish what's actually built.

**brand-os** — Personal branding/positioning doc system (strategy boards, scorecards, launch runbook) whose produced site launched 2026-08-11; not an app, and its audit flags private ops actions still owed.
Next: clear its own flagged security items; keep the audit catalog private.

**buzz-bridge** — Working Node bridge that runs five Claude-backed agents as members of a Nostr-based team-chat workspace (mention-gated, loop-guarded, daily reply caps); tested 5/5 on 2026-07-31, runs with setup.
Next: v1 — attach per-charter tools and harden agent identity storage into the OS credential store.

**voice-inbox** — Drop-audio-in-folder voice capture: a batch script feeds a local whisper-based transcriber, producing text beside each recording for a manual weekly sweep; runs if that transcriber app is installed.
Next: script the currently-manual "route transcripts by content" step.

**OWP-EMAIL-V2** — Documentation/deliverables bundle for a nonprofit's email-marketing rebuild (migration specs, an HTML email template, a carrier-registration resubmission package, onboarding decks); not an app, last touched 2026-06-30.
Next: the blockers are all external/ops (carrier registration, ESP automation-tier ceiling, missing email-auth DNS records, survey routing) — execute that checklist; nothing to build here.

**OWP-Email-Marketing** — Earlier planning stage of the same effort: journey diagrams, audit/dedupe/migration gameplans, plus raw audience exports (real-person data that must never leave this machine); last touched 2026-05-13.
Next: fold decisions into V2 and relocate the personal-data exports out of any synced or publishable path.

**_harvest-2026** — Private ops working directory: command-center dashboards, mission log, portfolio dossier, dated harvest notes, safe-to-delete lists, ~11 project sub-buckets; not an app.
Next: leave as-is; when cleaning, act on its own safe-to-delete lists.

**_to_delete-2026-07-30** — Staging folder for a pending delete ritual (retired project copies).
Next: execute the deletion pass already queued in the mission log.

---

## NEW BUILDS WORTH STARTING

**1. Renewal Sentinel — the SpargoDomains notification loop, sent through RelayFlow's rails.** Both active products are one build apart from each other's missing half: SpargoDomains has a nightly cron reconciler and portfolio-health data but no way to email anyone; RelayFlow has production-proven compliant sending (suppression, signed unsubscribe, send log) but no recurring real-world sender to justify it. A small Worker-to-RelayFlow hook that turns "domain expires in 30/7/1 days" into a compliant transactional email closes SpargoDomains' only named revenue blocker and gives RelayFlow its first standing production workload. Effort: ~12–18 hours.

**2. Voice → Desk router.** DailyReflect already has THE INBOX: a single drainable file where a line becomes a note, `[]` a todo, `.` a kept journal entry, with tag filing — and voice-inbox already produces transcripts beside each recording. The missing piece is a ~100-line script (plus one Claude classification call per transcript) that reads new transcripts and appends correctly-shaped lines to that inbox file. Thoughts spoken in the car land on the desk, classified, with zero new UI. Effort: ~6–10 hours.

**3. Buzz fleet v1 — give the five agents hands.** The bridge is built and tested (five chartered Claude agents in the team-chat workspace, mention-gated, loop-guarded, capped); v0 is deliberately conversation-only. v1 attaches each charter's actual tools (file access for the ops agent, project lookups for the product agents) and hardens agent identity storage into Windows Credential Manager — converting a demo into the staffed HQ the standing missions already assume. Effort: ~15–25 hours.

**4. K² launch sequence as RelayFlow's first real workflow.** Largely realized as of 2026-08-24: the sequence runner now exists and ships with the six-step K² welcome flow seeded, rehearsable, and dry-run-verified end to end. What remains of this idea is the owner provisioning pass, the approved welcome copy, and — longer term — the bridge that lets compiled canvas workflows (branches, wait-for-event) feed the runner. Effort remaining: provisioning is under an hour; the canvas bridge is its own project.

**5. HQ dashboard that reads this file.** Realized 2026-08-23: built as `hq-dashboard/` in this repo and served by GitHub Pages — see the DASHBOARD section below. Nothing remains of this idea except using it.

---

## DASHBOARD

**What it is:** A live rendering of this file — one self-contained static page (`hq-dashboard/index.html`, no build step, no backend) that fetches the raw HQ-STATE.md on open and on demand, so the current state is readable from any device without cloning anything.

**Where:** https://spartangomez.github.io/hq-state/hq-dashboard/ (GitHub Pages, enabled 2026-08-23 from the CLI, serving `main` root; the page itself reads only the raw public URL of this file).

**How it renders:** ACTIVE as cards up top (top gaps, highest-leverage next move, the rest folded away), EVERYTHING ELSE as a compact table, NEW BUILDS as a numbered list, staleness color-coded by last-commit age (green under 7 days, amber under 30, red past 30). Sections this file grows later render as plain markdown rather than breaking, and a fetch failure falls back to the viewer's last cached copy — so regenerating this file per the standing rule is the only maintenance the dashboard needs. Build record: `hq-dashboard/STATUS.md`.
