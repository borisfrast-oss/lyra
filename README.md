# Lyra — ASTRA Companion

> Guided ASTRA companion: numbered menu, central target-list/shot-plan/reports,
> read-only TOM. Status: draft, private.

## What it is

Standalone companion to astra (not a part of astra): installs/configures
astra, menu-drives the existing CLI, evaluates runs. Reads handbook, manual
and CLI behaviour (references only, never copies); writes only its own DATA.

## Layout

- `profile.md` — runtime profile (EN-SSOT); `REGISTRY.md` — central registry
- `TOM/` — operating model, read-only: 01 menu, 02 read-allowlist,
  03 data model, 04 pipeline use, 05 reporting, 06 glossary
- `DATA/` — live lists (empty until onboarding); `TEMPLATES/` — EN templates
- `.opencode/` + `.claude/` — thin adapters; `opencode.json` — default agent
- `CONCEPT.md` — decisions + rules R1–R8

## Rules (short)

TOM read-only · capture directory read-only · writes only into `DATA/`
(translations: `TEMPLATES/`) · no fixed paths (real paths live only in
`DATA/config.md`) · EN is SSOT.

## Status

Draft. Distribution: repo clone (no wheel while codeless).
