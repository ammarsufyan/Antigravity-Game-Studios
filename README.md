<p align="center">
  <h1 align="center">Antigravity Game Studios</h1>
  <p align="center">
    Describe a game. Antigravity asks a few questions, writes a one-page brief,
    and builds a playable browser game from it.
    <br />
    Then you change it, grow it, and finish it — one step at a time.
  </p>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
  <a href="https://antigravity.google/docs"><img src="https://img.shields.io/badge/built%20for-Google%20Antigravity-4285F4" alt="Built for Google Antigravity"></a>
  <a href="https://github.com/Donchitos/Claude-Code-Game-Studios"><img src="https://img.shields.io/badge/adapted%20from-Claude%20Code%20Game%20Studios-6e5494" alt="Adapted from Claude Code Game Studios"></a>
</p>

> **Upstream Attribution:** This repository is a 100% Native **Google Antigravity** Public Template conversion of [Donchitos/Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios), preserved under the original [MIT License](LICENSE).

---

## Make me a game

Open **Google Antigravity** (App, IDE, or `agy` CLI) in a copy of this repository and describe the game you want:

```text
/prototype a fishing game where the rare fish only bite at dusk
```

1. **A few questions.** One round, picked from the genre: the choices that shape the game, how it should feel, how it looks, how hard it is, and the goal. Each has a sensible default, so "you pick" works.
2. **A one-page brief.** `design/game-brief.md`: your words kept as you typed them, the look, the first minute, the challenge, the features, and what is deferred. You review it and approve before anything is built.
3. **A first build.** A playable browser game in `prototypes/<name>/` that opens with a double-click: every figure drawn, no emoji art, original mechanics, and meaningful challenge.
4. **Checked before handover.** Verified in a browser for runtime errors, responsiveness, visual layout, and brief coverage. The handover summary states what passed, what still needs work, and what was not assessed.

After that:

- **Change it by asking.** Each accepted change becomes a checkpoint. Ask to tune it and it adds a live tweak panel.
- **Share it.** Package a clean copy ready for itch.io or web hosting.
- **Grow it.** Promote the prototype into a structured web project (Vite + TypeScript, external data files, automated tests) or configure **Godot 4**, **Unity**, or **Unreal Engine 5** via `/setup-engine`.
- **Finish it.** Use `/cut` to scope down, polish, and ship.

Already have a browser game? `/prototype --from <path>` brings a copy in so it can be iterated on and grown the same way.

---

## Table of Contents

