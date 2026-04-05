# Prompt Layer Map

This note labels the current HBOx prompt stack by function instead of just by folder.

The goal is to answer three questions:

1. Which prompt files are structural?
2. Which prompt files are carrying show-specific content?
3. Where should world bible, character dynamics, and plot progression actually live?

## Legend

| Label | Meaning |
| --- | --- |
| `Structural` | Defines pipeline shape, stage contract, or rendering format |
| `World Bible` | Persistent setting truths, institutions, tone boundaries, metaphysics, social rules |
| `Character` | Persistent character identity, relationship shape, personal tactics, voice |
| `Plot State` | What is currently true in the story, what changed, what must carry forward |
| `Mixed` | Doing more than one of the above at once |

## Runtime Map

Current runtime flow:

`Idea -> Defaults.md -> Behavior Generation -> Editor Process -> Dialogue Generation -> Continuity/Memory -> Sequel Generation`

That means the practical split is:

- scene seed
- per-character scene stance
- shared scene spine
- performed dialogue
- continuity update
- next-scene pressure proposal

## Current Prompt Table

| Current file or pattern | Stage | Label now | Structural? | What it is doing now | Where it should mainly live |
| --- | --- | --- | --- | --- | --- |
| `Vault/<Show>/Prompts/Defaults.md` | Scene seed | `Mixed` | `Yes` | Defines the seed output format and also carries a large share of show bible and scene-selection logic | Structural scene seed frame plus a light world-bible header |
| `Vault/<Show>/Prompts/Actors/*.md` | Character source | `Character` | `No` | Holds persistent character identity, social role, habits, tactics, relationship hints, and voice | Character dynamics |
| `Vault/<Show>/Prompts/Defaults/Behavior Generation.md` | Per-character scene stance | `Mixed` | `Yes` | Converts scenario + actor file + memory into a scene-specific tactic/state brief | Mostly character dynamics, with plot-state input |
| `Vault/<Show>/Prompts/Defaults/Editor Process.md` | Scene consolidation | `Mixed` | `Yes` | Merges scenario and character cues into the canonical scene context; currently also carries a lot of show logic | Mostly structural scene engine, fed by world bible + character + plot state |
| `Vault/<Show>/Prompts/Defaults/Dialogue Generation.md` | Dialogue rendering | `Structural` | `Yes` | Enforces script format, mouth-feel, escalation rules, and parser-safe output | Structural output style layer |
| `Vault/<Show>/Prompts/Defaults/Memory Generation.md` | Personal carryover | `Plot State` | `Yes` | Produces biased first-person updates for what one character now remembers and will carry forward | Character-specific plot state |
| `Vault/<Show>/Prompts/Defaults/Episode To Episode Continuity.md` | Serialized carryover | `Plot State` | `Yes` | Summarizes public consequences, rumors, unresolved issues, and next-episode hooks | World/story plot state |
| `Vault/<Show>/Prompts/Defaults/Sequel Generation.md` | Next-scene escalation | `Mixed` | `Yes` | Turns prior context and actor states into the next pressure chamber | Plot progression engine |
| `Vault/<Show>/Prompts/Act 1/Sequel Generation.md` | Early escalation variant | `Plot State` | `Yes` | Biases sequel generation toward premise stabilization and early-series lock-in | Plot progression by phase |
| `Vault/<Show>/Prompts/Act 2/Sequel Generation.md` | Mid escalation variant | `Plot State` | `Yes` | Biases sequel generation toward complication and collision | Plot progression by phase |
| `Vault/<Show>/Prompts/Act 3/Sequel Generation.md` | Late escalation variant | `Plot State` | `Yes` | Biases sequel generation toward endgame escalation and consequence | Plot progression by phase |
| `Vault/<Show>/Prompts/Openers/*.md` | Upstream framing | `Mixed` | `No` | Provides thematic hooks, cluster focus, or cold-open energy; often mixes premise, character grouping, and conflict frame | Usually plot entry framing plus some character clustering |
| `Vault/<Show>/Prompts/Reddit Source.md` | Source adaptation | `Structural` | `Yes` | Translates external inputs into idea seeds | Structural source adapter |
| `Vault/<Show>/Prompts/Defaults/Codex Generation.md` and actor codex subfiles | Pairwise relationship post-pass | `Character` | `Yes` | Enriches relationship-specific interaction logic after dialogue | Character relationship layer |

