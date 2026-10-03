# TOM 03 — Central DATA Model

> EN-SSOT. Where Lyra keeps what, and who does what with it.
> Templates are versioned; live instances are git-less at runtime.

## 3.1 Structure

```
DATA/
  REGISTRY.md        — runtime index: which list/plan/report exists, state
  config.md          — the SOLE place holding real paths (R8); defaults EMPTY
  target-list.md     — live: one entry per target (template §1)
  shot-plan.md       — live: one plan per night (template §2)
  pipeline-report.md — live: one evaluation per run (template §3)
TEMPLATES/
  target-list-entry.md, shot-plan.md, pipeline-report.md,
  night-run-checklist.md — EN-SSOT, fixed header + fixed sections
```

## 3.2 Template vs. live

- `TEMPLATES/` = versioned schema. Never edited at runtime — except
  translations (R7 exception).
- `DATA/` = live instances, writable at runtime (`<LYRA_HOME>/DATA`).
- Empty until used: first target (menu 2.2/3.1), first plan (3.1),
  first evaluated run (6.2).
- Completeness rule: mandatory template header fields complete or explicit
  `TBD` — never silent gaps. Derive the handbook type (05–16) from the
  target name where unambiguous, else `TBD`; never invent start parameters.

## 3.3 Write rules (user-readable R7/R8)

- Lyra READS the capture tree, never writes there.
- Lyra writes ONLY into `DATA/`, exceptionally into `TEMPLATES/`
  (translations on request).
- No fixed paths anywhere: `<ASTRA_HOME>`, `<CAPTURE_ROOT>`, `<LYRA_HOME>`
  resolve from `DATA/config.md`.

## 3.4 Responsibilities (user-facing)

- Lyra acts ONLY on explicit user order (menu choice, install, run).
- Lyra asks: onboarding paths, every STOPP, every `--fix`, every install.
- The user confirms: failed checks, fixes, installs, merges, batch runs.
- Neither overwrites the other: central DATA is Lyra's; captures are the
  user's; astra is astra's (official CLI outputs excepted).
