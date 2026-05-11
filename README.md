# comfy-workbench

Last updated: 2026-05-11

Shared conventions, agents, skills, and templates for Claude Code working
across ComfyUI workload repositories. Apply-script + audit-pair protocol,
atomic-note documentation, CLAUDE.md governance, cross-repo memo channels.

## Status

Bootstrap phase. Repo is intentionally near-empty — content lands when a
second consumer of a pattern materializes in a sibling repo, not on
speculation. See "Extraction policy" below.

## What this is

A **companion umbrella** in the taxonomy at
`coderef/ComfyUI-AudioLoopHelper/internal/design/sister_repo_taxonomy.md`.
Its shape is a meta-harness: mostly `.claude/`-shaped (agents, skills,
hooks) and `docs/`-shaped (conventions, templates, governance), with a
thin layer of truly generic Python utilities where shared code earns its
keep.

What it **is**:

- Cross-workload Claude Code conventions (CLAUDE.md governance, atomic-note
  template, capture-then-review curation, public/private surface routing).
- Apply-script + paired-audit-check protocol as a reusable shape.
- Agent + skill templates that survive across ComfyUI custom-node repos.
- Cross-repo memo channel mechanism (`cross-repo-handoff`).
- Generic ComfyUI workflow-JSON editing primitives, extracted only when a
  second consumer needs them.

What it **is not**:

- ComfyUI custom nodes — those live where ComfyUI scans (sibling
  custom-node repos like `ComfyUI-AudioLoopHelper`).
- Workflow JSON — canonical in the custom-node repo whose nodes the
  workflow depends on.
- Workload-specific apply scripts — those live in their own custom-node
  repos and mutate their own workflow JSON.
- Anything that patches an upstream library's source — that's a sister
  fork (e.g. `sage-fork`), not an umbrella subpackage.

## Extraction policy

Code or content moves here only when **all three** hold:

1. A concrete second consumer exists.
2. The boundary in the source repo is already drawn or one PR away.
3. The umbrella has at least one prior subpackage (don't bootstrap with a
   single uncertain extraction).

Default is "stays in the source repo." See
`coderef/ComfyUI-AudioLoopHelper/internal/design/extraction_candidates.md`
for the current inventory of what's extractable and the coupling cost.

## Roadmap — likely first extractions

Order is by probable-second-consumer demand, not by technical readiness.
Each item is gated on the extraction policy above; listing here is not a
commitment.

1. **Apply-script templates + F-pair convention as documentation.** Any
   new ComfyUI workload that wants this repo's discipline needs these
   from line one. Highest leverage, lowest mechanical cost (copy + cite).
2. **`WorkflowEditor` API split from run-routing.** First workload that
   needs to mutate workflow JSON without inheriting the sister repo's
   per-workload env-var semantics forces the split.
3. **Audit framework + three generic invariants** (`graph_acyclic`,
   `widget_shape`, `link_integrity`). Once two workloads each have their
   own F-pair audits, the framework earns extraction.
4. **Run-artifact routing.** Last — the env-var-name rename is the
   forcing function, and that only matters when two repos compete for
   the same env var.

Full classification + coupling notes:
`coderef/ComfyUI-AudioLoopHelper/internal/design/extraction_candidates.md`.

## Related repos

| Repo | Bucket | Notes |
|---|---|---|
| [`fblissjr/ComfyUI-AudioLoopHelper`](https://github.com/fblissjr/ComfyUI-AudioLoopHelper) | Custom-node repo (LTX 2.3 audio-looped music video). Canonical source for shared patterns until extraction triggers fire. | Sibling custom-node directory. |
| [`fblissjr/SageAttention-ada`](https://github.com/fblissjr/SageAttention-ada) | Sister fork patching an upstream attention library's CUDA kernel. Self-contained; doesn't depend on this repo. | Not a ComfyUI custom-node package — lives outside `custom_nodes/`; referenced via `coderef/sage-fork/` in the sister repo. |
| [`fblissjr/shrug-prompter`](https://github.com/fblissjr/shrug-prompter) | Sibling custom-node repo for LLM/prompt nodes. Independent; composes with other custom-node repos at the ComfyUI graph level. | Sibling custom-node directory. |

## Bootstrap

This repo lives alongside the sibling custom-node repos under the
maintainer's ComfyUI install. It is not a ComfyUI custom-node package —
has no top-level `__init__.py`, registers no `NODE_CLASS_MAPPINGS`, and
ComfyUI skips the directory at startup without warning.

Bootstrap procedure (skeleton, sister symlinks, memo channel wiring):
`coderef/ComfyUI-AudioLoopHelper/internal/design/sister_repo_taxonomy.md`.

## License

See `LICENSE`.
