---
status: active
project: meta
type: guide
subtype: skill-node
last_updated: 2026-09-11 20:30
---

# 1 Motion rules

The non-negotiables. **Code quality is not what makes a video look cheap; motion craft is.**
Untrained generation produces linear easing, lone fades, everything entering at once, flat
backgrounds and no texture. That combination is the look people mean by "AI made this."

Adapted from the source skill named in
[[08 - Skills/Motion graphics/0 Motion graphics|the router]]. The entries marked *measured here*
are ours.

## The rules

### Never linear

Every interpolation carries an easing curve, and every entrance prefers a spring. **Always clamp
at both ends**, or elements are visible before they enter and after they leave.

Linear motion does not exist in the physical world, and the eye knows it immediately without
being able to say why.

### An entrance moves two or three properties together

Opacity plus a rise plus a small scale. **A lone fade is forbidden.** One property changing reads
as a slideshow transition; three reads as an object arriving.

### Stagger everything

Nothing enters simultaneously. Three frames between words, four or five between cards, six
between large blocks. Simultaneous entrance is the single loudest tell.

### Exits exist, and they are faster than entrances

Roughly half the duration. Things arrive with weight and leave with dispatch. **An element that
simply disappears is a bug the viewer feels and cannot name.**

### Five layers in every scene, bottom to top

Background, then assets, then graphics and type, then the colour grade, then grain and vignette.

**Never a flat solid background**, and the grade sits above the content rather than under it,
which is what makes footage and graphics read as one picture rather than as a sticker on a photo.

### Stills get a slow push, footage gets the right component

Any still image gets a slow scale and drift, or it reads as a dead frame. Video uses Remotion's
off-thread video component rather than the plain one.

*Measured here:* a 16fps source on a 30fps timeline is fine. Remotion seeks by time, not by frame
index, so a mismatch needs no conversion. A 1280x720 clip upscaled into a 1920x1080 composition
also held up, though the upscale is visible on fine texture.

### Anything on screen longer than two seconds breathes

A slow sine on scale or position, small enough that nobody notices it directly and everybody
notices its absence. Frozen elements read as a stalled render.

### All timing derives from the frame rate

Never a magic frame number. A composition whose numbers are hardcoded to 30fps breaks the day it
is asked for 60.

### A render is deterministic, or the verification loop is a lie

**No unseeded randomness in a composition.** Nothing reads the wall clock, nothing calls an
unseeded random number generator. Any pseudo-randomness is seeded from the frame or element index so
the same frame renders identically every time.

The reason is the hard rule rather than tidiness. **Render, fix, re-render only proves something if
the two renders are comparable.** When frames differ between runs for reasons unrelated to the fix,
a real regression and ordinary noise look the same, and the loop that this whole skill depends on
stops being evidence.

*Adopted 2026-09-11* from `video-shotcraft` by Vincentwei1021, Apache-2.0, which enforces the same
rule for the same reason. **Our grain reseeds per frame by design**, which is correct film-grain
behaviour and is exactly the kind of motion that must be driven from the frame index rather than
from chance.

### One theme object

Colours, easings, springs and fonts in one file, imported everywhere. **No hex value and no easing
curve ever appears inline in a component.** The colours themselves come from the brand, through
[[08 - Skills/Core Design/0 Core Design|Core Design]], never from this skill.

### Render, extract, look, fix, re-render

The hard rule from the router. It is a rule rather than a habit because the failures it catches
are invisible in source code.

## Pacing, which is where amateur and expensive separate

**Contrast is the whole technique: a fast move, then complete stillness, then the next move.**
Constant motion reads cheap. Holds are a design tool, not dead air.

**A composed hold is not a frozen join.** Stillness inside a living shot retains breathing motion,
camera texture and audio intent. Repeating one identical frame at a boundary reads as a stalled
render. A freeze may support a short dissolve underneath; it must not become the visible bridge.

- **Something moves inside the first fifteen frames.** A static opening is a stalled video.
- **A new visual element at least every three seconds**, or attention leaves.
- **At least three genuine moments of stillness** across a short piece.
- **Vertical video keeps critical text inside the middle three quarters**, because platform
  interface elements cover the top and bottom.

## What this skill does not decide

**Palette, typography and whether the thing is on brand.** All of that is
[[08 - Skills/Core Design/0 Core Design|Core Design]], in every medium, and duplicating it here
would create a second authority that drifts.

The one motion-specific colour rule worth stating, because it is about the frame rather than the
palette: **at most one element glows or carries the hero colour in any given frame.** An accent
on everything is not an accent, and two glowing objects read as a fairground.

## Failure modes that are worth naming

- **Emoji used as icons.** They render as full-colour platform glyphs that ignore the palette
  entirely and sit on whatever background they were given. Draw the mark instead.
- **One giant component** instead of themed reusable pieces. It cannot be adjusted later without
  re-reading all of it.
- **Composition duration not matching the content**, which ships dead air at the end.
- **Forgetting to overwrite on a re-render**, then inspecting the stale file and concluding the
  fix did not work.
- **Describing the result instead of rendering it.** The rule against this is the router's hard
  rule, and it is the one most easily rationalised when time is short.
