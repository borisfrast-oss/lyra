# Lyra — Concept (consolidated 2026-10-03, decisions F1–F5 same day)

> Status: draft. SSOT for the Lyra runtime Knowledge Base lives in this repo,
> not in orion. The orion Build-Akte (project.md / plan / backlog) is
> intentionally NOT maintained — no SDLC, text work only.
> Stella review: `orion/_work/stella/lyra-concept-review.md` (2026-10-03).
> Handbook count fixed same day: 37 chapters + README = 38 files
> (was "36" in stella profile/knowledge-index/adapter).

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
| stella | Concept + TOM content. Direct chat Boris ↔ stella only (stella is `task: deny`, no agent interaction). Output = proposals to `_work/stella/`. |
| leo | Implementation of the skeleton + contents into `projects/lyra/` (scope exception, direct on Boris' order). No commit without Boris-Go (HR2). |
| remy | Publishing ONLY at the end (own `builds/lyra/release-repo`, own publisher, own gates). Never publishes placeholders. |

No owen/tess/backy/ray/warden in the loop.

## 4. Repositories

- Dev repo: `this repository` — own Git repo (`git init`
  2026-10-03), decoupled from the `projects/` monorepo via `/lyra/`
  in the parent `.gitignore`. Holds templates + schema + docs.
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
                      01_*.md, 02_*.md, NN_*.md (numbered, handbook-style).
                      Enforcement = profile sentence + adapter `edit: deny`
                      on TOM paths + one guard test (planned).
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
  .opencode/agents/lyra.md — thin adapter, reference to `profile.md` only,
                      no expertise inside (Zielbild §4). Current alex content
                      is placeholder, to be healed.
  .claude/agents/lyra.md   — same, Claude flavour. Placeholder, to be healed.
```

## 6. Two KBs (settled)

- **Lyra-Runtime-KB** = this repo (`profile.md` + `REGISTRY.md` + `TOM/` +
  `DATA/`). This is what Lyra works WITH at runtime.
- **Orion-Build-Akte** (`knowledge-base/projects/lyra/`,
  `knowledge-base/agents/lyra/`) = what we would work with to BUILD Lyra.
  NOT maintained (no-SDLC decision). No SSOT break: each KB has its owner.

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
  in-install — e.g. wheel installed to `<LYRA_HOME>` writes into `<LYRA_HOME>/DATA`
  of the KB. Rationale: opencode/claude likewise require the folder to be
  opened to read `.opencode/`/`.claude/`. Install test must prove writability.
- R5: `display_name` is user-chosen, stored in Lyra user config. No privacy
  handling beyond that.
- R6: Adapters stay thin (syntax + reference only).

## 8. Open points (in order)

1. TOM content detailing (Boris ↔ stella): chapter 01 user-guidance menu,
   allowlist directory, inaccuracies vs. real CLI groups. Stella drafts
   01–05+NN as proposals to `_work/stella/`, leo builds into `TOM/`.
2. Heal both `lyra.md` adapters (de-alex, point at Lyra profile, EN).
3. Profile skeleton (frontmatter `type/scope/role/layer/status` + sections,
   TOM-read-only rule + central REGISTRY reference).
4. ROOT-REGISTRY → DATA-Registry + TOM/REGISTRY wiring.
5. Guard test for TOM-read-only (which TOM paths `edit:deny`, what it protects)
   + darkset/CLI-gap check: pipeline is expected to handle darksets; if a CLI
   command is missing we discuss it (F5).
6. PyPI/npm name check for `lyra`.
7. Install-path verification: prove `<LYRA_HOME>/DATA` writable at runtime.
8. Initial commit + remote (Boris-Go) → much later: remy publish.
