# comfy-workbench — Claude instructions

Last updated: 2026-05-11

This repo is the **companion umbrella** in the taxonomy at
`coderef/ComfyUI-AudioLoopHelper/internal/design/sister_repo_taxonomy.md`.
Its content shape is a meta-harness: Claude Code conventions, agents,
skills, hooks, templates, CLAUDE.md governance patterns, apply-script +
paired-audit-check protocol, cross-repo memo channels, and the small
amount of generic Python that earns shared-code status across ComfyUI
custom-node repos.

## Status

Bootstrap phase — repo is near-empty. See `README.md` § "Extraction
policy" for trigger criteria and § "Roadmap" for likely first extractions.

## Canonical sources (cite, don't restate)

Until extractions actually happen, the canonical home for conventions
and primitives is `coderef/ComfyUI-AudioLoopHelper/`. Read from there
rather than copying.

### CLAUDE.md governance + conventions
- `CLAUDE.md` (root) — turn-1 rules; layered model of rules-as-code →
  wiki → CLAUDE.md → findings ledger
- `.claude/CLAUDE.md` — CLAUDE.md governance (200-line budget, rule
  lifecycle, capture-then-review, public/private surface routing)
- `scripts/CLAUDE.md` — apply-script + audit-pair conventions, F-pair
  convention, layout-helper patterns, full script inventory
- `tests/CLAUDE.md` — pytest invocation, AST patterns, fakes hierarchy

### Wiki + templates
- `docs/reference/_atomic_note_template.md` — wiki shape for atomic notes
- `docs/reference/f_pair_convention.md` — paired apply-script +
  audit-check protocol
- `docs/reference/debug_tools.md` — debug-tool + apply-script inventory;
  F-check ID index with remediation pointers
- `docs/reference/environment.md` — env-var registry
- `scripts/templates/` — apply-script scaffolds (idempotence,
  `--revert`, `--dry-run`, `require_nodes` pre-flight)

### Sister-repo design docs
- `internal/design/sister_repo_taxonomy.md` — fork vs umbrella decision;
  bootstrap procedure; promotion path
- `internal/design/extraction_candidates.md` — what's currently extractable
  and the coupling cost

### Cross-repo coordination
- `.claude/skills/cross-repo-handoff/SKILL.md` — bilateral memo channel
  pattern (sage-fork variant; canonical reference implementation)
  *(gitignored in the sister; presence not guaranteed on every clone)*

### Skills worth knowing
- `.claude/skills/validate-structural-refactor/` — pre-refactor agent
  dispatch (canonical-home map, rule classifier, subtree density)
- Marketplace plugin: `claude-md-improver` (audit + improve CLAUDE.md
  files; quarterly cadence recommended)

## Working in this repo

1. **Read before adding.** Before introducing a new convention here,
   check whether the canonical sister repo already has it. If yes, cite;
   don't restate.
2. **Promote, don't duplicate.** When a pattern in the sister repo has
   genuinely earned cross-workload status (third consumer materializes),
   *move* the canonical content here and replace the sister-repo
   original with a one-line pointer back. Restating is the failure mode.
3. **Atomic-note shape for new content.** Follow
   `coderef/ComfyUI-AudioLoopHelper/docs/reference/_atomic_note_template.md`.

## Repo layout (current)

```
comfy-workbench/
├── README.md                      ← GitHub-facing
├── CLAUDE.md                      ← this file
├── LICENSE
├── .gitignore
├── .claude/
│   ├── settings.json              ← minimal; hooks empty
│   ├── agents/                    ← scaffolded; empty
│   ├── skills/
│   │   └── cross-repo-handoff-audio-loop-helper/
│   │       └── SKILL.md           ← placeholder; not wired up
│   └── hooks/                     ← scaffolded; empty
├── docs/
│   ├── reference/                 ← scaffolded; empty
│   └── guides/                    ← scaffolded; empty
├── coderef/                       ← gitignored; symlinks to sister repos
│   └── ComfyUI-AudioLoopHelper/   ← canonical source for now
└── internal/                      ← gitignored; session logs + drafts
    └── log/
```

Empty subdirs carry `.gitkeep` markers so the structure persists across
clones. Future content lands only when its extraction trigger has fired:

- `pyproject.toml` / `src/<namespace>/` / `tests/` — when first generic
  Python module extracts
- `.claude/agents/*.md` — when an agent pattern from a sibling has a
  second consumer
- `.claude/skills/*/SKILL.md` (beyond the memo channel) — when a skill
  pattern from a sibling has a second consumer
- `.claude/hooks/*` — when a hook pattern from a sibling has a second
  consumer
- `docs/reference/*.md` — when a sister-repo doc is promoted to canonical
  here (sister-repo original becomes a one-line pointer back)

## Cross-repo coordination

The bilateral memo channel pattern lives at
`.claude/skills/cross-repo-handoff-audio-loop-helper/SKILL.md` (currently
a placeholder). The canonical reference implementation is in the sister
at `coderef/ComfyUI-AudioLoopHelper/.claude/skills/cross-repo-handoff/`
(gitignored; presence not guaranteed). Wire up the channel — including
the SessionStart hook that fires on inbox mtime — when the first
cross-session work between comfy-workbench and AudioLoopHelper claude
needs synchronization.

Per the taxonomy doc § step 8: default is **clone-per-sister** until ≥3
sisters justify parametrization. The directory name carries the sister:
`cross-repo-handoff-audio-loop-helper`, `cross-repo-handoff-<next>`,
etc.

## Documentation conventions

Inherited from `coderef/ComfyUI-AudioLoopHelper/CLAUDE.md` §
"Documentation conventions" and the atomic-note template. Last-updated
date at top; lowercase filenames with underscores; repo-relative
pointers; `internal/` gitignored; session logs at
`internal/log/log_YYYY-MM-DD.md`.

## Path privacy

Same rules as the sister repo. The `path-privacy` plugin's pre-commit
and commit-msg hooks are installed and hard-block any committed content
that references paths outside the repo root. Canonical rule:
`coderef/ComfyUI-AudioLoopHelper/.claude/CLAUDE.md` § "Privacy".
Suggestion config (if used) goes in `.path-privacy.local.json`
(gitignored).
