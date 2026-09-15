---
status: active
project: meta
type: guide
subtype: skill-router
description: Build a presentation as HTML, either a deck for a talk or a tabbed presentation site for a link. Fires whenever Rick asks for a presentation, deck or slides. Loads after Core Design, never instead of it. Default brand is Terracotta; JADS for anything handed to the university.
last_updated: 2026-08-16 01:05
---

# Skill: HTML Presentations

The router. It holds the trigger, the hard rule, the default brand, and the read order. The
method sits in the numbered nodes.

Created 2026-08-10. Before it existed, deck mechanics lived inside the JADS brand profile,
which meant a session building a non-JADS deck had no source for them, and
[[08 - Skills/Data Apps/0 Data Apps|Data Apps]] had to be told to skip half that file.

## When this fires

Rick asks for a presentation, a deck, slides, or a pitch. Academic presentations, project
presentations, consulting decks, technical talks, data storytelling.

**It never fires alone.** [[08 - Skills/Core Design/0 Core Design|Core Design]] is read
first and establishes the brand. This skill turns that brand into slides.

## The hard rule

**A deck is not a website with slide dividers.**

They share a rendering engine and almost nothing else. A fixed stage, a hard density budget
per slide, a speaker who exists, and discrete linear navigation each fork the work away from
web conventions. Applying a web habit to a deck is the failure this skill exists to prevent,
and the reverse is equally wrong.

## First question: is it presented, or is it sent?

**Added 2026-08-15.** Rick tested the rule above rather than taking it on trust, and the test
found a third artifact. Ask this before anything else, because it changes the whole build:

| The presentation is | Build | Read |
|---|---|---|
| **Stood in front of**, with a clicker | A deck | The numbered nodes below |
| **Sent as a link**, read alone at a desk | A presentation site | [[08 - Skills/HTML Presentations/Presentation sites\|Presentation sites]], plus the numbered nodes |

**Neither is a better version of the other.** A site presented in a room makes the audience
watch blank panels animate in; a deck emailed as a link says far too little to read alone.
**If it is genuinely both, build the deck and say so**, because a deck read alone degrades more
gracefully than a site presented badly.

## Format: HTML, one self-contained file

**Default for every deck, whatever the brand.** Rick's decision, 2026-08-01, after building
the same deck both ways. A `python-pptx` build costs far more tokens for a worse result, the
output looks cleaner in HTML, and a single file opens anywhere, prints to PDF one slide per
page, and needs no software.

Only build a `.pptx` when someone other than Rick has to edit the file, and say why.

## The brand: Terracotta by default

Row 1 of the ladder in [[08 - Skills/Core Design/0 Core Design|Core Design]]. **Rick's
decision, 2026-08-15**, replacing the JADS default he set on 2026-08-10.

| Answer | Load |
|---|---|
| Default, anything not otherwise named | [[08 - Skills/Core Design/Terracotta - presentation default\|Terracotta]] |
| Coursework, or anything handed to the university | [[03 - School/_Meta/JADS Presentation Style Guide\|JADS Presentation Style Guide]] |
| Rick's own brand, for a personal talk | The `Rick - *` nodes in `Core Design` |
| A custom palette Rick supplies | His values. Only the colours swap |

**The one risk in this default, and it is worth a sentence when it comes up.** JADS stopped
being automatic, so a deck that is actually being handed in is only JADS if Rick says so or the
task makes it obvious. **When a deck is for a course, a supervisor or a submission, ask before
building it in Terracotta.**

**Do not build the same deck in several brands to compare.** Rick called that token waste on
2026-08-15. Build the default, and rebuild in another brand only when he asks.

**The brand supplies the values. This skill supplies the architecture.** A custom palette
changes what a step card looks like, never whether the deck has a density budget.

## Colour is the variable. Everything else is fixed

**Rick's decision, 2026-08-15**, after seeing one narrative built in four brands. The goal he
stated: a deck gets built the same way every time, from the same archetypes, at the same type
scale, with the same motion, so quality does not depend on which session built it.

| Fixed on every deck | The brand's to set |
|---|---|
| The type scale, and Inter embedded in the file, per [[08 - Skills/HTML Presentations/1 Deck architecture\|1 Deck architecture]] | Colour, in every role |
| The archetypes and the density budget | Radius and shadow |
| The entrance animation | Which colour marks the emphasised element |
| Navigation, printing, the single-file rule | |