## RomeBots

| File | Label now | Why |
| --- | --- | --- |
| `Vault/RomeBots/Prompts/Defaults.md` | `Mixed` | It is structurally a scene-seed prompt, but it also carries a strong RomeBots world bible: politics through family, ritual, gifts, silence, marriages, and social pressure. |
| `Vault/RomeBots/Prompts/Actors/Agrippa.md` | `Character` | Persistent voice, method, and relationship posture. This is exactly where character identity belongs. |
| `Vault/RomeBots/Prompts/Defaults/Behavior Generation.md` | `Mixed` | It uses the actor profile and current scenario to create scene-specific tactic and pressure. This is the bridge between character bible and plot state. |
| `Vault/RomeBots/Prompts/Defaults/Editor Process.md` | `Mixed` | It acts like a scene engine, but it also currently asks the prompt to preserve political standing, personal history, emotional state, setup, escalation, and final power shift all at once. |
| `Vault/RomeBots/Prompts/Defaults/Dialogue Generation.md` | `Structural` | Mostly clean. It is not deciding the story; it is deciding how the story gets spoken. |
| `Vault/RomeBots/Prompts/Defaults/Episode To Episode Continuity.md` | `Plot State` | Tracks publicly weaponizable consequences, rumors, and unresolved issues. |
| `Vault/RomeBots/Prompts/Defaults/Sequel Generation.md` | `Mixed` | Very close to a true plot engine, but it still partly substitutes for an explicit story-state layer. |
| `Vault/RomeBots/Prompts/Act 1/Sequel Generation.md` | `Plot State` | Good example of phase-specific plot logic: convert joke to motive, confusion to plan, slight to grudge. |
| `Vault/RomeBots/Prompts/Openers/Triumvirate Talk.md` | `Mixed` | Clusters characters, defines ideological fault lines, and frames a specific conflict entry point. |

### RomeBots read

`RomeBots` is already close to the right layering:

- world bible is mostly in `Defaults.md`
- character dynamics are mostly in `Actors/*.md`
- plot progression is split between continuity and sequel prompts

The main blur is that `Editor Process` and `Sequel Generation` are still carrying some world-state and plot-state burden that would be cleaner in a dedicated story-state layer.

## SpaceDrivel

| File | Label now | Why |
| --- | --- | --- |
| `Vault/SpaceDrivel/Prompts/Defaults.md` | `Mixed` | It is structurally a seed prompt, but it also carries the shipboard premise and anomaly logic. |
| `Vault/SpaceDrivel/Prompts/Actors/Pete.md` | `Character` | Strong example of character file as pressure profile: role in the room, want, control method, misread, pressure tell. |
| `Vault/SpaceDrivel/Prompts/Defaults/Behavior Generation.md` | `Mixed` | Converts persistent character design into current-scene tactic and destabilization. |
| `Vault/SpaceDrivel/Prompts/Defaults/Editor Process.md` | `Mixed` | Explicitly asks for the immediate problem, deeper problem, each character's tactic, escalation path, and final consequence. This is the scene spine, but it is still doing some job of story-state synthesis too. |
| `Vault/SpaceDrivel/Prompts/Defaults/Dialogue Generation.md` | `Structural` | Mostly a rendering contract plus house style. It is behaving as intended. |
| `Vault/SpaceDrivel/Prompts/Defaults/Episode To Episode Continuity.md` | `Mixed` | Intended to be plot state, but the current text still reads like a RomeBots public-rumor template instead of a shipboard anomaly continuity layer. |
| `Vault/SpaceDrivel/Prompts/Defaults/Sequel Generation.md` | `Plot State` | Stronger than RomeBots here. It explicitly inherits damage, adds new complication, mutates behavior, and forces a concrete consequence. |
| `Vault/SpaceDrivel/Prompts/Openers/Cosmic Horror.md` | `Mixed` | Opens with thematic premise, character clustering, belief conflict, and ontological framing all together. |

### SpaceDrivel read

`SpaceDrivel` has a cleaner sequel engine than its continuity engine.

The strongest fit is:

