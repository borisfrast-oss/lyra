# Template: pipeline-report.md

> One file = one run / one evaluation. EN-SSOT. Proposed by stella 2026-10-03.
> Fixed header + fixed sections; free text only in Notes.
> Honesty rules apply (no misleading sharpness metrics; elongation gate
> before registration tuning).

## Header (mandatory)

| field | value |
|-------|-------|
| target | _exact capture folder name_ |
| type | _handbook chapter 05–16_ |
| date / version | _YYYY-MM-DD / vN_ |
| preset-source | _handbook chapter (05–16) / stella-proposal / lyra-report + date_ |
| preflight | _pass / fail + date_ |
| evidence | _run log / generated-path + file mtimes_ |

## Sections

### 1. Input evidence

_Run inputs: paths + file mtimes. No evidence, no claims._

### 2. Runtime / plausibility

_Duration, timeout class, plausibility verdict
(e.g. 2–3s "success" = anomaly → diagnose, never compensate)._

### 3. Quality findings

_Elongation check first; honest metrics only._

### 4. CLI suggestion (existing flags only)

_Suggested next CLI flags + parameter origin
(stella-proposal vs. lyra-report + timestamp)._

### 5. Notes (free)

_Anything else._
