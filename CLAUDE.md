# hq-state — working notes

Read HQ-DOCTRINE.md in this repo before any mission; it overrides local habit.

This repo is public. HQ-STATE.md is the machine-state snapshot (regenerated per
the standing rule in HQ-DOCTRINE.md §5); PRODUCTS.md is the ground-truthed
live-surface registry the dashboard's LAUNCHPAD tab renders. `hq-dashboard/`
serves byte-identical copies of BOTH files same-origin for the GitHub Pages
dashboard — every push that touches either file refreshes its dashboard copy in
the same commit. Sanitize before every push — grep for credential-shaped AND
email-shaped strings; facts by shape, never contents.

Standing rule amendment (2026-08-25, launchpad mission): every mission-end push
also refreshes the touched product's PRODUCTS.md block **if its live state
changed** — a deploy, a go-live flip, a new public surface, or a live URL
starting to serve different content all count. Update the block's `checked:`
line with the date and what the live URL actually serves (fetch it; truth beats
intention), keep `shipped:` to the three freshest dated bullets, and keep the
one-line `next:` current. Blocks stay ordered LIVE first, most recently
updated first.
