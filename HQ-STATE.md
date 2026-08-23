# HQ-STATE

Machine-state snapshot of the Projects workspace. Generated 2026-08-23 by a read-only recon pass; regenerated at the end of every mission so this file always shows current state.
Sanitized for public hosting: no credentials, no env values, no personal or client data — sensitive facts are described by shape, not contents.

---

## ACTIVE

### RelayFlow (dir: SpargoEmailAutomations)

**What it is:** Diagram-first email/SMS automation builder — describe a customer journey in plain English, a deterministic compiler turns it into a canonical workflow you edit on a React Flow canvas, with a real compliance/deliverability sending backend growing underneath the demo.

**Stack:** Next.js 16 (App Router) + React 19 + TypeScript strict, Tailwind v4, React Flow 12 + dagre, Zustand, Zod v4. Supabase (Postgres) for the send-side data with a local fallback. Transactional email provider (Resend SDK) behind a signed inbound webhook; SMS provider SDK; both default to mock. Vercel hosting with a code-level "public surface only" deploy gate. 19 Vitest suites (~138 tests).

**Git:** branch `main`, last commit 2026-08-18 — "Drop the reconcile poll; handle provider-side suppression events."

**Runs today:** Yes — `npm run dev` runs the full builder, AI generation, simulation, and mock sends with zero config. Typecheck clean. Real sending requires env setup and is deliberately single-recipient, suppression-checked, and confirmation-gated; no bulk endpoint exists.

**Top 3 gaps (docs vs code):**
1. README still describes a mock-only demo, but a production compliance backend is shipped and proven: DB schema (2 migrations), signed provider webhook, signed unsubscribe (footer + RFC 8058 one-click), deploy-time public-surface gate, real deliveries verified through a live deployment.
2. The promised "swap the repository for a real DB later" never happened for the core domain — workflows, contacts, automations, and templates are still per-browser localStorage; only opt-out/brand/audit data is server-side.
3. Compliance rails exist but nothing drives them over time: there is no durable sequence runner (queue + scheduler). A 6-step welcome flow with wait-for-event steps exists, seeded as a template, but nothing executes it end to end — sends today are manual, single, confirmation-gated.

**Highest-leverage next move:** Build the durable workflow runner that executes a compiled workflow over real time on top of the already-proven suppression/unsubscribe/send-log rails — that one piece converts compliance plumbing into an actually-automating product.

---

### Mira

**What it is:** A private, Spanish-language "answer machine" PWA for one older adult: she speaks a question or photographs a letter, gets one plain-language card back, and the app remembers her ongoing topics so she never re-explains them.

**Stack:** TypeScript monorepo. Client: Vite + React 19 PWA (7 screens, service worker, strict same-origin CSP). Server: Express 5 + SQLite, SSE streaming, in-process cron (nightly backup, timed purges). Claude models via the official SDK, model-routed (cheap text model + stronger vision/escalation model, env-configurable). Vitest + Playwright (WebKit iPhone + Chromium). Railway hosting via Dockerfile with a persistent volume and healthcheck.

**Git:** branch `master`, last commit 2026-07-30 — "Verification suite, gate runner, and fixes found by running it."

**Runs today:** Yes, immediately, in mock-AI mode (`npm run dev`, mock answers watermarked, no credentials needed). Both typechecks clean; both dists already built. Production boot deliberately refuses to start without proper env setup — runs-with-setup by design, nothing broken. (A worktree branch for the install-day build also exists.)

**Top 3 gaps (docs vs code):**
1. The spec the repo cites is not in the repo: ~98 references to numbered requirements (REQ-001…REQ-020) across 45 files, and four spec docs named in the README, but none of those files exist — requirement coverage can't actually be audited.
2. The release gate has never fully passed: recorded verification run is `overall: incomplete` — 10/12 automated gates green, but the two live-model safety evals (one-question discipline, hostile-letter red-team) never ran, plus 5 manual/on-device gates outstanding.
3. The primary interaction rests on an untested assumption with no built fallback: browser Spanish speech-recognition quality on the target phone is the flagged biggest unknown, and the documented fallback (server-side speech-to-text behind the same interface) is deferred and unimplemented.

**Highest-leverage next move:** Run the two live-model evals to green and do the on-phone dictation test — the only things standing between "verified on a laptop" and "safe to hand to the actual user."

---

### SpargoDomains

**What it is:** A single-user, safety-first domain search-and-purchase tool over the official Cloudflare Registrar API — invent a name, verify live availability and price, register it at cost in your own Cloudflare account — now with a public marketing front door and a credential-free demo.

**Stack:** React 19 + Vite + TypeScript, Tailwind + shadcn-style UI, TanStack Query. Hono API on Cloudflare Workers (one Worker serves SPA + API). Drizzle ORM on Cloudflare D1. Cloudflare Access JWT auth gated to a single admin identity. Money as decimal strings via big.js. Nightly cron reconciler (read-only). ~129 Vitest cases + 11 Playwright tests.

**Git:** branch `main`, last commit 2026-08-17 — "Act on the marketing handoff: hero, screener, and the demo's honest ending."

**Runs today:** Runs with light setup — `npm run dev` after a one-time local DB migration; full product works with zero credentials (mock provider + dry-run defaults). Typecheck clean on all three configs. Production config ships purchase-disabled and dry-run by default.

**Top 3 gaps (docs vs code):**
1. The retention feature the business case is staked on doesn't exist: every planning doc justifies the subscription with renewal/expiry notifications, but there is no notification path, no payments, and the nightly job only reconciles records — renewal risk surfaces passively in-app only.
2. Marketing docs lag the shipped code: the documented hero copy and two-question screener were superseded by the Aug 17 commit (new hero, third screener question, matching schema migration) but the marketing briefs were never updated.
3. Stale test counts and route lists in the README and handoff docs (README claims 66 unit tests; actual ~129 across 17 files; two mounted API route groups missing from the architecture blurb).

**Highest-leverage next move:** Build the renewal/expiry notification loop on top of the existing nightly reconciler and portfolio-health data — the single retention hook every doc names as the reason anyone would pay.

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

**4. K² launch sequence as RelayFlow's first real workflow.** The kanban board already holds a K² marketing track with an email channel, and RelayFlow's whole pitch is "describe the journey, get the automation." Authoring the K² launch/welcome sequence as a RelayFlow workflow makes an in-house product the sequence runner's first customer — the runner (RelayFlow's own top gap) gets built against a real need instead of a hypothetical, and K² gets a launch asset. Effort: ~10–15 hours on top of the runner build.

**5. HQ dashboard that reads this file.** The ops directory already contains hand-built command-center HTML dashboards, and this repo now exposes machine state at a stable raw URL. A single static page that fetches and renders HQ-STATE.md — active projects up top, staleness highlighted by last-commit age — turns the existing dashboard habit into one that is always current and readable from any device, including by the chat-side Claude this file was built for. Effort: ~4–6 hours.