- world bible in the show seed and any future ship/anomaly bible layer
- character dynamics in actor files and behavior generation
- plot progression in sequel generation

The weak spot is continuity. Its continuity prompt still carries residue from a Rome-like public-social model instead of a shipboard systems-and-belief model.

## What Counts As Structural

These are the pieces that should stay relatively stable across new IPs such as cowboys, cops, or military:

| Prompt family | Structural reason |
| --- | --- |
| `Defaults.md` | The seed-stage contract is reusable even when the tone changes |
| `Defaults/Behavior Generation.md` | The runtime needs a per-character scene-state pass no matter the IP |
| `Defaults/Editor Process.md` | The runtime benefits from a canonical scene spine before dialogue |
| `Defaults/Dialogue Generation.md` | The parser and output format need a stable contract |
| `Defaults/Memory Generation.md` | Character carryover is a reusable stage |
| `Defaults/Episode To Episode Continuity.md` | World/story carryover is a reusable stage |
| `Defaults/Sequel Generation.md` | Follow-on pressure generation is a reusable stage |

These are the pieces that should stay highly IP-specific:

| Prompt family | Why |
| --- | --- |
| `Actors/*.md` | This is where the cast actually becomes itself |
| `Openers/*.md` | These are premise injectors and should reflect the show's favorite entry points |
| show-specific tone language inside `Defaults.md` | The seed prompt must know what kind of pressure this world considers normal |
| act-specific sequel variants | Serialization rhythm is not universal |

## Best Placement For The Three Buckets

| Bucket | Best home in the current system | Notes |
| --- | --- | --- |
| World Bible | `Defaults.md` plus a future dedicated world-state/bible insert | Good for persistent setting truths, institutions, metaphysics, and tone limits. It should not have to re-explain current plot motion every scene. |
| Character Dynamics | `Actors/*.md` plus `Behavior Generation.md` | Actor files should define persistent personality and pressure style. Behavior generation should define what that looks like now, in this exact scene. |
| Plot Progression | `Episode To Episode Continuity.md` plus `Sequel Generation.md` | Continuity should say what changed in the world. Sequel should say what pressure chamber comes next because of it. |

## Current Friction Points

| Friction point | Why it matters |
| --- | --- |
| `Editor Process` is doing too much | It is currently part scene engine, part plot-state merger, and part show bible reminder. That makes it a likely place for prompt bloat. |
| `Sequel Generation` partly substitutes for missing explicit story state | When sequel prompts must both infer the current world and propose the next scene, they start carrying too much editorial load. |
| Some continuity prompts are not fully IP-aligned | The SpaceDrivel continuity prompt still reads like a public-rumor serial instead of a closed-system shipboard serial. |
| `Defaults.md` still does double duty | It is both seed contract and show bible. That works, but it will get harder to scale when you start standardizing prompt trees across many settings. |

## Recommended Next Split

If HBOx grows toward a reusable "compile the world bible into the prompt" system, the clean next split is:

| Future layer | Source material | Feeds |
| --- | --- | --- |
| World Bible | show bible note(s), setting rules, institutions, metaphysics | `Defaults.md`, `Editor Process`, maybe `Continuity` |
| Story State | timeline position, live alliances, deaths, marriages, current dangers, public mood, active theories | `Defaults.md`, `Behavior Generation`, `Editor Process`, `Sequel Generation` |
| Character Bible | actor notes, pairwise codex, stable wants and methods | `Behavior Generation`, `Dialogue Generation` |
| Scene Spine | current scene seed, selected cast, location, live pressure, target shift | `Dialogue Generation` |
| Output Style | script formatting and mouth-feel | `Dialogue Generation` |

That would let the prompt tree stop reusing the same paragraph for multiple jobs.

## Short Version

Right now the HBOx prompt stack is already close to the right architecture:

- `Actors/*.md` is mostly character
- `Dialogue Generation.md` is mostly structural
- `Continuity` and `Sequel` are mostly plot state
- `Defaults.md` and `Editor Process.md` are the main mixed layers

So the real cleanup target is not "invent a new system."

It is:

1. keep the current stage pipeline
2. separate persistent world truths from current story state
3. let `Editor Process` become a cleaner scene engine instead of a catch-all merger
