# it-scans — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `it-scans`                                 |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none`                                     |

## Scenarios

### S01 — Extract dialogue and describe scene from comic page

**Intent:** Validate full-page analysis: dialogue extraction with panel attribution and visual action description.

**Context:** Single comic/BD/manga page image provided. No prior context.

**Input:**

```
/it-scans
[comic page image provided]
```

**Expected behavior:**

- [ ] Displays `[SCAN-INK]` tag
- [ ] Reads the image before producing any output
- [ ] Preserves reading order (LTR for comics/BD, RTL for manga)
- [ ] Original language of the text is preserved (no unsolicited translation)

**Expected output:**

- [ ] STRUCTURE: all dialogue extracted with panel attribution (Panel 1, Panel 2, etc.)
- [ ] Distinguishes text types: character dialogue, narration boxes, sound effects
- [ ] CONTAINS: visual action description for each panel

**Anti-patterns (must NOT happen):**

- [ ] Invents dialogue not visible on the page
- [ ] Generates content beyond what the image shows
- [ ] Translates text without being asked

---

### S02 — Identify characters across pages

**Intent:** Validate character identification and visual tracking across multiple pages.

**Context:** Multiple comic page images provided. Some characters recur across pages.

**Input:**

```
/it-scans --characters
[multiple comic page images provided]
```

**Expected behavior:**

- [ ] Identifies recurring characters across pages
- [ ] Notes visual distinguishing features (hair, clothing, build, accessories)
- [ ] Uses character names when visible in dialogue; otherwise uses descriptive labels

**Expected output:**

- [ ] STRUCTURE: character list with panel appearances tracked
- [ ] CONTAINS: distinguishing visual features per character
- [ ] Distinguishes between confirmed identity (named in text) and visual identification

**Anti-patterns (must NOT happen):**

- [ ] Assumes character names without textual evidence
- [ ] Invents backstory or relationships not shown in the images
- [ ] Confuses distinct characters who look similar

---

### S03 — Full page composition description

**Intent:** Validate description of visual storytelling techniques and panel layout.

**Context:** Single comic page image provided. Focus is on layout analysis, not dialogue.

**Input:**

```
/it-scans --layout
[comic page image provided]
```

**Expected behavior:**

- [ ] Identifies visual storytelling techniques (splash pages, bleeds, insets, gutters)
- [ ] Notes panel-to-panel transitions (moment-to-moment, action-to-action, scene-to-scene)

**Expected output:**

- [ ] STRUCTURE: page composition breakdown — panel count, sizes, arrangement
- [ ] CONTAINS: color palette, lighting, and art style choices
- [ ] CONTAINS: pacing assessment conveyed through layout

**Anti-patterns (must NOT happen):**

- [ ] Limits description to dialogue content only
- [ ] Ignores composition and layout in favor of plot summary
- [ ] Uses generic descriptions that could apply to any page

---

## Edge Cases

### E01 — Low quality or illegible scan

**Intent:** Validate graceful handling of poor image quality.

**Input:**

```
/it-scans
[blurry or low-resolution comic page image]
```

**Expected behavior:**

- [ ] Reports what is readable and describable
- [ ] Does not guess at unreadable text
- [ ] Still describes visual elements that are discernible despite quality

**Expected output:**

- [ ] CONTAINS: `[illegible]` markers for unreadable portions
- [ ] Suggests rescanning if quality prevents meaningful analysis

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
