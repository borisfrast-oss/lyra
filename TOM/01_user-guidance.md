# TOM 01 — User Guidance (numbered menu)

> EN-SSOT. Follows the astra CLI groups (+ lyra extras).
> Source of the command surface: `astra/docs/03-cli-reference.md`
> (generated from `<ASTRA_HOME>/src/astro_process/cli.py`).
> Rule: Lyra calls ONLY these commands and writes ONLY into its own DATA —
> never files inside astra (except what the official command itself writes,
> e.g. a `target add` template, and only after user confirmation).

```
LYRA
 1  Setup
  1.1  Install / update ASTRA (pip-level, outside the astra CLI — ONLY
        pinned `python -m pip install [--upgrade]
        "astra-pipeline[<extras>]" after explicit user go + env query;
        mandatory `astra --version` after; forbidden: other packages,
        uninstall, --force/--break-system-packages, silent retries;
        violation = STOPP + report)
 1.2  Configure ASTRA + Lyra settings
        (astra init / astra config wizard; lyra onboarding asks:
        astra location, capture root, display name, language, pipeline_timeout)
 1.3  Show configuration (astra config show / config get KEY)
 1.4  Set / reset a value (astra config set KEY VALUE / config reset KEY)
 1.5  Environment check (astra doctor — read-only WITHOUT --fix;
       --fix WRITES dirs/config/darks → only with explicit confirm)
 1.6  Download example data (astra download-example)
 1.7  System status (astra status)
 2  Targets
 2.1  List targets (astra target list)
 2.2  Add target (astra target add)
 2.3  Show / update / remove target (astra target show|update|remove)
 2.4  Organize lights (astra organize TARGET --dry-run first, then real run;
       astra organize --all [--dry-run] for all targets, ignores
       _darks/generated/_work/…)
 3  Planning
 3.1  Suggest preset (astra suggest TARGET [--header/--coords/--output/--json]
       — ALWAYS writes suggested.yaml into the target root (overwrite)
       → stored into lyra target-list)
 3.2  Inspect headers (astra inspect TARGET [--json/--eqmode/--frames/--quality])
 4  Darks
 4.1  Sync DwarfLab export (astra darks sync [--dry-run/--source/--dest]
       — TELE/cam_0 only, never WIDE)
 4.2  List library (astra darks list)
 4.3  Check coverage for a target (astra darks check TARGET — local darks/
       vs. library)
 4.4  Import frames (astra darks import PATH --dry-run first)
 5  Processing
 5.1  Process one target (astra process TARGET --from-suggested REQUIRED
       since v1.11 [--preset] [--dry-run] [--limit = smoke] [--resume]
       [--preflight] [--yes only with go] [--keep-working])
 5.2  Process all targets (astra batch [--preset/--dry-run/--limit/data_root]
       — requires suggested.yaml per target)
 5.3  Merge group stacks (astra merge [--method/--weight-by/--merge-filter/
       --dry-run]; needs >=2 groups, single = auto-merged)
 6  Quality & reports
 6.1  Quality check (astra qc <generated-path> [--json/--check-header];
       --all/--latest for target-root)
 6.2  Pipeline report (lyra analysis of the run + suggested next CLI flags)
 7  Plugins
  7.1  List pipeline plugins (astra plugin list — info only, no installs
       through Lyra; the Menu 1.1 pip allowance applies ONLY to 1.1 and
       never here — plugin installs only via official CLI with explicit
       user go, never via pip)
 8  Lyra
 8.1  My config (display_name, output language, astra/data locations)
 8.2  Maintain target-list / shot-plan
 8.3  View reports
 8.4  Switch output language (render EN template in another language;
       stored exceptionally in TEMPLATES/, see R7)
```
