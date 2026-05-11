---
name: cross-repo-handoff-audio-loop-helper
description: Placeholder for the bilateral memo channel with ComfyUI-AudioLoopHelper claude. Not wired up yet — canonical reference implementation lives at `coderef/ComfyUI-AudioLoopHelper/.claude/skills/cross-repo-handoff/SKILL.md` (sage-fork variant). Clone-and-parameterize this slot when the first cross-session coordination between comfy-workbench and ComfyUI-AudioLoopHelper needs synchronization. Until then, do not dispatch this skill.
---

# cross-repo-handoff-audio-loop-helper (placeholder)

Last updated: 2026-05-11

This file holds the slot for the bilateral memo channel between
comfy-workbench claude and ComfyUI-AudioLoopHelper claude. It is **not
wired up** — the skill body, the inbox/outbox files, and the
SessionStart hook that fires on inbox mtime all need to be authored
before the channel functions.

## Why this exists empty

Per the taxonomy doc at
`coderef/ComfyUI-AudioLoopHelper/internal/design/sister_repo_taxonomy.md`
§ step 8: each sister gets a bilateral memo channel. The default is
**clone-per-sister** (one `cross-repo-handoff-<sister>/` per
relationship) until ≥3 sisters justify abstracting into a parameterized
single skill. comfy-workbench's first sister is ComfyUI-AudioLoopHelper;
this directory reserves the slot using the parametrized naming
convention from day one.

## How to wire it up (when the need arrives)

1. Read the canonical reference implementation:
   `coderef/ComfyUI-AudioLoopHelper/.claude/skills/cross-repo-handoff/SKILL.md`
   (gitignored in the sister; presence not guaranteed on every clone).
2. Clone its body here, rewriting the channel topology table:
   - Inbound (AudioLoopHelper claude → us):
     `internal/AUDIO_LOOP_HELPER_CLAUDE_TO_COMFY_WORKBENCH_CLAUDE_MEMO.md`
   - Outbound (us → AudioLoopHelper claude):
     `coderef/ComfyUI-AudioLoopHelper/internal/COMFY_WORKBENCH_CLAUDE_TO_AUDIO_LOOP_HELPER_CLAUDE_MEMO.md`
3. Rewrite the trigger-phrasing table (e.g. "send memo to AudioLoopHelper
   claude", "AudioLoopHelper claude sent us a memo").
4. Author the SessionStart hook at
   `.claude/hooks/check_memo_inbox.sh` so the inbox notifies on new
   mtime; pattern: the sister's existing hook.
5. Update the matching channel definition on the AudioLoopHelper side
   (it currently only knows about sage-fork; add comfy-workbench as a
   second sister there).
6. Replace this placeholder with the working SKILL.md. Update the
   frontmatter `description:` to remove "Not wired up yet" and add the
   actual trigger phrases.

## Until then

Do not dispatch this skill. If the user invokes a trigger phrase that
would match it ("send a memo to AudioLoopHelper claude" or similar),
reply that the channel is not wired up and propose wiring it per the
steps above.
