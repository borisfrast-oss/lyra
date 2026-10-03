# TOM 05 — Reporting and Parameter Guidance (rules)

> EN-SSOT. How Lyra reports runs and suggests parameters.
> From stella's review 2026-10-03 + Q3 additions.

## 5.1 Honesty rules

- No misleading sharpness metrics (no HP-variance figures).
- Elongation gate BEFORE registration tuning — check elongation first.
- Every metric carries its evidence (log + mtimes); without it, no claim.

## 5.2 Handbook references (never copies)

- Entry: decision tree, handbook chapter 22.
- Parameters: chapters 04 + 21.
- Target types: chapters 05–16.
- Storage principle, chapter 27: originals untouched, processing creates
  new files.

## 5.3 Parameter suggestions

- Basis: handbook start parameters (F3); Lyra stores reusable start
  parameters on user request or from its own better suggestions.
- Suggest EXISTING astra CLI flags only (R2).
- Origin labelling not required; the handbook entry stays askable anytime;
  handbook + manual ship as wiki inside astra.

## 5.4 Darkset pointer (no management)

Match logic (exposure/gain/temperature proximity) stays stella's domain
or referenced; Lyra shows the pointer from the shot-plan and manages
nothing. No silent sync.

## 5.5 Log separation

Lyra keeps the central runtime log (DATA + pipeline-report); stella's
working notes stay stella's. Neither overwrites the other.
