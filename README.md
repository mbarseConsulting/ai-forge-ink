# 🌙 AI Forge Ink

_AI artifacts for visual fiction — worldbuilding, scan analysis, and image prompt generation._

## Description

A visual fiction toolkit: build and maintain world bibles, analyze comic/manga pages, and generate image prompts for AI illustration tools. 3 specialized skills bridging narrative and visual creation.

## Overview

| Skill        | Role                                                                                                        |
| ------------ | ----------------------------------------------------------------------------------------------------------- |
| `world-ink`  | World bible builder — generates and maintains universe bibles, timelines, character sheets, relation sheets |
| `scan-ink`   | Scan analyzer — extracts script, dialogue, scene descriptions and tags from comic/manga/BD pages            |
| `prompt-ink` | Prompt generator — translates narrative content into image prompts (NovelAI, Midjourney, Stable Diffusion)  |

**3 skills** — 1 worldbuilding, 1 scan analysis, 1 prompt generation

## Usage

### `/world-ink`

Build or extend a world bible — universe, timeline, characters, relations.

- **`--universe` / `--timeline` / `--character` / `--relation`** — guided construction by template
- **`-i` / `--inline`** — write output inline instead of file
- **default** — interrogation: identify gaps, propose structure

---

### `/scan-ink`

Analyze comic/manga/BD scans — extract script, scenes, tags, characters.

- **`--script`** — dialogue + stage directions only
- **`--scene`** — scene description only
- **`--tags`** — categorized tags only
- **`--characters`** — character identification and description
- **default** — full analysis: dialogue + scene + summary

---

### `/prompt-ink`

Generate image prompts from narrative content.

- **`--novelai`** — NovelAI syntax (default)
- **`--midjourney`** — Midjourney syntax
- **`--sd`** — Stable Diffusion syntax
