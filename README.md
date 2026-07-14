# 🌙 AI Forge Ink

_AI artifacts for visual fiction — worldbuilding, characters, dialogue, and image generation._

## Description

A visual fiction toolkit: build worlds, forge characters with emotional depth and memory, stage dialogue and scenes, analyze comic pages, and generate image prompts. 12 specialized skills organized in 3 families, designed for Claude Code.

## Skills

### BD — Worldbuilding & Characters

| Skill          | Role                                                                      |
| -------------- | ------------------------------------------------------------------------- |
| `bd-world`     | World bible builder — universes, timelines, worldbuilding gaps            |
| `bd-character` | Character forge — complete skill directories with snapshots and portraits |
| `bd-emotions`  | Emotional profiler — builds and analyzes character emotional profiles     |
| `bd-memory`    | Memory recorder — tracks how characters remember and distort past events  |
| `bd-relation`  | Relation builder — deep bidirectional relation sheets between characters  |
| `bd-supp-cast` | Supporting cast — lightweight fiches for secondary characters             |
| `bd-loader`    | Context loader — surgically loads the right bd-* data for a scene          |

### Puppet — Character Embodiment & Fiction

| Skill | Role |
| --- | --- |
| `puppet-play` | Collaborative fiction — roleplay with NPCs, character embodiment |
| `puppet-cast` | Characters interact, react, argue — author directs from outside (prose or dialogue) |
| `puppet-analyze` | Multi-focal literary analysis — 11 reading agents, 3 orbits, 4 macro-focales |

### IT — Image & Analysis Tools

| Skill        | Role                                                                                         |
| ------------ | -------------------------------------------------------------------------------------------- |
| `it-scans`   | Scan analyzer — extracts script, dialogue, scenes from comic/manga/BD pages                  |
| `it-prompts` | Prompt generator — translates narrative content into image prompts (NovelAI, Midjourney, SD) |

**12 skills** — 7 worldbuilding/characters, 3 puppet/fiction, 2 image tools

## Structure

```
skills/          # Skills (SKILL.md + references/)
agents/          # Agents (.md) and symlinks to skills/*/agents/
claudeai/        # Zips ready for claude.ai import
.claude/         # Config, hooks, symlinks
```

## Claude.ai Export

Pre-built zips in `claudeai/` can be imported directly into claude.ai projects.

Rebuild after any skill modification:

```bash
.claude/scripts/build-claudeai.sh            # all zips
.claude/scripts/build-claudeai.sh bd-world    # single zip
```
