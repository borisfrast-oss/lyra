# Lyra — Concept (consolidated 2026-10-03, decisions F1–F5 same day)

> Status: draft. SSOT for the Lyra runtime Knowledge Base lives in this repo.
> Build material (project/plan/backlog for building Lyra) is intentionally
> NOT maintained — no SDLC, text work only.
> Stella review 2026-10-03 (consumed, file removed).
> Handbook count fixed same day: 37 chapters + README = 38 files
> (was "36" in stella's profile/index/adapter).

## 1. Goal

Lyra is a companion to astra (not a part of astra, not a stella upgrade):

- Installable as its own wheel (like astra), installed git-less (no `.git`
  at runtime).
- Installs astra, performs configuration (where astra lives, where the
  capture data lives — actual astra paths stay configured in astra itself).
- Keeps ONE central shot-plan / target-list / pipeline-report + log
  (central = in Lyra's DATA, not one file per capture folder).
- Structured menu along the astra CLI function groups + extras
  (config, reports, target-list, shot-plan, ...).
- Analyses runs and results, suggests optimal CLI parameters.
- Uses EXCLUSIVELY currently available astra CLI functions for the pipeline.
- Changes NOTHING about the TOM (forbidden, read-only).
- Multilingual behaviour: profile + KB are English (SSOT); templates default
  English; Lyra translates on request (ephemeral output, never DE leaks
  into EN docs).
- Addresses the user by a self-chosen display name (e.g. "Mickey Mouse",
  stored as `display_name`, no privacy topic).

## 2. Name

`lyra` (decided). `nova` rejected: triple collision — npm `nova-ai`
(Claude+OpenCode orchestrator), OpenStack Nova, plus chat confusion
stella/nova (both short female astro names). PyPI/npm uniqueness check
still open before publish.

## 3. Roles (no SDLC)

| Who | What |
|-----|------|
| stella | Concept + TOM content. Direct chat with Boris only; proposals handed directly to leo (no review files). |
| leo | Implementation of the skeleton + contents into `projects/lyra/` (scope exception, direct on Boris' order). No commit without Boris-Go (HR2). |
| remy | Publishing ONLY at the end (own `builds/lyra/release-repo`, own publisher, own gates). Never publishes placeholders. |

No owen/tess/backy/ray/warden in the loop.

## 4. Repositories

- Dev repo: this repository — own Git repo (`git init` 2026-10-03), decoupled
  from any parent monorepo (nested repo ignored at parent level).
  Holds templates + schema + docs.
- Runtime: wheel install without `.git`. DATA instances are writable at
  runtime; TOM stays read-only.
- Remote + initial commit: pending Boris-Go.

## 5. Structure (this repo)

```
lyra/
  CONCEPT.md        — this file
  profile.md        — Lyra's profile (EN, SSOT): Identity / Responsibility /
                      Boundaries / Permissions; holds the TOM-read-only rule
                      + reference to the central REGISTRY
  REGISTRY.md       — THE central registry (root). References DATA/REGISTRY.md
                      (runtime index) + TOM/ (docs) + adapters. No second
                      competing registry.
  TOM/              — Target Operating Model chapters, EN, versioned, read-only:
                      01–06 (numbered, handbook-style; 06 glossary closes
                      the set).
                      Enforcement = profile sentence + adapter text rule
                      (`edit` allowed ONLY for DATA/TEMPLATES) + one guard test
                      (planned).
                      Own TOM/REGISTRY.md (decided). Chapter 01 = user guidance
                      as numbered menu, e.g. 1. install/update ASTRA,
                      2. configure ASTRA, 3. functions along the CLI groups,
                      4. plan captures, 5. view reports (exemplary).
                      NEVER duplicates handbook/manual or anything from astra —
                      only references. Contains an allowlist directory: what
                      Lyra may READ from ASTRA (handbook, manual, CLI.py,
                      config files such as `config.yaml` — everything else is
                      off-limits). Lyra writes NOTHING into astra.
  DATA/             — runtime knowledge, central (not per-folder):
    REGISTRY.md     — runtime index only (which list/plan/report exists, state)
    config.md       — Lyra user config (NOT astra): astra location, data
                      location (pointers), preferred reporting language,
                      user nickname (`display_name`)
    target-list.md  — central target-list incl. suggested pipeline parameters
                      (template in repo, live instance at runtime)
    shot-plan.md    — central shot-plan (template in repo, live at runtime)
    pipeline-report.md — run analysis + parameter suggestions
                      (template in repo, live at runtime)
  TEMPLATES/        — EN template SSOT (proposed by stella 2026-10-03):
                      target-list-entry.md, shot-plan.md, pipeline-report.md,
                      night-run-checklist.md. Fixed header
                      (target|type|date-version|preset-source|preflight|evidence)
                      + fixed sections, free text only in Notes. Translations
                      are the ONE exception allowed to be written here.
  .opencode/agents/lyra.md — thin adapter, reference to `profile.md` only,
                      no expertise inside (Zielbild §4). Current alex content
                      is placeholder, to be healed.
  .claude/agents/lyra.md   — same, Claude flavour. Placeholder, to be healed.
```

## 6. Two KBs (settled)

- **Lyra-Runtime-KB** = this repo (`profile.md` + `REGISTRY.md` + `TOM/` +
  `DATA/`). This is what Lyra works WITH at runtime.
- **Build-Akte** (project/plan/backlog material for building Lyra) = what one
  would work with to BUILD Lyra. NOT maintained (no-SDLC decision).
  No SSOT break: each KB has its owner.

## 7. Rules

- R1: TOM is read-only for Lyra (profile boundary + `edit: deny` + guard test).
- R2: Pipeline only via existing astra CLI functions. No new pipeline code.
- R3: EN is SSOT for profile/KB/TOM/templates. Translations only on request,
  ephemeral.
- R4: Central lists live in Lyra DATA (template versioned, live git-less).
  NO drift danger (decided F2): the installed astra wheel contains NO
  Aufnahmelisten — only stella keeps per-target sheets, and stella is used
  by Boris only. The end user gets Lyra. No master/sync mapping needed.
- R4b (decided F3): astra handbook start parameters are the basis. Lyra stores
  start parameters for repeatable later use on user request or from its own
  better suggestions — origin labelling is irrelevant. The user can always ask
  Lyra for the handbook entry; handbook + manual ship as wiki inside astra.
  Darksets live where configured (user directory at the captures); Lyra does
  nothing with them — unless we find a missing CLI command, then we discuss.
- R4c (decided F4, verification open at install test): runtime DATA lives
  in-install — the wheel writes into `<LYRA_HOME>/DATA` of the KB.
  Rationale: opencode/claude likewise require the folder to be
  opened to read `.opencode/`/`.claude/`. Install test must prove writability.
- R5: `display_name` is user-chosen, stored in Lyra user config. No privacy
  handling beyond that.
- R6: Adapters stay thin (syntax + reference only).
- R7 (decided): Lyra does NOTHING in the user's capture directory — it may
  READ there but never WRITE there. Lyra writes only into `lyra/DATA`.
  Sole exception: `lyra/TEMPLATES/` for translations (rendered output language
  on user request).
- R8 (decided): Lyra contains NO fixed paths and NO references into orion —
  no absolute paths, no foreign-tree paths anywhere. The SOLE place holding
  real paths is `DATA/config.md` (installation paths and user-provided ones:
  `<ASTRA_HOME>`, `<CAPTURE_ROOT>`, `<LYRA_HOME>` resolve from there).

## 8. Status (built 2026-10-03 by leo, inside `lyra/` only)

Built — profile skeleton (frontmatter + R1–R8 + registry refs), central
`REGISTRY.md`, `TOM/REGISTRY.md` + `DATA/REGISTRY.md`, TOM 01 (menu) + 02
(allowlist + onboarding) + 06 (glossary), 4 EN templates, `DATA/config.md`
(empty defaults) + live pointers, both adapters healed (thin, EN).

Open / collected unclear (no speculation made — decisions needed):

1. TOM content detailing (BUILT 2026-10-03: 01 menu, 02 allowlist, 03 DATA
   model, 04 pipeline-use, 05 reporting, 06 glossary — full chapter set):
   chapter 01 user-guidance menu,
   allowlist directory, inaccuracies vs. real CLI groups. Carried forward from
   stella's review (2026-10-03, file removed after incorporation): TOM 04 must
   hold the pre-flight rule (exact target folder + `lights\` exists, else STOPP
   + report, never mkdir; `<CAPTURE_ROOT>` is the only basis), timeout/plausibility
   rules (ECHT 300s family; 2–3s "success" = anomaly → diagnose) and
   file-mtime evidence duty; TOM 05 the honesty rules (no misleading sharpness
   metrics, elongation gate before registration tuning) plus handbook
   REFERENCES not copies (ch22 entry, 04/21 parameters, 05–16 target types,
   27 storage principle: originals untouched, processing creates new files);
   glossary: the darkset pointer (match logic stays stella's / referenced, no silent
   sync) and log separation (Lyra central runtime log vs. stella's working notes).
   Plus (stella Q3): `process --preflight` first (+ `--yes` only with go),
   `--dry-run` duty (organize/process/merge/darks), `--limit` smoke vs. ECHT
   separated, AZ/EQ-mix + Moon-READY (from organize), single-group needs no
   merge, local-darks nuance.
   Leo builds drafts into `TOM/`.
2. Adapter permission (U1, RESOLVED 2026-10-03): `edit: allow` like stella —
   a hard `deny` would leave Lyra unable to write anything (Write alone
   cannot maintain DATA/TEMPLATES). Enforcement via textual boundaries R1/R7
   (guard test DROPPED — stella precedent: text rules suffice; revisit only
   after an actual violation).
3. Machine-readable config format (U2, PARKED until packaging): needed only
   when remy ships (installer/wheel reads it); `DATA/config.md` stays the
   human doc until then.
4. CLI: NO gaps (stella Q2) — no new command needed. `--json` retrofit for
   `darks list/check` + `target show` DROPPED 2026-10-03 (purpose would have
   been robust machine parsing; text parsing suffices) — revisit only if
   parsing actually breaks.
5. PyPI name check (DONE 2026-10-03): plain `lyra` TAKEN since 2011
   (Django time-management app v1.3, owner hylje). DECIDED: `astra-agent`
   (404 = free, analogy to `astra-pipeline`; Boris 2026-10-03). Fallbacks if
   needed: `lyra-astro`, `astra-lyra` (both free). Relevant only if a wheel
   ever ships; repo distribution needs no name.
6. Install verification: NO separate test — onboarding verifies implicitly
   (`astra --version` proves install + location, first DATA write proves
   writability). Covered by TOM 02.
7. Distribution: NO wheel while codeless (pip needs a buildable package;
   repo clone/zip suffices). remy publish only once something shippable
   exists. Remote + tags on Boris-Go.

## 9. Lyra menu (TOM-01 draft, along the astra CLI groups)

> Numbered guidance. Lyra calls ONLY these commands and writes ONLY into its
> own DATA — never files inside astra (except what the official command itself
> writes, e.g. a `target add` template, and only after user confirmation).

```
LYRA
 1  Setup
 1.1  Install / update ASTRA (pip-level, outside the astra CLI)
 1.2  Configure ASTRA (astra init / astra config wizard)
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
      through Lyra without explicit user go)
  8  Lyra
  8.1  My config (display_name, output language, astra/data locations)
  8.2  Maintain target-list / shot-plan
  8.3  View reports
  8.4  Switch output language (render EN template in another language;
       stored exceptionally in TEMPLATES/, see R7)
```

Source of the command surface: `astra/docs/03-cli-reference.md`
(generated from `<ASTRA_HOME>/src/astro_process/cli.py`).

## 10. Read-allowlist (parameterized — NO absolute paths)

> `<ASTRA_HOME>` resolves from lyra `DATA/config.md` (astra location pointer).
> Everything not listed is off-limits. Write access into `<ASTRA_HOME>`: NONE
> (changes only via the official CLI commands above, on user confirmation).

| # | Path (parameterized) | Access | Purpose |
|---|----------------------|--------|---------|
| A1 | `<ASTRA_HOME>/handbook/` | read | Siril workflow SSOT (37 ch. + README, EN); referenced, never copied |
| A2 | astra Manual: `https://github.com/borisfrast-oss/astra/wiki` (remote, GitHub wiki with Handbook + Pipeline Docs menus) | read | user manual; referenced, never copied |
| A3 | `<ASTRA_HOME>/src/astro_process/cli.py` | read | behaviour reference for the menu above |
| A4 | `<ASTRA_HOME>/config.example.yaml` | read | config schema / defaults |
| A5 | `<ASTRA_HOME>/templates/suggested_parameters.yaml` | read | suggestion template |
| A6 | `<ASTRA_HOME>/config.yaml` + environment files | via `astra config*` ONLY | user config: shown/set through the CLI, never edited as files |

Onboarding rule (decided): `<ASTRA_HOME>` defaults to EMPTY — Lyra initially
knows neither whether astra is installed nor where it lives. First run asks
once: astra installed? → verify via `astra --version` on PATH and record the
location; not installed? → guide the install, then record; or the user hands
over a path directly. No guessing, no silent fallback; install test proves
`<LYRA_HOME>/DATA` writability.
