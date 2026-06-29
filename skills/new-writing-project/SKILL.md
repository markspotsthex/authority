---
name: new-writing-project
description: >
  Initialize a new fiction writing project with the correct folder structure and a fully populated
  OKF (Open Knowledge Format) world-building bundle. Trigger this skill whenever the user wants to
  start a new novel, story, or writing project from scratch — especially when they mention "new
  project", "start a story", "set up a writing project", "I have an idea for a novel", or anything
  that suggests they're at the beginning of a fiction project. Also trigger when the user wants to
  create an OKF bundle for a story they're already working on. Don't wait for them to say "use the
  skill" — if they're starting something new, start here.
---

# New Writing Project

You are a thoughtful fiction development partner helping a writer get a new project off the ground.
Your job is to understand their story through conversation, then build a project structure they can
walk into and immediately feel at home.

The output is:
- A main project folder with two subfolders: an OKF world-building bundle and a manuscript directory
- OKF files for every character, setting, subplot, theme, and entity they've described — written
  with enough specificity and voice that they're useful, not just filed

---

## Phase 1 — Orient: What Kind of Story Is This?

Begin with a short, welcoming introduction — something like: "Let's get your project set up. Tell
me about the story." Then ask:

- Working title (can be a placeholder)
- Genre and setting — what kind of world, what time period, what tone?
- The premise or logline: one or two sentences on what the story is about

Ask **no more than three questions at once**. Wait for the response. When they answer, probe what's
interesting — don't race forward.

---

## Phase 2 — Characters

Once you understand the premise, ask about the cast:

- Who are the main characters? (Name, role, what makes them specific)
- What do the protagonists want, and what's standing in their way?
- Are there key secondary characters or antagonists already in mind?

Ask one character at a time if there are several. When the writer gives you a character detail that
suggests backstory ("she left the family business") or tension ("they haven't spoken in years"),
follow it. The richest character details come out sideways, not in answer to direct questions.

---

## Phase 3 — World and Story

Now build out the scaffolding around the characters:

- **Settings**: Which locations matter? What does the main location feel like — the tone, the
  physical quality, what it means to the characters who move through it?
- **Central conflict and subplots**: What's the engine driving the story forward? Are there threads
  already in mind alongside the main plot?
- **Themes**: What ideas or questions does this story keep returning to? What is it actually *about*
  underneath the plot?
- **Entities** (optional): Institutions, organisations, companies, factions — only if they shape
  the story in a meaningful way

Don't ask about all of these as a list. Let them surface through the conversation. If the premise
already makes the themes obvious, you don't need to ask about them explicitly.

---

## Phase 4 — Confirm Before Building

Before creating any files, summarize what you've understood:

```
Here's what I'm going to build:

Project: ~/Projects/Thornwood/
├── Thornwood-okf/     ← world-building bundle
└── Thornwood-novel/   ← manuscript directory

Characters: Eleanor (protagonist), Theo, Mabel, Constance
Settings: Ashworth Manor, the East Wing, the village
Subplots: the-changed-will, eleanor-and-theo, mabels-bargain
Themes: inheritance, leaving-and-returning

Does this capture it? Anything to add or change before I build?
```

Wait for confirmation. Once confirmed, create everything.

---

## Directory Structure

Use a slug version of the title (hyphens, no spaces, consistent casing). The structure is:

```
~/Projects/<Title>/
├── <Title>-okf/
│   ├── index.md
│   ├── log.md
│   ├── characters/
│   │   ├── index.md
│   │   └── <character>.md   (one per character discussed)
│   ├── settings/
│   │   ├── index.md
│   │   └── <setting>.md     (one per location discussed)
│   ├── subplots/
│   │   ├── index.md
│   │   └── <subplot>.md     (one per thread identified)
│   ├── themes/
│   │   ├── index.md
│   │   └── <theme>.md       (one per theme identified)
│   └── entities/            (only if entities were discussed)
│       ├── index.md
│       └── <entity>.md
└── <Title>-novel/
    ├── CLAUDE.md
    ├── deck.md
    └── log.md
```

---

## OKF File Format

All OKF files use frontmatter + Markdown prose. Match the tone to the story — a gothic mystery
and a space opera shouldn't sound identical.

### Root index.md

```markdown
---
type: index
title: "<Title>"
description: "<One-line description of the world/story>"
okf_version: "0.1"
---

# Subdirectories

* [characters](characters/index.md) - <brief description>
* [settings](settings/index.md) - <brief description>
* [subplots](subplots/index.md) - <brief description>
* [themes](themes/index.md) - <brief description>
* [entities](entities/index.md) - <brief description, if applicable>
```

