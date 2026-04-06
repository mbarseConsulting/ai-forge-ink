---
name: {character-name}
description: "{one line — who this character is, not what they do}"
---

# {Character Name}

> Generic orchestrator. This file is identical for every character.
> Character data lives in core/, snapshots/encyclopedia/, and snapshots/writing/.
> This file describes the structure and loading protocol.

---

## Directory structure

```
{character-name}/
  SKILL.md                 # this file (orchestrator, no character data)
  SPEC.md                  # tests only
  index.md                 # snapshot registry
  core/                    # IMMUTABLE — who the character IS
    core.md                #   identity, psychology, behavior, voice baseline
    writing-rules.md       #   always/never/traps/signals (permanent)
  snapshots/               # EVOLVING — who the character BECOMES
    {NNN}/
      encyclopedia/        #   raw data (updated by bd-emotions/relations/memory)
        state.md           #     deltas from core at this point
        emotional-profile.md #   by bd-emotions (if invoked)
        relations/         #     by bd-relation
          {other}.md
        memory/            #     by bd-memory
          narrative/
          somatic/
      writing/             #   compiled from encyclopedia (by --compile)
        voice.md           #     dialogue construction rules
        emotions.md        #     emotional expression rules
        relations.md       #     interaction rules per character
        body.md            #     physicality rules
  meta/                    # OUTSIDE THE WORK
    puppets/               #   puppet-play/cast session outputs
      notebook.md          #     persistent positions
      _staging/            #     unvalidated outputs
```

## Loading protocol

### Step 1 — Identify

Read this file's frontmatter: `name` and `description`.
Read `index.md` to find the current snapshot number. If no index.md, character is at baseline (core only).

### Step 2 — Load for writing (surface)

If `snapshots/{current}/writing/` exists:
1. `writing/voice.md` — dialogue construction rules
2. `writing/emotions.md` — emotional expression rules
3. `writing/relations.md` — interaction rules per character
4. `writing/body.md` — physicality rules
5. `core/writing-rules.md` — permanent guardrails (always load alongside writing/)

This is sufficient for most scenes. writing/ files are the primary consumer interface.

### Step 3 — Load for depth (when needed)

When a scene demands psychological depth, wound architecture, or memory activation:
- `core/core.md` — permanent reference (extract relevant sections)
- `snapshots/{current}/encyclopedia/state.md` — current deltas
- `snapshots/{current}/encyclopedia/emotional-profile.md` — if exists
- `snapshots/{current}/encyclopedia/relations/{other}.md` — raw relation data
- `snapshots/{current}/encyclopedia/memory/` — triggered memories only

### Fallback — no writing/ directory

If writing/ does not exist, the character is in fallback mode:
1. Load `core/core.md` + `core/writing-rules.md`
2. Load `snapshots/{current}/encyclopedia/state.md` if exists
3. Flag: `No compiled writing rules. Run /bd-character --compile for optimized loading.`

### Consumer shortcuts

| Consumer | What to load |
|----------|-------------|
| Quick reference | SKILL.md frontmatter only |
| Scene writing (surface) | writing/ + core/writing-rules.md |
| Scene writing (deep) | writing/ + core/ + encyclopedia/ |
| Character forge/edit | core/ + snapshots/encyclopedia/ (full access) |
| Relation forge | core/core.md + current encyclopedia/ |
| Puppet incarnation | core/ + encyclopedia/ (full stack) |

## Staleness

writing/ files are compiled from encyclopedia/. Each writing/ file header contains the snapshot number it was compiled from. If that number does not match the current snapshot in index.md, writing/ is stale. Recompile with `/bd-character --compile`.

## The three roots contract

| Root | Content | Modified by | When |
|------|---------|-------------|------|
| `core/` | Permanent, immutable | Initial forge only (retcon = fix core, not evolution) | Once |
| `snapshots/` | Per time point: `encyclopedia/` (raw) + `writing/` (compiled) | encyclopedia/ by bd-emotions/relations/memory; writing/ by --compile | Each narrative event |
| `meta/` | Outside the work | puppet-play, puppet-cast, author tools | Live sessions |
