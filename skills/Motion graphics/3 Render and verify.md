---
status: active
project: meta
type: guide
subtype: skill-node
last_updated: 2026-09-11 20:30
---

# 3 Render and verify

How a piece gets rendered and how it is proved. **Read before the first render.**

## What the machine already has

Verified 2026-08-19 on Rick's PC: **Node 24.19 and npm 11.17**, and **ffmpeg** on the path from a
winget install. Remotion installs into the project and brings its own Chromium.

**Nothing here needs a GPU and nothing here costs money.** That is the whole reason this skill sits
beside [[08 - Skills/Rented compute/0 Rented compute|Rented compute]] rather than inside it: a pod
is a meter, and this is not.

*Measured here:* 200 frames at 1920x1080 rendered in **about a minute**, twice, including the
re-render after a fix. The iteration loop is seconds to minutes, against twenty five minutes a
clip on a rented GPU.

## The render

One command renders the composition to mp4. Two settings worth deciding rather than defaulting:

- **Quality with headroom.** Anything destined for a platform gets recompressed on upload, so
  render generously and let their pass be the only lossy one.
- **Overwrite explicitly.** Forgetting it and then inspecting the previous file is a real trap,
  and it presents as "my fix did nothing."

Heavy transparency and blur stacks want a lossless intermediate image format; ordinary work does
not.

## The verification loop, which is the point of this node

**Render, extract frames, look at them, fix, re-render, look again.** Nothing is shown to Rick
before a clean pass.

Two ways to get frames, and they prove different things:

- **Remotion's own still command** renders one exact frame directly from the composition. Portable,
  needs no system ffmpeg, and it is the right tool while iterating on the design.
- **ffmpeg seeking into the finished file** proves the encode as well as the design, because it
  looks at what actually shipped. Seek by time rather than by a frame-select filter; the filter's
  quoting breaks in some shells.

**Extract at least four frames spread across the piece**, including one inside every entrance and
one on the final state.

### What to look for, in the order things actually go wrong

1. **Spacing bugs**, especially em-based gaps around large type.
2. **Text touching an edge**, or outside the safe area in vertical formats.
3. **Elements visible before their entrance or after their exit**, which means a missing clamp.
4. **Banding on flat or near-flat areas**, which is a dithering problem rather than a colour one.
5. **Layer order**, grain and vignette on top, grade above content.
6. **Contrast failures** where dim text sits over the grade.
7. **Anything to do with joins, freezes or the delivered file's endpoints.** Frozen runs,
   untreated discontinuities and audio finishing past the picture are all
   [[08 - Skills/Video editing/2 Edit protocol|Video editing]]'s checks, with the measurement commands
   that find them. Moved there 2026-09-11 rather than kept in both places. **If the piece being
   rendered assembles clips at all, that skill's checklist runs as well as this list.**

*Measured here:* items 4 and 1 are the two that actually occurred on the first real build. Neither
was visible in the source.

## Traps already paid for

### A still frame is not evidence about motion, and a correct file is not evidence about design

Both halves matter. The first hammer clip generated on a pod had an excellent opening frame and
was unusable in motion. The first Remotion render was a valid mp4 of exactly the right length with
a visible artefact through the whole end card.

**Look at moving output, and look at several frames of it.**

For an assembled performance the complete watch against the master audio is required, and it belongs
to [[08 - Skills/Video editing/0 Video editing|Video editing]] along with the rest of the join
checks. Frame extraction finds black frames, freezes and discontinuity spikes; only the complete
watch decides whether a reaction cutaway or transition feels natural.

### Motion graphics cannot rescue bad footage

*Measured here, and it is the most useful thing this build proved.* Grading, grain, a vignette and
typography made a rejected clip look like a considered asset. **They did not fix the camera drift
or the subject leaving frame.** The flaws were dressed, not removed.

The consequence for planning: this skill raises what a good take is worth, it does not lower the
bar on generating one.

### A test build must announce that it is a test

When a piece is made for a third party who has no brand profile yet, **do not invent their brand
to fill the gap.** Sample a placeholder palette from the footage, and say on screen that it is a
technique test. A convincing-looking asset with an invented brand is the thing that later gets
mistaken for approved work.

## Where output goes

The project folder under `Code-Project\`, with renders in its own output directory, and **that
directory is git-ignored** along with every other generated media folder. The source, the theme
and the components are text and stay tracked.
