---
status: active
project: meta
type: guide
subtype: skill-node
last_updated: 2026-08-16 16:40
---

# 1 Deck architecture

The physics of a slide deck. **Brand-agnostic**: every rule here holds whether the deck is
JADS blue or something Rick supplies.

Lifted out of the JADS brand profile on 2026-08-10, where it had been filed since
2026-07-31. A comparison slide is an archetype of decks, not of JADS.

## The fixed stage

**A deck has one layout and its dimensions are known at authoring time.** This is the single
fact that forks everything else away from web conventions.

- **16:9, always.** A canvas of 13.333 by 7.5 inches, represented as a 1280 by 720 stage.
- **The stage scales to the viewport; it does not reflow into it.** One transform on the
  container, applied on load and on resize. Content never rearranges itself for a narrower
  window, because a projector is not a phone.
- **A safe margin of roughly 0.7 inches on all sides.** Projectors crop, and the edge of the
  canvas is not the edge of what the room sees.
- Position can be absolute and dimensions can be assumed. That freedom is the compensation
  for everything the fixed stage costs.

## One conceptual unit per slide

**Overflow is a defect, not a scrolling opportunity.** If the content does not fit the stage,
the slide is wrong, and the fix is splitting it rather than shrinking the type.

- **One dominant message per slide.** If a slide needs the word "and" to describe what it is
  about, it is two slides.
- **Leave at least a quarter of the stage empty.** Whitespace here is not restraint, it is
  legibility at four metres.
- **A slide with only a heading and a paragraph is not acceptable**, except where the quote
  or insight archetype specifically calls for a single block of text.

## The density budget

Every slide is checked against this before it is considered done:

| | Ceiling |
|---|---|
| Lines of body text | Roughly 6 |
| Items in a list | 4 |
| Cards or boxes in a row | 4 |
| Stages in a process strip | 5 |
| Distinct focal points | 1 |

**These are ceilings, not targets.** A slide at every ceiling simultaneously is over budget
even though no single number is.

## A speaker exists, and it changes what you write

**The deepest difference between a deck and a page, and it is not technical.** Slide text is
a prompt supporting speech. Web text is the content, read alone.

- **Write the slide to be incomplete.** The sentence the speaker says out loud does not need
  to be on the slide as well.
- **A headline states the conclusion**, and the evidence sits under it. A headline that only
  names the topic wastes the one line everyone reads.
- **Where a deck will be read without a speaker**, say so up front and budget for it. That is
  a different artifact and it needs more words per slide, fewer slides, and speaker notes
  folded into the body.

## Slide structure

- Each slide is one sectioning element in the source, in narrative order. The source reads
  like the talk.
- **Progressive reveal only where the order genuinely matters**: a build that changes what
  the audience understands, not a bullet list appearing one line at a time because it can.
- **Transitions are between slides, never inside them.** Motion inside a slide competes with
  the speaker.

### The house entrance, and it is the only animation so far

**One pattern, used on every slide, set 2026-08-15.** Blocks marked as revealable fade up from
16 px over 420 ms on `cubic-bezier(.22,.61,.36,1)`, staggered 50 ms apart, capped at the first
five blocks. It fires when a slide becomes active and never again.

- **Stagger is not decoration; it is reading order.** The eyebrow, then the headline, then the
  body, in the order the speaker will take them.
- **Nothing loops, nothing drifts, nothing moves after the slide has settled.**
- **`prefers-reduced-motion` switches it off entirely**, in the stylesheet, not in script.

**This is deliberately a small library and Rick intends to grow it.** A vetted set of patterns
is parked in `Active Priorities` for him to go through with JARVIS. Until then, **do not invent
a second animation**: an unvetted flourish is exactly the AI-slop signature this skill exists to
avoid.

## Type on a stage: the house scale

**Rick's decision, 2026-08-15, after seeing the same deck built in four brands.** He picked
the type of the Terracotta build and made it the standard for every presentation. **This scale
is no longer a per-brand choice.** It is deck physics like the 16:9 stage, and it is what makes
two decks a year apart look like the same hand made them.

| Role | Size | Weight | Tracking |
|---|---|---|---|
| Display, title and closing headline | 96 px | 700 | -0.035em |
| Section numeral, on dividers | 132 px | 700 | -0.035em |
| H1, the slide headline | 56 px | 700 | -0.035em |
| H2, card and stage titles | 28 px | 700 | -0.01em |
| Body | 21 px | 400 | normal |
| Label, eyebrow, caption, citation | 19 px | 700 | 0.16em, uppercase |

### The font is Inter, and it ships inside the deck

**Rick supplied the font and approved embedding it, 2026-08-15.** Stack:
`Inter, 'Segoe UI', Helvetica, Arial, sans-serif`, with the face embedded so Inter is
guaranteed rather than hoped for.

**The asset is built and lives beside this skill:**
`08 - Skills/HTML Presentations/assets/inter-subset.woff2`, 51 KB, with `Inter-OFL.txt` and the
codepoint list next to it. Embed it as a base64 data URI in a single `@font-face`, which keeps
the one-file offline rule intact and costs about **68 KB** on the page.

| | |
|---|---|
| Source | Inter variable, `opsz` and `wght` axes, from Rick's own download |
| Subset | Latin-1 plus the punctuation a deck reaches for, 202 codepoints |
| Result | 854 KB of TTF becomes **51 KB** of woff2, a 94% cut |
| Declaration | `font-weight:100 900`, one face covers every weight |
| Also set | `font-optical-sizing:auto` on the body, so 96 px display and 21 px body take the right cut of the axis |

