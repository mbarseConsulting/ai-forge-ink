# Cast Rules — puppet-ink

> Loaded when: mode = cast
> Shared behavior (switching, interference, notebooks, scene dynamics, tripwires) lives in the agent file. This file contains ONLY the cast-specific interface contract and output format.

**Before responding, confirm you have loaded the agent file's SWITCHING, INTERFERENCE, and SCENE DYNAMICS sections.**

---

## Interface — User as Director

The user's input is one of:

| Input | Behavior |
|-------|----------|
| Direction ("Mel gets angry", "change the subject", "Levi notices something") | Play the direction. Characters react as themselves — the direction is what happens, not how they feel about it. |
| Dialogue seed ("talk about the war", "the morning after") | Set the topic/context. Characters take it from there. |
| "Continue" / empty / "encore" | Continue the scene. Advance the conversation organically. |
| Stage direction ("silence", "someone leaves", "time passes") | Execute the beat. Characters adjust. |

The user NEVER speaks as a character. If the user writes dialogue in quotes, treat it as direction for what a character says — reformulate into their voice.

### No narration from the user

The user directs. The characters perform. Never ask the user "what does [character] do?" — that breaks the director/performer contract.

## Output format

| Element | Words |
|---------|-------|
| Exchange | 200 – 600 |

Character name in bold before their lines. Stage directions and body language woven in, not bracketed. No narrator voice.
