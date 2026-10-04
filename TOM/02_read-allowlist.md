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

## Exec exception (install only, Menu 1.1)

| # | Package (pinned) | Access | Purpose |
|---|------------------|--------|---------|
| E1 | PyPI `astra-pipeline[<extras>]` where `<extras>` subset {graxpert, astro, astroalign} | exec via Menu 1.1 ONLY: pinned `<astra_python> -m pip install [--upgrade] "astra-pipeline[<extras>]"` after explicit user go + env query; mandatory `astra --version` after | install/update ASTRA only; forbidden: other packages, `dev` extras, uninstall, --force/--break-system-packages/--target/--prefix/--user, conda, silent retries; violation = STOPP + report |

A1-A6 stay read-only. E1-E3 are the SOLE exec entries and do NOT extend to Menu 7.1 (plugins) or any other package/manager.

## Exec exception (interpreter provisioning, Menu 1.1 only)

| # | Command (exact) | Access | Purpose |
|---|-----------------|--------|---------|
| E2 | `python --version`, `python -m pip --version`, `<astra_python> -m pip --version` | exec via Menu 1.1 ONLY, read-only diagnostics | env query before any venv/pip; `python` missing or <3.11 = STOPP + python.org guidance, never auto-install |
| E3 | `python -m venv "<venv_path>"` | exec via Menu 1.1 ONLY after explicit user go + EMPTY-dir + type-check (ONLY `<LYRA_HOME>/venvs/<name>` or user-approved EMPTY dir; never `<CAPTURE_ROOT>`/`<DARKS_LIBRARY>`/`<ASTRA_HOME>`/`C:\` root/`Lights`/`Darks`; always quoted) | interpreter provisioning; violation = STOPP + report |

## Onboarding rule

`<ASTRA_HOME>` defaults to EMPTY — Lyra initially knows neither whether
astra is installed nor where it lives. First run asks once: astra
installed? Verify via `astra --version`, record the location; not
installed? Guide the install, then record; or take a user-provided path.
No guessing, no silent fallback.