**Every brand uses this face**, JADS included, since Rick overrode the JADS style guide on
2026-08-15. The only reason to omit the embedded font is a deck deliberately built on system
fonts, which costs about 68 KB less and should be a stated decision rather than an oversight.

**Inter runs slightly taller than the system fallbacks**, which pushed the densest slide past
the safe margin when the font was first embedded. The spacing in this skill is now tuned to
Inter. **If the font ever changes, re-run the overflow check rather than assuming it survives.**

**Licensing is part of the decision.** Inter is SIL Open Font Licence, so embedding and sharing
the binary is explicitly permitted, and the licence text ships beside the asset. **Helvetica
Neue was offered and refused**: it is a commercial Monotype face, embedding it is
redistribution, and these decks go to the university and to Bryn clients. **Never embed a
commercial font in a deck that leaves this machine.**

**What makes this scale work is the ratio, not the sizes.** Display sits at roughly 4.5x body
and H1 at 2.7x. That gap is the whole character: a headline that dominates and body text that
stays quiet and readable. Compressing it toward a gentler scale is what makes a deck look
generic, and it is the first thing to resist when a slide feels tight.

**The scale is tight vertically, and the spacing is tuned to it.** A 56 px headline costs real
room, so card padding, body offset and the head rule are set to compensate. **Loosening any of
them overflows the stage.** If a slide does not fit, split it; never loosen the system.

### The floor, which the scale already respects

On a 1280 pixel stage representing 13.333 inches, **1 pt = 1.333 px**, so the 14 pt floor is
**19 px**. Every size above is at or over it, and the label step sits exactly on it.

Chrome that is not part of a slide, such as a page badge, is exempt. Everything a reader is
expected to read is not.

### What a brand may still change

| Fixed, every deck | The brand's to set |
|---|---|
| The type scale and the font stack | Colour, in every role |
| Spacing, the density budget, the archetypes | Radius and shadow, the surface treatment |
| Motion, and the navigation model | Which colour marks the emphasised element |

**Colour is the variable and almost nothing else is.** A brand that wants a different headline
size is asking for a different deck, and the answer is no unless Rick changes this table.

## Alignment inside repeated components

When several cards sit in a row, equal outer height is not enough. **The elements inside them
have to line up across the row**, or the set reads as sloppy even though every box is the
same size.

The usual cause is a title wrapping to two lines in one card and one line in the next, which
pushes that card's divider and body text down relative to its neighbours.

**Fix it by reserving space, not by shortening the text.** Give the repeated title a
minimum height of two lines so every divider and every body block starts at the same
position, whatever the title length. Same for captions in a process strip.

## The traps that have actually happened

**A grid fed more children than it has columns wraps silently.** On 2026-08-01 a
three-column grid received five children, because the connectors between the cards are also
children, and a slide wrapped into a second row and overlapped its own footer. The markup
read correctly.

Count what a container will actually receive, including anything decorative, and render it.
**Draw connectors as pseudo elements**, so a decorative rule can never become a grid child.

**Only the visibility rule may declare `display`. This is the worst bug of 2026-08-15 and it
shipped to Rick twice.** A deck switches slides with `.slide{display:none}` plus
`.slide.is-active{display:block}`. If an archetype also sets `display`, as in
`.title-slide{display:flex}`, the two rules have **equal specificity** and the later one wins
by source order. The archetype comes later, so **that slide is visible on every slide of the
deck**, permanently.

The failure does not look like a visibility bug. Slides are absolutely positioned, so the
last permanently-visible slide in the DOM paints over everything and the deck appears frozen
on it. Arrow keys work perfectly and change nothing the eye can see. Rick reported it as
"I can only see slide 18".

**The rule:** an archetype sets background, colour, `flex-direction` and `justify-content`,
and never `display`. The switch owns visibility alone:

> `.slide{display:none}` · `.slide.is-active{display:block}` ·
> `.slide.is-active.title-slide, .slide.is-active.divider-slide, .slide.is-active.closing-slide{display:flex}`

**Raising the archetype's specificity is not the fix, and was the wrong first correction.**
`.slide.is-active.title-slide{display:flex}` makes the active slide flex correctly while
leaving the bare `.title-slide{display:flex}` in place, so the deck still shows five slides at
once. Both halves are required: add the three-class rule **and** strip `display` from the
archetype.

The same shape of bug hit the visualizer four days earlier from the opposite direction, where a
`display:flex` beat the browser's own `[hidden]` rule. **Whenever visibility and layout are both
expressed as `display`, one of them has to give the property up.**

### The check that catches it, and nothing else does

Counting active classes does not catch this, because exactly one slide has `is-active` the
whole time. **Measure computed `display`, and step the whole deck:**

> For each slide index, advance, then assert that exactly one element matching `.slide` has a
> computed `display` other than `none`, and that it is the expected one.

A contact sheet does not catch it either, because each slide is rendered in its own tile.
Neither does an overflow measurement that forces `is-active` on one slide at a time.

**A theme override is not automatically stronger than the base it overrides.** A brand layer
written as `.title-slide .eyebrow` loses to a base rule of `.slide.on-panel .eyebrow`, so a
theme that inverts one archetype from dark to light keeps the base's white text and prints it
onto a pale ground. Match or beat the base's specificity in the theme layer, then render the
slide that changed.
