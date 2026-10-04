# TOM 03 — Central DATA Model

> EN-SSOT. Where Lyra keeps what, and who does what with it.
> Templates are versioned; live instances are git-less at runtime.
> **In the repo only `DATA/REGISTRY.md` exists.** Live files are created
> at runtime in `<LYRA_HOME>/DATA/` from `TEMPLATES/`.

## 3.1 Structure

```
DATA/ (repo)
  REGISTRY.md        — runtime index: which list/plan/report exists, state
TEMPLATES/
  config.md          — onboarding config (template)
  target-list-entry.md, shot-plan.md, pipeline-report.md,
  night-run-checklist.md — EN-SSOT, fixed header + fixed sections
```

Runtime (created by Lyra on first use if missing):

```
<LYRA_HOME>/DATA/
  config.md          — user paths + display_name + language
  target-list.md     — live: one entry per target (template §1)
  shot-plan.md       — live: one plan per night (template §2)
  pipeline-report.md — live: one evaluation per run (template §3)
```

Roots (from `config.md`):

- `capture_root` (mandatory): user capture-data root → `<CAPTURE_ROOT>`.
- `darks_library` (optional, default EMPTY): second root for the darks
  library → `<DARKS_LIBRARY>`; EMPTY keeps single-root use
  (backward-compatible).

## 3.2 Template vs. live

- `TEMPLATES/` = versioned schema. Never edited at runtime — except
  translations (R7 exception).
- `DATA/` (repo) = only `REGISTRY.md` (static index).
- `DATA/` (runtime, `<LYRA_HOME>/DATA/`) = live instances, writable,
  created from templates on first use if missing.
- Upgrade-safe: new Lyra version copied over existing install →
  `<LYRA_HOME>/DATA/` already exists with user data → Lyra uses existing
  files, never overwrites. Template updates only apply to *new* files.
- Completeness rule: mandatory template header fields complete or explicit
  `TBD` — never silent gaps. Derive the handbook type (05–16) from the
  target name where unambiguous, else `TBD`; never invent start parameters.
- Field conventions: `preflight` is `pass <date>`, `fail <date>` or `not-run`
  (never bare `TBD` — a check either ran or it did not); `preset-source`
  stays `TBD` until F3 assigns handbook references (no invented values).

## 3.3 Write rules (user-readable R7/R8)

- Lyra READS `capture_root` and (when non-EMPTY) `darks_library`, never
  writes to either (R7, ghost-guard: no `mkdir` in either root).
- Lyra writes ONLY into `DATA/` (runtime), exceptionally into `TEMPLATES/`
  (translations on request).
- No fixed paths anywhere: `<ASTRA_HOME>`, `<CAPTURE_ROOT>`,
  `<DARKS_LIBRARY>`, `<LYRA_HOME>` resolve from
  `<LYRA_HOME>/DATA/config.md`.

## 3.4 Responsibilities (user-facing)

- Lyra acts ONLY on explicit user order (menu choice, install, run).
- Lyra asks: onboarding paths, every STOPP, every `--fix`, every install.
- The user confirms: failed checks, fixes, installs, merges, batch runs.
- Neither overwrites the other: central DATA is Lyra's; captures are the
  user's; astra is astra's (official CLI outputs excepted).

## 3.5 Session-start config check
- At session start, Lyra checks live `<LYRA_HOME>/DATA/config.md` against `TEMPLATES/config.md` by structure (keys/options, few lines). Other templates (target-list, shot-plan, pipeline-report): user may add columns/sections freely, never checked, never reported.
- Missing live `config.md` = first-use onboarding (TOM/01), never drift. `TBD`/`EMPTY` values are legal. User-added keys are ignored, never removed.
- Short hint (1 line in sync, else short DELTA + offer). Writing into `DATA/` on user go is allowed; never touch either root, astra, or `TOM/`.
- Drift never STOPPs; only a missing mandatory field for the ordered command STOPPs.
