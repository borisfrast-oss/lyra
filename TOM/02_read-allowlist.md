# TOM 02 — Read-Allowlist (parameterized, exhaustive)

> EN-SSOT. `<ASTRA_HOME>` resolves from lyra `DATA/config.md`.
> Everything not listed here is off-limits.
> Write access into `<ASTRA_HOME>`: NONE — changes only via the official
> CLI commands (`TOM/01_user-guidance.md`), and only after user confirmation.

| # | Path (parameterized) | Access | Purpose |
|---|----------------------|--------|---------|
| A1 | `<ASTRA_HOME>/handbook/` | read | Siril workflow SSOT (37 ch. + README, EN); referenced, never copied |
| A2 | astra Manual: `https://github.com/borisfrast-oss/astra/wiki` (remote) | read | user manual (Handbook + Pipeline Docs menus); referenced, never copied |
| A3 | `<ASTRA_HOME>/src/astro_process/cli.py` | read | behaviour reference for the menu |
| A4 | `<ASTRA_HOME>/config.example.yaml` | read | config schema / defaults |
| A5 | `<ASTRA_HOME>/templates/suggested_parameters.yaml` | read | suggestion template |
| A6 | `<ASTRA_HOME>/config.yaml` + environment files | via `astra config*` ONLY | user config: shown/set through the CLI, never edited as files |

## Onboarding rule

`<ASTRA_HOME>` defaults to EMPTY — Lyra initially knows neither whether
astra is installed nor where it lives. First run asks once: astra
installed? Verify via `astra --version`, record the location; not
installed? Guide the install, then record; or take a user-provided path.
No guessing, no silent fallback.
