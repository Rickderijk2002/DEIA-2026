---
status: active
project: meta
type: guide
subtype: skill-node
last_updated: 2026-09-11 20:30
---

# 2 Pattern library

The components a piece is assembled from. **Read before writing a component**, because inventing
each one fresh is how a build drifts from
[[08 - Skills/Motion graphics/1 Motion rules|1 Motion rules]] without anyone noticing.

**Working implementations of everything below live in `Code-Project\remotion-test\src\`**, built
and rendered on 2026-08-19. That folder is the reference copy; this node says what each piece is
for and where it bites. **Copy from the code, not from prose.**

## The project shape

An entry point registering the root, a root declaring the composition and its duration, frame
rate and dimensions, then scenes, then components, then one theme file. User assets live in a
public folder and are referenced through Remotion's static file helper, never by relative path.

**The theme file is written before the first scene.** Retrofitting one means touching every
component.

## The entrance

The workhorse, and most of a piece is built from it: a spring driving opacity, a rise and a small
scale together, with an optional exit that runs faster than the entrance.

Everything else is this component with different numbers. **Resist writing a second one.**

## Staggered children

The entrance with an increasing delay per child. Three frames for words, four or five for cards,
six for large blocks.

## Word reveal

Text split on spaces, each word its own spring with a per-word offset. The visible result is a
line assembling rather than appearing.

**The gap between words is set in pixels, not em.** An em gap resolves against the parent's font
size rather than the text's own, so a large headline inside an ordinary container gets a gap sized
for body text. This is the single most common spacing bug in the medium.

## The background stack

Three components that turn footage plus type into one picture:

- **The grade:** a soft directional wash in the brand's colours plus a broad darkening toward the
  edges. This is what pulls generated footage into the palette, and it does more work than
  anything else in the stack.
- **The vignette:** a radial darkening, always on top.
- **The grain:** a moving noise field, on top of everything.

*Measured here, and it cost a render:* **grain made of scattered dots is decorative and useless.**
Its real job is dithering. A flat dark plate under a radial vignette bands into visible concentric
rings at eight bits, and ninety scattered dots over a 1920x1080 frame do nothing about it. **A
full-field noise, generated from an SVG turbulence filter as a data URI and blended in overlay,
fixes it.** Reseed it every second frame so it moves like film grain rather than sitting there as
a static texture.

The rings were invisible in the source and obvious in the first extracted frame.

## Animating on top of a photograph, and keeping it locked

**The method, and it is the whole trick:** work in the photograph's own pixel coordinates, not in
the frame's.

Put the image and every drawn element inside **one wrapper**, scale that wrapper to cover the
frame, and position the drawn elements in the image's native pixel space. Then a push, a pan or a
breath moves everything together and the drawn elements stay welded to the picture.

**Positioning drawn elements in percentages of the 16:9 frame instead is the trap.** A photograph
cropped to cover is not aligned with the frame, so anything placed against the frame drifts the
moment the wrapper scales, and a droplet that has to land exactly on a cup's surface lands
somewhere else.

*Measured here, on the coffee hero:* one wrapper, the image at its natural 1402x1122, ripples
placed at measured pixel coordinates, and a slow push over the whole thing. The landing point held
across the entire render.

**Clip effects to the shape they belong to.** Ripples on a liquid surface go inside a container
shaped like that surface with overflow hidden, so a ring can never expand across the rim onto the
porcelain. Falling objects stay outside the clip, because they are above the surface rather than
on it.

**The honest limit of this technique:** drawn effects sit *on top of* the photograph and do not
deform it. A real ripple refracts what is under it; this one is a ring over a static texture. It
reads well in motion and it is not simulation. Displacing the underlying pixels is possible and
has not been done here.

## Ken Burns

A slow scale and drift on any still. Also worth applying to footage, gently, on top of whatever
the footage already does: it hides the fact that a five second clip is short.

## Multi-clip finishing lives elsewhere now

**Moved to [[08 - Skills/Video editing/0 Video editing|Video editing]] on 2026-09-11**, with Rick's
approval. The one-master principle, the fault-to-repair taxonomy and the rule against padding a
timing correction are that skill's values node, and the measurement commands are its protocol.

**What stays here is the authoring half.** When a diagnosed join needs motion no take contains, that
skill specifies the repair and this one builds it, from the entrance, the background stack and the
breathing components above. A finishing composition is a legitimate use of this skill; deciding where
its cuts go is not.

## Breathing

A slow sine on scale, small enough to be subliminal. Applied to anything that would otherwise sit
still for more than two seconds.

## Counters, transitions, parallax

In the source library and **not yet used by us**. They exist; nothing here has run them, so
nothing is claimed about them.

## Captions over speech

Word timestamps come from a transcription pass, then each caption group renders in its own
sequence with the active word highlighted.

**Untried.** Written down so a future session knows the route exists rather than inventing one.

## Fonts

**Never rely on a system default for hero text.** Load a real display face, either through
Remotion's font package or an embedded file.

*Measured here:* the test build used a system face deliberately, to keep the test about motion
rather than about typography. It is the weakest part of that render and it shows.
