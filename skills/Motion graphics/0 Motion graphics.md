---
status: active
project: meta
type: guide
subtype: skill-router
description: Build a rendered video: a promo, an intro or outro, a logo sting, kinetic typography, captions over footage, or a finished edit of clips we generated. Built in Remotion, React rendered frame by frame to mp4. Fires when the deliverable is a video file rather than a page.
last_updated: 2026-09-11 20:30
---

# Skill: Motion graphics

The router. Trigger, hard rule, how it differs from its neighbours, read order.

Created 2026-08-19, **after** a working test rather than before one. A rejected five second
generated clip was graded, grained, titled and rendered on Rick's own machine in about fifteen
minutes, and the result is in `Code-Project\remotion-test\`.

## When this fires

**The deliverable is a video file whose pictures have to be authored.** A promo, a social short, an
intro or outro, a logo sting, kinetic typography, captions burned over footage, a grade over a plate,
or motion for a join that no existing take contains.

**It never fires alone.** [[08 - Skills/Core Design/0 Core Design|Core Design]] is read first and
settles the brand, exactly as it does for the other output domains.

## It does not fire for

| Situation | Skill |
|---|---|
| **Footage that already exists and has to play as one piece**: joins, freezes, pacing, aligning to an audio master, proving an export | [[08 - Skills/Video editing/0 Video editing\|Video editing]] |
| A web page whose hero is driven by scrolling | [[08 - Skills/Interactive Websites/4 Cinematic hero\|4 Cinematic hero]] |
| Generating the footage itself, on a rented GPU | [[08 - Skills/Rented compute/4 ComfyUI pods\|4 ComfyUI pods]] |
| Designing the shot that gets generated | [[08 - Skills/Interactive Websites/5 Hero footage\|5 Hero footage]] |
| A deck, even an animated one | [[08 - Skills/HTML Presentations/0 HTML Presentations\|HTML Presentations]] |
| A local screen over a running system | [[08 - Skills/Interface build/0 Interface build\|Interface build]] |

**The line against [[08 - Skills/Video editing/0 Video editing|Video editing]] is the one that
matters most, because both skills touch the same files and both can involve Remotion.** The question
is never which tool is used. It is what is being decided:

- **That skill decides the cut.** Where a join goes, what the fault actually is, whether picture and
  audio agree, whether the exported file is sound.
- **This skill authors the frames.** Anything that does not exist in a take yet.

**They run together often and that is correct.** The Hapopy song 2 v04 finish was decided there and
built here. When Rick says a video should flow naturally, that skill opens first and calls this one
when a repair needs motion authored. What must not happen is either skill deciding the other's half.

**The line against `4 Cinematic hero` is worth stating too.** That archetype outputs a
web page a visitor scrubs with their scroll wheel. This outputs a file that plays. Same footage
can feed both; they are not the same deliverable and they do not share a build.

## The hard rule

**Render it, extract frames, look at them, fix, render again. Nothing is delivered unverified.**

This is not a formality, and it earned its place on the first build. The first render carried
visible banding rings across a flat dark plate. **The code was correct and the bug was invisible
in it.** One extracted frame showed it immediately.

Rick's rule 1 already says evidence only, never guess. In this medium the evidence is a picture of
the actual output, and nothing else counts. **A description of a video is not a video.**

## Where this came from

**Adapted from the MIT-licensed `claude-remotion-skill` by haidrrrry**, which Rick supplied on
2026-08-19, read in full and translated rather than installed. Two deliberate departures:

- **Its colour and type rules are dropped.** [[08 - Skills/Core Design/0 Core Design|Core Design]]
  owns palette and typography across every medium, and a second authority is exactly the
  duplication the vault's no-bloat rule exists to stop. What is kept here is what is specific to
  motion **in time**: pacing, holds, entrances, layer order, verification.
- **Its example palettes are not reusable.** One of them is Anthropic's own brand. Nothing in this
  skill supplies a colour; the brand does.

## Read order

1. [[08 - Skills/Motion graphics/1 Motion rules|1 Motion rules]] — the non-negotiables, and the
   reasons they exist. Always, and first.
2. [[08 - Skills/Motion graphics/2 Pattern library|2 Pattern library]] — the components to build
   from, rather than inventing each time. Always, before writing a component.
3. [[08 - Skills/Motion graphics/3 Render and verify|3 Render and verify]] — the render command,
   the verification loop and the traps already paid for. **Before the first render**, not after
   something looks wrong.

Plus the brand, from `Core Design`. Nothing else loads.

## The shape of a job

1. **Scope it:** duration, frame rate, dimensions, and what assets already exist.
2. **Read `Core Design` and settle the brand.** If the subject is a third party without a brand
   profile yet, that profile is written first; a placeholder palette sampled from the footage is
   for tests only and gets labelled as such.
3. **Write the theme file first.** One object holding colours, easings and springs. No hex value
   and no easing ever appears inline in a component.
4. **Build scenes from the pattern library.**
5. **Render, extract, look, fix, re-render.**
6. **Deliver into the project folder** under `Code-Project\`, never a temp directory.

## Changelog

[[08 - Skills/Motion graphics/Motion graphics Changelog|Motion graphics Changelog]].
