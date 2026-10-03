# TOM 04 — Pipeline Use (rules)

> EN-SSOT. How Lyra runs the pipeline. Pre-flight first, dry-run duty,
> evidence always. From stella's review 2026-10-03 + Q3 additions.

## 4.1 Pre-flight rule (before EVERY run)

- Exact target folder + `lights\` exist — else STOPP + report.
- `<CAPTURE_ROOT>` is the only basis. No guessing, no creating.
- NEVER `mkdir` in the capture tree (ghost folders forbidden).
- Required darks present (pointer per shot-plan) — else STOPP.
- Disk space + timeout class sane; log destination = lyra DATA.
- First STOPP = diagnose + report, never compensate.
- Run `process --preflight` first; `--yes` (start on pass) ONLY with
  explicit user go.

## 4.2 Dry-run duty

`organize`, `process`, `merge`, `darks` (sync/import): `--dry-run` first,
real run only after review.

## 4.3 Smoke vs. ECHT

`--limit` = smoke testing only, uniformly applied. ECHT runs never carry
a limit. Label every run: smoke or ECHT.

## 4.4 Mixes and special cases (from organize)

- AZ/EQ-mix and filter-mixes: warn BEFORE the run; process only listed series.
- Moon-READY states ride along where organize reports them.
- Single group needs no merge (`merge` requires >= 2 groups).
- Local-darks nuance: `darks check TARGET` compares local `darks/` against
  the library — Lyra reports, manages nothing.

## 4.5 Timeout / plausibility + evidence

- **Pipeline timeout:** configurable per user (`pipeline_timeout` in config; default 10 hours = 36,000 seconds). Onboarding asks once; user can adjust or set unlimited for overnight runs.
- **On timeout abort:** half-generated runs remain in `<target>/generated/` — do NOT delete blindly. Use `astra process --resume` to continue or decide cleanup manually.
- Plausibility: a 2–3s "success" is an anomaly → diagnose, never trust.
- Evidence duty: run inputs as paths + file mtimes. No evidence, no claims.
