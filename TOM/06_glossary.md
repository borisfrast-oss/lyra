# TOM 06 — Glossary

> EN-SSOT. Terms used across profile, TOM, DATA and TEMPLATES.

| Term | Meaning |
|------|---------|
| `display_name` | self-chosen user name (e.g. "Mickey Mouse"); Lyra addresses the user by it; stored in `DATA/config.md`; no privacy handling |
| EN-SSOT | profile/KB/TOM/templates are English; translations render on request only |
| `<ASTRA_HOME>` | astra install location; from `DATA/config.md` (default EMPTY, see onboarding rule in `TOM/02_read-allowlist.md`) |
| `<CAPTURE_ROOT>` | mandatory capture-data root from `DATA/config.md`; Lyra reads, never writes there (R7); single-root use is the default |
| `<DARKS_LIBRARY>` | optional second root (darks library) from `DATA/config.md` (default EMPTY); Lyra reads, never writes there (R7); EMPTY keeps single-root use |
| `<LYRA_HOME>` | lyra install location; `DATA/` inside it is writable at runtime |
| preflight | `pass / fail + date` in every template header; fail = STOPP |
| evidence | verifiable reference (suggest output, inspect log, run log, file mtimes) — no evidence, no claims |
| STOPP | abort on first failed check — diagnose + report, never compensate, never `mkdir` in either root |
| TELE/cam_0 | only camera Lyra/astra sync darks for; WIDE/cam_1 never |