- [Getting Started](#getting-started)
- [Engines](#engines)
- [Configuration](#configuration)
- [Project Structure](#project-structure)
- [Rules & Subagents](#rules--subagents)
- [Studio Mode](#studio-mode)
- [Design Philosophy](#design-philosophy)
- [Customization](#customization)
- [Platform Support](#platform-support)
- [Attribution & License](#attribution--license)

---

## Getting Started

### Prerequisites

- **Google Antigravity** — [Antigravity App, IDE, or `agy` CLI](https://antigravity.google/docs)
- **[Git](https://git-scm.com/)**
- **Recommended (optional):**
  - **[Node.js](https://nodejs.org/)** — to grow a browser prototype into a Vite + TypeScript web project and run web tests
  - **Chrome, Edge, or Chromium** — for automated browser verification and screenshots
  - **Bash** (built-in on macOS/Linux; optional via Git Bash on Windows) — optional speedup for `.agents/scripts/*.sh` helpers; **not required** on Windows because all skills natively fall back to `read_file`/`edit_file`/`write_file`

### Setup (Windows, macOS, Linux)

1. **Click "Use this template"** on GitHub (`https://github.com/ammarsufyan/Antigravity-Game-Studios`) **or clone directly**:
   ```bash
   git clone https://github.com/ammarsufyan/Antigravity-Game-Studios.git my-game
   cd my-game
   ```

2. **Open the repository root folder in Google Antigravity** (the folder containing `AGENTS.md`, `project.yaml`, and `.agents/`).
   - Antigravity automatically discovers:
     - `AGENTS.md` (root + `design/AGENTS.md`, `docs/AGENTS.md`, `src/AGENTS.md`)
     - **49 subagents** in `.agents/agents/*.md`
     - **78 skills** in `.agents/skills/*/SKILL.md`
     - **14 glob-scoped rules** in `.agents/rules/*.md`

3. **Start building!** Type `/prototype` with your idea, or run `/start` for guided onboarding.

   Other entry points:
   - `/next-step` — recommends the single best next step wherever you are
   - `/brainstorm` — explore game concepts from scratch
   - `/setup-engine godot 4.7` — configure Godot, Unity, Unreal, or Web
   - `/project-stage-detect` — analyze an existing project

---

## Engines

| Engine | `engine.name` | Code root | Notes |
|---|---|---|---|
| **Web** | `Web` | `src/` | Default for a new project. One-shots need no engine; grown games use Vite + TypeScript (optional three.js, Phaser, or PixiJS). |
| **Godot 4** | `Godot` | `src/` | GDScript, C#, or GDExtension |
| **Unity** | `Unity` | `Assets/` | Unity compiles only `Assets/` and `Packages/` |
| **Unreal Engine 5** | `Unreal` | `Source/<Module>/` | C++ and Blueprints |

`/setup-engine` pins your engine version and populates `docs/engine-reference/<engine>/`. Each engine's default directories and commands live in `.agents/engines/engines.tsv` (overridable via `engine.code_root` / `engine.test_root` in `project.yaml`).

---

## Configuration

`project.yaml` at the repo root is the single source of truth for studio settings (`engine`, naming conventions, and `modes`). `/start` sets it up for you.

The primary knob is **`modes.rigor`** (`minimal`, `standard`, or `full`), which fronts six process knobs (`workflow`, `docs.density`, `qa.level`, `story_granularity`, `review_mode`, `team.size`):

- **`minimal`** (default) — light path: one-page brief, playable first, grow one feature at a time.
- **`standard`** — 5 required GDD sections, balanced docs, standard QA evidence, lean review.
- **`full`** — all 8 GDD sections, thorough docs, full QA evidence, full director review.

Personal per-developer overrides (`modes.review_mode`, `team.size`, `modes.automation`) can be stored in a gitignored `project.local.yaml`:

```text
/project-settings                                # view effective config
/project-settings modes.review_mode              # view one setting
/project-settings modes.rigor=full               # write to project.yaml (team-wide)
/project-settings --local modes.review_mode=solo # write to project.local.yaml (personal)
```

Full schema and precedence rules: `.agents/docs/effects-map.md` and `.agents/docs/config-resolution.md`.

---

## Project Structure

```text
AGENTS.md                           # Master Antigravity instructions (auto-discovered)
project.yaml                        # Project settings: engine, modes, goal
.agents/
  agents/                           # 49 native Antigravity subagents (subagent: true, mainAgent: false)
  skills/                           # 78 native Antigravity skills (SKILL.md + references)
  rules/                            # 14 glob-triggered coding & authoring rules (trigger: glob)
  scripts/                          # Cross-platform optional bash helpers + yaml-helper.sh
  genres/                           # Genre sheets and visual guidance used by /prototype
  engines/                          # Engine table (engines.tsv) and web starters
  docs/
    workflow-catalog.yaml           # 7-phase pipeline definition (read by /next-step)
    templates/                      # 62 document templates
prototypes/                         # Playable one-shots, one folder each (isolated from src/)
references/                         # Optional reference images/audio for /prototype
src/                                # Game source code (Godot/Web; Unity -> Assets/, Unreal -> Source/<Module>/)
assets/                             # Art, audio, VFX, shaders, data files
design/                             # Game brief, GDDs, narrative docs, UX specs, level designs
docs/                               # Technical documentation, ADRs, version-pinned engine references
tests/                              # Game test suites (unit, integration, performance, playtest)
tools/                              # Build and pipeline tools
production/                         # Sprint plans, milestones, QA evidence, release tracking
studio-tests/                       # QA framework for testing the studio's own skills & agents
```

### Testing Customizations (`studio-tests/`)

```text
/skill-test static [name]     # structural linter
/skill-test category [name]   # category-specific quality rubric
/skill-test spec [name]       # behavioral spec assertions
/skill-test audit             # coverage report across skills and agents
/skill-improve [name]         # test-fix-retest loop
```

---

## Rules & Subagents

### Glob-Triggered Rules (`.agents/rules/*.md`)

All 14 rules use Antigravity's `trigger: glob` frontmatter so they only enter context when working on matching files (preserving the `always_on` rules budget). Each code rule matches Godot (`src/`), Unity (`Assets/`), and Unreal (`Source/`) layouts:

| Rule File | Matches | Enforces |
|---|---|---|
| `gameplay-code.md` | `src/gameplay/**`, `src/game/**`, Unity/Unreal gameplay | Data-driven values, delta time usage, no UI refs |
| `engine-code.md` | `src/core/**`, Unity/Unreal core | Zero hot-path allocations, thread safety, API stability |
| `ai-code.md` | `src/ai/**`, Unity/Unreal AI | Performance budgets, debuggability, data-driven params |
| `network-code.md` | `src/networking/**`, Unity/Unreal networking | Server-authoritative design, versioned messages, security |
| `ui-code.md` | `src/ui/**`, Unity/Unreal UI | No game state ownership, localization-ready, accessibility |
| `design-docs.md` | `design/gdd/**` | Required GDD sections per `modes.workflow`, formulas, edge cases |
| `narrative.md` | `design/narrative/**` | Lore consistency, character voice, canon levels |
| `data-files.md` | `assets/data/**/*.json`, `data/**/*.json`, Unity/Unreal data | JSON validity, naming conventions, schema rules |
| `shader-code.md` | `assets/shaders/**`, `.gdshader`, `.hlsl`, `.shader`, `.usf`, `.ush` | Naming, perf targets, cross-platform shader rules |
| `scene-files.md` | `.tscn`, `.tres`, `.unity`, `.prefab`, `.asset` | Safe scene/resource editing guidelines |
| `test-standards.md` | `tests/**`, Unity/Unreal test roots | Test naming, determinism, fixtures |
| `prototype-code.md` | `prototypes/**` | `config.js` tuning knobs, seeded RNG, relaxed prototype rules |
| `agent-memory.md` | `.agents/agent-memory/**` | Durable agent working notes discipline |
| `skill-authoring.md` | `.agents/skills/**`, `.agents/agents/**` | Five authoring obligations for skills & gates |

> **Note on Claude Code Hooks:** The 17 Claude Code bash event hooks originally in `.claude/hooks/` and `.claude/settings.json` were intentionally omitted because Antigravity uses a different JSON hook contract (`hooks.json`) and omitting mandatory bash hooks ensures out-of-the-box reliability on Windows, macOS, and Linux. The shared YAML library was preserved at `.agents/scripts/yaml-helper.sh`.

---

## Studio Mode

When a game grows beyond a quick prototype, switch on studio workflows: **49 specialized subagents**, GDDs, ADRs, epics, sprints, phase gates, and `team-*` multi-agent pipelines.

### What's Included

| Category | Count | Location | Description |
|---|---|---|---|
| **Subagents** | 49 | `.agents/agents/*.md` | Directors, department leads, specialists, and Godot/Unity/Unreal engine specialists |
| **Skills** | 78 | `.agents/skills/*/SKILL.md` | 75 core workflow skills + 3 legacy aliases (`/prototype`, `/start`, `/design-system`, `/dev-story`, `/team-*`, etc.) |
| **Rules** | 14 | `.agents/rules/*.md` | Glob-triggered domain rules (plus hierarchical `AGENTS.md` in root, `design/`, `docs/`, `src/`, `studio-tests/`) |
| **Templates** | 62 | `.agents/docs/templates/` | GDDs, UX specs, ADRs, sprint plans, HUD specs, accessibility checklists, and more |

### Studio Hierarchy

```text
Tier 1 — Directors
  creative-director    technical-director    producer

Tier 2 — Department Leads
  game-designer        lead-programmer       art-director
  audio-director       narrative-director    qa-lead
  release-manager      localization-lead

Tier 3 — Specialists
  gameplay-programmer  engine-programmer     ai-programmer
  network-programmer   tools-programmer      ui-programmer
  systems-designer     level-designer        economy-designer
  technical-artist     sound-designer        writer
  world-builder        ux-designer           prototyper
  performance-analyst  devops-engineer       analytics-engineer
  security-engineer    qa-tester             accessibility-specialist
  live-ops-designer    community-manager
```

### Engine Specialists

| Engine | Lead Agent | Sub-Specialists |
|---|---|---|
| **Godot 4** | `godot-specialist` | GDScript, C#, Shaders, GDExtension |
| **Unity** | `unity-specialist` | DOTS/ECS, Shaders/VFX, Addressables, UI Toolkit |
| **Unreal Engine 5** | `unreal-specialist` | GAS, Blueprints, Replication, UMG/CommonUI |

### Available Skills (Invoke via `/skill-name` or Natural Language)

- **Make a Game:** `/prototype` `/cut`
- **Onboarding & Navigation:** `/start` `/next-step` `/project-stage-detect` `/setup-engine` `/adopt` `/project-settings`
- **Game Design:** `/brainstorm` `/map-systems` `/design-system` `/quick-design` `/review-all-gdds` `/propagate-design-change`
- **Art & Assets:** `/art-bible` `/asset-spec` `/asset-audit`
- **UX & Interface:** `/ux-design` `/ux-review`
- **Architecture:** `/create-architecture` `/architecture-decision` `/architecture-review` `/create-control-manifest`
- **Stories & Sprints:** `/create-epics` `/create-stories` `/dev-story` `/sprint-plan` `/sprint-status` `/story-readiness` `/story-done` `/estimate`
- **Reviews & Analysis:** `/design-review` `/code-review` `/balance-check` `/content-audit` `/scope-check` `/perf-profile` `/tech-debt` `/gate-check` `/consistency-check` `/security-audit`
- **QA & Testing:** `/qa-plan` `/smoke-check` `/soak-test` `/regression-suite` `/test-setup` `/test-helpers` `/test-evidence-review` `/test-flakiness` `/skill-test` `/skill-improve`
- **Production:** `/milestone-review` `/retrospective` `/bug-report` `/bug-triage` `/reverse-document` `/playtest-report`
- **Release:** `/release-checklist` `/launch-checklist` `/write-changelog` `/patch-notes` `/hotfix` `/day-one-patch`
- **Creative & Content:** `/vertical-slice` `/onboard` `/localize`
- **Team Orchestration:** `/team-combat` `/team-narrative` `/team-ui` `/team-release` `/team-polish` `/team-audio` `/team-level` `/team-live-ops` `/team-qa`

### Collaborative, Not Autonomous

Every agent follows the **Question -> Options -> Decision -> Draft -> Approval** protocol: nothing is written to your game files without explicit approval (configurable via `modes.automation` in `project.yaml`).

---

## Design Philosophy

- **Playable first** — build something playable before writing mountains of documentation
- **MDA Framework** — Mechanics, Dynamics, Aesthetics analysis
- **Self-Determination Theory** — Autonomy, Competence, Relatedness
- **Flow State Design** — challenge-skill balance
- **Verification-Driven Development** — automated tests for logic + retained screenshots for visual/UI stories

---

## Customization

This repository is a **template** meant to be tailored to your studio:

- Add or remove subagents in `.agents/agents/`
- Edit or add skills in `.agents/skills/`
- Add path-scoped rules in `.agents/rules/`
- Tune `modes.rigor` and engine settings in `project.yaml`

---

## Platform Support

Designed to work cleanly across **Windows, macOS, and Linux**:

- All 49 subagents, 78 skills, 14 glob rules, and `AGENTS.md` files use pure Markdown/YAML and Antigravity's native cross-platform tools (`read_file`, `edit_file`, `write_file`, `run_command`, `ask_question`, `invoke_subagent`, `search_web`).
- No Bash or Python is required on Windows to resolve `project.yaml` or run skills.
- `.gitattributes` enforces LF (`\n`) line endings on `.sh`, `.awk`, `.tsv`, and `.agents/**/*.md` across all operating systems.

---

## Attribution & License

- **Original Project:** [Donchitos/Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) by Donchitos.
- **Antigravity Conversion:** [ammarsufyan/Antigravity-Game-Studios](https://github.com/ammarsufyan/Antigravity-Game-Studios).
- **License:** MIT License. See [LICENSE](LICENSE) for full copyright and permission notice.
