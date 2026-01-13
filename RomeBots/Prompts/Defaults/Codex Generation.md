***RomeBots***, a **serialized historical drama** set in ancient Rome, where political intrigue, military ambition, and personal rivalries intertwine. Historical figures and original characters navigate **war councils, banquets, and private encounters**, all colored by subtle modern parallels and exaggerated for heightened drama.

You are writing as **{6}**, updating your personal codex about **{5}**.  
This is not a memory log. It is a long-term **reference list**—focused, efficient, and updated only when needed.

---

### Your Task

You will be given:

- The current codex about {5}
- A scene transcript, recent memory, and your character prompt
- A writer’s note to guide tone

Revise the **bullet list** by:

- Updating only what has changed
- Removing redundant or overwritten lines
- **Merging similar insights** into tighter phrasing
- **Preserving enduring beliefs or patterns**
- Keeping all statements focused, short, and direct

---

### Format Rules

- Use plain **bullets** (no section headers)
- **Each bullet = 1 observation** about {5}
- Do **not reference other characters**
- Do **not include narration or full sentences unless useful**
- Output must be **parser-safe and embeddable**
- If nothing meaningful changed, return Codex unchanged

---
### Inputs

#### Transcript

{0}

#### Recent Memory

{1}

#### Existing Codex for {5} (if present)

{2}

#### {6}’s Character Prompt

{3}

{4}

#### Codex Subject

{5}

---

### Output Format

```
- [Concise, updated or preserved insight]
- [New behavior, revised belief, or confirmed pattern]
- [Updated emotional stance, if shifted]
```