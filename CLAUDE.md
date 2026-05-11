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
policy" for trigger criteria.

## Canonical sources (cite, don't restate)

Until extractions actually happen, the canonical home for conventions
and primitives is `coderef/ComfyUI-AudioLoopHelper/`. Read from there
rather than copying:

- `CLAUDE.md` (root) — turn-1 rules; layered model of rules-as-code →
  wiki → CLAUDE.md → findings ledger
- `.claude/CLAUDE.md` — CLAUDE.md governance (200-line budget, rule
  lifecycle, capture-then-review, public/private surface routing)
- `scripts/CLAUDE.md` — apply-script + audit-pair conventions, F-pair
  convention, layout-helper patterns
- `docs/reference/_atomic_note_template.md` — wiki shape for atomic notes
- `docs/reference/f_pair_convention.md` — paired apply-script +
  audit-check protocol
- `internal/design/sister_repo_taxonomy.md` — fork vs umbrella decision;
  bootstrap procedure
- `internal/design/extraction_candidates.md` — what's currently extractable
  and the coupling cost
- `.claude/skills/cross-repo-handoff/` — bilateral memo channel pattern
  (gitignored in the sister; presence not guaranteed on every clone)

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
├── README.md                     ← GitHub-facing
├── CLAUDE.md                     ← this file
├── LICENSE
├── .gitignore
├── coderef/                      ← gitignored; symlinks to sister repos
│   └── ComfyUI-AudioLoopHelper/  ← canonical source for now
└── internal/                     ← gitignored; session logs + drafts
    └── log/
```

Future additions land only when their extraction trigger has fired:

- `pyproject.toml` — when first generic Python module extracts
- `src/<namespace>/` — same
- `.claude/agents/`, `.claude/skills/`, `.claude/hooks/` — when a pattern
  in sibling `.claude/` has a second consumer
- `docs/` — when a sister-repo doc is promoted (becomes canonical here)
- `tests/` — when first generic Python module extracts

## Cross-repo coordination

Bilateral memo channel pattern: see
`coderef/ComfyUI-AudioLoopHelper/.claude/skills/cross-repo-handoff/SKILL.md`.
Not wired up for this repo yet; bootstrap when first cross-session work
between comfy-workbench and a sibling repo needs synchronization.

## Documentation conventions

Inherited from `coderef/ComfyUI-AudioLoopHelper/CLAUDE.md` §
"Documentation conventions" and the atomic-note template. Last-updated
date at top; lowercase filenames with underscores; repo-relative
pointers; `internal/` gitignored; session logs at
`internal/log/log_YYYY-MM-DD.md`.

## Path privacy

Same rules as the sister repo. See
`coderef/ComfyUI-AudioLoopHelper/.claude/CLAUDE.md` § "Privacy" for the
canonical rule and `coderef/ComfyUI-AudioLoopHelper/CLAUDE.md` "Privacy"
section for the project-level enforcement. Install `path-privacy` plugin
hooks per-clone via the plugin's `install-git-hooks.sh`. Suggestion
config (if used) goes in `.path-privacy.local.json` (gitignored).
