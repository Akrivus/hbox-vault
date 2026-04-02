# Vault Architecture Map

Vault is the prompt and trace layer for HBOx.

At runtime, HBOx resolves markdown files from `Vault/<Show>/Prompts/...`, sends them to the LLM, and then writes the resolved prompt text and model outputs back under `Vault/<Show>/Inputs/...` and `Vault/<Show>/Outputs/...`.

That makes Vault more than a content folder:

- It defines each show's editorial voice.
- It defines the generation pipeline stage by stage.
- It acts as the primary debugging record for what the model was asked and what it returned.

## Core Folder Shape

Each show generally follows this structure:

```text
Vault/<Show>/
  Prompts/
    Defaults.md
    Reddit Source.md
    Actors/
    Defaults/
    Openers/
    Act 1/              # only some shows
    Act 2/              # only some shows
    Act 3/              # only some shows
  Inputs/
  Outputs/
  Memories/
```

### Meaning of the main prompt folders

- `Prompts/Defaults.md`
  The scene-seeding prompt. This is the first major show-level prompt used by `ChatGenerator` unless a generator-specific prompt overrides it.
- `Prompts/Actors/*.md`
  Character bibles. These are loaded into `ActorContext.SetPrompt()` and shape behavior, voice, emotional reflexes, and relationship cues.
- `Prompts/Defaults/*.md`
  Stage-specific prompts used by shared generator components such as behavior generation, dialogue generation, sentiment tagging, memory generation, title cards, and continuity.
- `Prompts/Openers/*.md`
  Thematic framing layers. These are usually used upstream as idea-shaping or context-shaping material rather than the main script-writing prompt.
- `Prompts/Reddit Source.md`
  The source adapter prompt for Reddit-driven idea generation.
- `Prompts/Act 1`, `Act 2`, `Act 3`
  Follow-on escalation prompts used by sequel/continuation flows in shows that are structured more serially.

## Runtime Resolution Model

The main resolver lives in `Assets/Core/Integrations/Vault/PromptResolver.cs`.

Important rules:

- `new PromptResolver(chatGenerator)` resolves `Vault/<Show>/Prompts/<GeneratorName>.md`.
- If that file does not exist, it falls back to `Vault/<Show>/Prompts/Defaults.md`.
- `new PromptResolver(chatGenerator, subGenerator)` resolves `Vault/<Show>/Prompts/<GeneratorName>/<SubGeneratorName>.md`.
- If that file does not exist, it falls back to `Vault/<Show>/Prompts/Defaults/<SubGeneratorName>.md`.
- `new PromptResolver(actor)` resolves `Vault/<Show>/Prompts/Actors/<ActorName>.md`.

This means the shared C# pipeline stays mostly constant while each show swaps in its own prompt stack.

## End-to-End Prompt Chain

The prompt chain is driven by `Assets/Core/ChatGenerator.cs`.

### 1. Idea formation

An upstream source produces an `Idea`.

Possible sources include:

- replay folders
- HTTP routes
- Reddit batches
- scene-specific systems like `polbots` soccer mode

For Reddit runs, `Assets/Core/Integrations/Sources/RedditSource.cs` builds the `Idea` by:

1. loading `Prompts/Reddit Source.md`
2. optionally loading a dated or named meta-prompt from `Prompts/Reddit Source/...`
3. injecting mined Reddit material into that wrapper

At this stage, the system is not writing the final scene yet. It is choosing what kind of scene pressure to introduce.

### 2. Scene seed generation

`ChatGenerator.Generate()` resolves the show's top-level generator prompt:

- usually `Prompts/Defaults.md`
- or `Prompts/<GeneratorName>.md` if a scene-specific override exists

Inputs injected here are:

- prior continuity context from `MemoryBucket.GetContext(...)`
- the available character pool
- the current idea text
- the available location pool

The result is expected to contain:

- `Location: ...`
- `Characters: ...`
- a scenario description or equivalent dramatic seed

This stage decides who is in the scene, where it happens, and what the immediate dramatic problem is.

### 3. Character interpretation

`BehaviorGeneration` runs once per selected actor.

It combines:

- the generated scenario
- the original idea
- the actor prompt from `Prompts/Actors/...`
- any accumulated memory bucket for that actor

The output is not final dialogue. It is a behavior brief describing how that character will react, misread, posture, spiral, or confess inside the scene.

### 4. Scene consolidation

`EditorProcess` merges the scenario with all actor behavior briefs into the canonical scene context.

This is where HBOx turns:

- one show-level setup prompt
- several actor-level behavior prompts

into one shared dramatic context that later generators can consume.

In practice, this is the layer that converts "premise plus cast" into "what is actually happening in this room right now."

### 5. Dialogue generation

`DialogueGeneration` turns the consolidated context into line-by-line dialogue.

Its prompt usually lives at:

- `Prompts/Defaults/Dialogue Generation.md`

This stage consumes:

- the original idea
- the consolidated character context
- the scenario/context built earlier

The output is parsed into `ChatNode`s.

This is the point where the show's voice becomes visible on screen.

### 6. Post-dialogue enrichment

After dialogue exists, additional prompt-driven components may run.

Common ones:

- `SentimentTagger`
  Assigns reactions/sentiments to lines and to the initial state of the scene.
- `SentimentAnalyzer`
  A stronger variant that can also suggest line edits and delivery notes.
- `MemoryGeneration`
  Produces per-character memory summaries from the finished scene.
- `EpisodeToEpisodeContinuity`
  Produces serialized continuity memories for future scenes.
