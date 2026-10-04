# Template: config.md

> Lyra user config (NOT astra config). Created on first onboarding if missing.
> EN-SSOT. Proposed by stella 2026-10-03.

| Key | Default | Meaning |
|-----|---------|---------|
| `astra_home` | `""` (empty) | astra install location → `<ASTRA_HOME>` |
| `capture_root` | `""` (empty) | user capture-data root → `<CAPTURE_ROOT>` (read-only for Lyra, R7) |
| `darks_library` | `""` (empty) | optional darks-library root → `<DARKS_LIBRARY>` (read-only for Lyra, R7; empty = single-root use) |
| `display_name` | `""` (empty) | self-chosen user name Lyra addresses the user by |
| `language` | `en` | preferred reporting language; EN templates render on request |
| `pipeline_timeout` | `36000` (10 hours) | timeout in seconds for pipeline runs (`astra process`); user-configurable at onboarding; set to `0` or `null` for unlimited (overnight runs) |

Machine-readable format (file type/location for the wheel): OPEN —
decided at wheel build, not here.