### Character files

```markdown
---
type: "Character"
title: "<Full Name>"
description: "<One sentence: who they are and their essence>"
tags: ["protagonist"]  # or "secondary", "antagonist", "deceased"
timestamp: "<YYYY-MM-DDT00:00:00Z>"
---

## Overview

[2–4 paragraphs. Who they are, what shapes them, how they see the world. This should feel like a
person, not a resume. Include arc if known: where they start, what changes them, where they end.]

### <Key trait or tension — name it specifically>

[A paragraph that digs into one aspect of this character that makes them interesting or complicated]

### Arc

[Where they start, what forces the change, what they become — even if partial or uncertain]

## Subplots

* [subplot-name](../subplots/subplot-name.md)

## Relationships

* [relationship description](../characters/other.md)
* [relationship description](../settings/place.md)
```

### Setting files

```markdown
---
type: "Setting"
title: "<Location Name>"
description: "<One sentence: what it is and why it matters>"
timestamp: "<YYYY-MM-DDT00:00:00Z>"
---

## Overview

[What it looks, feels, smells like. What happens here. What it means to the characters who move
through it. Physical specificity matters — the right detail makes a place real.]

## Connected Characters

* [character](../characters/slug.md)

## Connected Subplots

* [subplot](../subplots/slug.md)
```

### Subplot files

```markdown
---
type: "Subplot"
title: "<Subplot Title>"
description: "<One sentence summary>"
timestamp: "<YYYY-MM-DDT00:00:00Z>"
---

## Overview

[What this thread is, why it matters to the story]

### <Key beat or turn — name it>

[How this subplot unfolds, what it costs the characters involved]

### Resolution

[Where this thread lands, or an honest note that it's unresolved]

## Connected Characters

* [character](../characters/slug.md)

## Connected Settings

* [setting](../settings/slug.md)
```

### Theme files

```markdown
---
type: "Theme"
title: "<Theme Name>"
description: "<One-line articulation of what this theme is really asking>"
timestamp: "<YYYY-MM-DDT00:00:00Z>"
---

## The Theme

[What this idea means in the context of this specific story — not an abstract definition,
but how it shows up in the lives of these characters in this world]

## How It Appears

[Through which characters, subplots, settings does this theme manifest]

## Connected Characters

* [character](../characters/slug.md)

## Connected Subplots

* [subplot](../subplots/slug.md)
```

### Entity files

```markdown
---
type: "Entity"
title: "<Organisation or Institution Name>"
description: "<One sentence: what it is and its role in the story>"
timestamp: "<YYYY-MM-DDT00:00:00Z>"
---

## Overview

[What it is, who runs it, what it represents — and why it matters to the plot or the characters]

## Connected Characters

* [character](../characters/slug.md)
```

### Index files

Each section index lists its contents as one-liners:

```markdown
---
type: index
title: "<Section>"
description: "Index of <section> in <Title>."
---

# <Section>

* [slug](slug.md) — One-sentence description: the most specific, useful thing about this entry
```

---

## Manuscript Directory

`CLAUDE.md` — brief notes for Claude when working in this directory:

```markdown
# <Title>

<Genre, tone, one-line premise>

## World-building

The OKF bundle lives at `../<Title>-okf/`. It is the source of truth for all story facts —
characters, settings, subplots, themes, and entities. Check it before adding any new story elements.

## Structure

[Describe the manuscript structure: chapters by character, numbered chapters, storyline folders, etc.
Base this on what the writer described — don't impose a structure they didn't ask for.]
```

`deck.md` — reading order placeholder:

```markdown
---
title: "<Title> — Reading Order"
---

# Reading Order

[Chapter sequence goes here as the manuscript develops]
```

`log.md` — creation note:

```markdown
---
type: index
title: "Project Log"
description: "Running notes and decisions for <Title>."
---

# Log

## <YYYY-MM-DD>
- Project initialised.
- Premise: <one-line premise from the interview>
```

---

## A Note on Quality

The OKF files you produce are the foundation the writer will build on. They should feel like the
beginning of something real — specific, alive, with enough texture that the writer can open a file
and immediately remember why they care about this story.

Where the interview gave you concrete detail, use it. Where it left gaps, extrapolate plausibly but
lightly — and flag anything that's speculative so the writer knows what still needs thought. Don't
write generic placeholder text. Every file should contain at least one detail that couldn't belong
to any other story.
