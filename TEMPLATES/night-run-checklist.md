# Template: night-run-checklist.md

> Pre-flight to tick off before every run. EN-SSOT.
> Proposed by stella 2026-10-03. Abort on first STOPP — never compensate.

## Header (mandatory)

| field | value |
|-------|-------|
| target | _exact capture folder name_ |
| type | _handbook chapter 05–16_ |
| date / version | _YYYY-MM-DD / vN_ |
| preset-source | _handbook chapter (05–16) / stella-proposal / lyra-report + date_ |
| preflight | _pass / fail + date_ |
| evidence | _check log reference_ |

## Checklist

- [ ] Target folder exists exactly (no guessing, no creating) — else STOPP
- [ ] `lights\` present and matches the shot-plan series — else STOPP
- [ ] No `mkdir` in either root (ghost folders forbidden in both)
- [ ] `<CAPTURE_ROOT>` exists (mandatory capture basis from lyra config) — else STOPP
- [ ] `<DARKS_LIBRARY>` exists — ONLY when non-EMPTY (optional second root) — else STOPP
- [ ] Required darks present (pointer per shot-plan) — else STOPP
- [ ] Disk space + pipeline_timeout sane (from config, default 10 hours)
- [ ] Log destination set (lyra DATA, never the capture folder)

_Result: all ticked = GO. First STOPP = diagnose + report, never compensate._