- `VibeSelector`
  Picks the music/scene vibe.
- `TitleCardGeneration`
  Generates episode title and synopsis.
- `DialogueEditorProcess`
  Rewrites or tightens existing lines after the first pass.
- `SequelGeneration`
  Produces a follow-up idea based on the resulting state of the cast.
- `CodexGeneration`
  Runs pairwise codex/interpersonal prompts for actor relationships where those files exist.

Not every show or scene uses every stage, but they all follow the same resolver pattern.

## Vault as Diagnostic Layer

When an LLM call succeeds, HBOx writes:

- the resolved prompt text to `Vault/<Show>/Inputs/...`
- the model output to `Vault/<Show>/Outputs/...`

Those traces are grouped by prompt part name, so a single run can usually be reconstructed as:

1. top-level scene seed
2. per-actor behavior prompts
3. editor/context merge
4. dialogue generation
5. post-processing stages like sentiments, memory, sequel, or title cards

This means prompt debugging should usually start in Vault before changing C#:

- Was the right prompt file selected?
- Were the placeholders populated with the right context?
- Did the model output match the parser assumptions of that stage?
- Did continuity or memory inject the expected prior state?

## Show-by-Show IP Breakdown

## `polbots`

`polbots` is the oldest and broadest prompt library.

Key traits:

- geopolitical sitcom tone
- very large actor roster
- more mode-specific overrides than the other shows
- strongest attachment to input-source adapters like Reddit and soccer events

Prompt character:

- loud, sloppy, interrupt-heavy
- humor through ego, national caricature, grievance, confusion, and accidental honesty
- politics expressed as personal insecurity rather than speeches

Notable Vault traits:

- 200+ actor prompts
- large `Openers/` library
- special generator branches such as `Soccer Mode/...`
- top-level show-specific prompts like `UN Discord.md` and `Soccer Mode.md`

Editorially, `polbots` is the least serialized and most reactive. It excels at turning a live topic or event stream into messy group-chat energy.

## `RomeBots`

`RomeBots` is a serialized dynastic melodrama disguised as a historical satire.

Key traits:

- social pressure over spectacle
- power expressed through manners, ritual, and domestic proximity
- young elites making permanent decisions with immature emotional tools

Prompt character:

- subtext-heavy
- formal language used as a weapon
- comedy through politeness, plausible deniability, and quiet cruelty
- consequence always lurking under the joke

Notable Vault traits:

- compact but specific actor prompts
- strong `Defaults.md` world bible
- sequel prompts split into `Act 1`, `Act 2`, and `Act 3`
- stronger emphasis on continuity and escalation than `polbots`

Editorially, `RomeBots` uses Vault to keep power dynamics coherent across scenes, not just to make single-scene jokes land.

## `AppyDays`

`AppyDays` is startup melodrama built out of hype language, emotional exhaustion, and corporate self-deception.

Key traits:

- office politics as survival
- buzzwords used like shields, threats, apologies, and pickup lines
- burnout, debt, ego, HR-speak, and magical thinking

Prompt character:

- cringe-comic but emotionally legible
- strong emphasis on coping mechanisms and professional language hiding private collapse
- scenes feel like meetings held during a soft emergency

Notable Vault traits:

- a strong show bible in `Defaults.md`
- actor prompts that are often short, high-signal personality fragments
- opener set tuned around organizational dysfunction
- no custom act folders, so serialization is driven more by continuity buckets than act-specific sequel scaffolding

Editorially, `AppyDays` is the "systems failure in human language" show.

## `SpaceDrivel`

`SpaceDrivel` shares some modular structure with `AppyDays`, but its emotional engine is paranoia, distortion, and existential malfunction.

Key traits:

- low-budget shipboard sci-fi
- unreliable perception
- emotional desperation mixed with procedural failure
- cosmic dread filtered through petty crew dynamics

Prompt character:

- disorientation without losing scene playability
- reality slips, lies, hallucinations, and fear
- dark comedy from people trying to stay functional inside a broken ontology

Notable Vault traits:

- strong world bible in `Defaults.md`
- actor prompts built around trauma, denial, and role failure
- openers oriented around science, debates, lab drama, and cosmic horror
- act-structured sequel prompts similar to `RomeBots`

Editorially, `SpaceDrivel` uses the same chain as the more grounded shows, but every stage is biased toward making reality itself feel unstable.

## How the IPs Relate

All four shows share the same runtime grammar:

- source framing
- scene seed
- actor interpretation
- scene merge
- dialogue
- post-processing and continuity

What changes from show to show is not the engine but the pressure model:

- `polbots`: reactive chaos
- `RomeBots`: dynastic pressure
- `AppyDays`: institutional delusion
- `SpaceDrivel`: ontological drift

That is why Vault matters so much: the same generator components can produce radically different worlds because the prompts define what kind of failure, humor, fear, and escalation count as normal.

## Practical Debugging Checklist

When a generation feels wrong, check Vault in this order:

1. Was the upstream `Idea` framed correctly?
2. Did `Defaults.md` choose the right characters and location?
3. Did actor prompts produce distinct behavior briefs?
4. Did `Editor Process` preserve the useful tension instead of flattening it?
5. Did `Dialogue Generation` keep the show's mouth-feel and parser-friendly structure?
6. Did post-processing stages add signal or muddy the scene?
7. Did continuity buckets inject the right prior memories?

If the answer is "the scene is technically valid but spiritually wrong," the problem is usually in Vault before it is in code.