**No brand overrides the font any more.** JADS mandated Arial in its own style guide; Rick
ruled on 2026-08-15 that the house font wins, so **every deck carries Inter**, JADS included.
That section of the JADS guide is struck through rather than deleted, so the override reads as
deliberate.

**The deck is not where a new idea gets tried.** If something here is wrong, change it here,
for every future deck, rather than making one deck special.

## Read order

1. [[08 - Skills/HTML Presentations/1 Deck architecture|1 Deck architecture]] — the fixed
   stage, the slide model, the density budget. Always.
2. [[08 - Skills/HTML Presentations/2 Slide component library|2 Slide component library]]
   — the archetypes every slide is built from. Always.
3. [[08 - Skills/HTML Presentations/3 Deck delivery|3 Deck delivery]] — navigation,
   printing, and the single-file constraint. Always, before handing anything over.

Plus the brand, from `Core Design`.

**Conditional, loaded only when the task needs them:**

- [[08 - Skills/HTML Presentations/Presentation sites|Presentation sites]] — when the artifact is
  **sent rather than presented**. The tabbed format Rick approved on 2026-08-15, its navigation
  contract and its entrance animation set.
- [[08 - Skills/HTML Presentations/Data and media motion|Data and media motion]] — when the
  presentation needs **a chart, a timeline, a headline number or an image**. Carries the rule
  that any unmeasured figure must be visibly tagged as illustrative.

Nothing else loads.

## The build procedure

**Follow it in order. Every step below is settled, so nothing here needs deciding again.**
Where a step has one answer, that answer is stated rather than left as a choice.

### Step 1 — establish the artifact, in two questions

1. **Presented or sent?** Deck, or presentation site. The table above.
2. **Which brand?** **Terracotta unless Rick says otherwise**, and JADS for anything handed to
   the university. Ask if a submission looks likely. The table above.

Then: audience, length, and whether a speaker exists. Nothing else needs asking.

### Step 2 — read

`Core Design` and the chosen brand, then nodes 1 to 3 here, plus
[[08 - Skills/HTML Presentations/Presentation sites|Presentation sites]] if it is a site.

### Step 3 — write the narrative before any markup

**One line per slide, in order, as prose.** An argument that does not survive being read as a
list of sentences will not survive being presented. Do not open an editor until this reads.

### Step 4 — the settled defaults, applied without asking

| | The answer |
|---|---|
| Brand | Terracotta, unless named otherwise |
| Font | **Inter**, embedded from `assets/inter-subset.woff2` as a base64 `@font-face`. No brand overrides it |
| Type scale | The house scale in [[08 - Skills/HTML Presentations/1 Deck architecture\|1 Deck architecture]]. Display 96, H1 56, H2 28, body 21, label 19 |
| Stage | 16:9, 1280 by 720, safe margin 68 px |
| Motion | The house entrance. A deck reveals on slide activation; a site reveals on section entry. Timings in the nodes |
| Icons | `assets/icons/`, applied as CSS masks and tinted to the brand. Only where they carry meaning |
| Charts and images | [[08 - Skills/HTML Presentations/Data and media motion\|Data and media motion]]. **Any unmeasured figure carries a visible "illustrative" tag** |
| Output | One self-contained HTML file. No CDN, no fetched font, no remote image |

### Step 5 — build one of each archetype first

**Look at those before building forty more.** Then fill in the rest.

### Step 6 — verify, and these are the checks that actually catch things

Reading the markup catches none of them.

1. **Exactly one slide visible**, stepped through the whole deck, measured on computed
   `display`. This has shipped broken twice.
2. **Nothing past the safe margin**, measured on every slide.
3. **Every declared size at or above the 19 px floor.**
4. **Contrast computed** for every foreground-on-background pairing the brand uses.
5. **Print to PDF and open it**, one slide per page, backgrounds intact.
6. **No dashes as punctuation**, and no external host referenced anywhere.

### Step 7 — run [[08 - Skills/Core Design/5 Quality checks|5 Quality checks]] and hand over

## Changelog

Feedback is corrected into the node responsible, in the same conversation it was raised, so
this router only ever states current behaviour. What changed and why:
[[08 - Skills/HTML Presentations/HTML Presentations Changelog|HTML Presentations Changelog]].
