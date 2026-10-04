# DATA — Registry (runtime index, live)

> Which live lists/plans/reports exist at runtime.
> **In the repo only this REGISTRY.md exists.**
> Live instances are created by Lyra at runtime in the user's install directory
> (`<LYRA_HOME>/DATA/`) on first use — templates come from `TEMPLATES/`.

| Entry | Source | Runtime Location | State |
|-------|--------|------------------|-------|
| config | `TEMPLATES/config.md` | `<LYRA_HOME>/DATA/config.md` | created on first onboarding if missing (both paths: `capture_root` → `<CAPTURE_ROOT>`, `darks_library` → `<DARKS_LIBRARY>`, default EMPTY); session-start config check per TOM/03 §3.5 |
| target-list | `TEMPLATES/target-list-entry.md` | `<LYRA_HOME>/DATA/target-list.md` | created on first entry if missing |
| shot-plan | `TEMPLATES/shot-plan.md` | `<LYRA_HOME>/DATA/shot-plan.md` | created on first plan if missing |
| pipeline-report | `TEMPLATES/pipeline-report.md` | `<LYRA_HOME>/DATA/pipeline-report.md` | created on first evaluated run if missing |
| config field `astra_python` (+ `astra_extras`) | `TEMPLATES/config.md` | `<LYRA_HOME>/DATA/config.md` DELTA | recorded after successful venv + `astra --version` (1.12.1 proof); Env-Wechsel only with new user go |

> **User upgrade path:** new Lyra version copied over existing install →
> `<LYRA_HOME>/DATA/` already exists with user data → Lyra uses existing
> files, never overwrites. Template updates only apply to *new* files.