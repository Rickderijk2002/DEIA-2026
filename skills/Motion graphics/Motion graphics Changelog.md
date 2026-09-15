---
status: active
project: meta
type: log
subtype: skill-changelog
last_updated: 2026-09-11 20:30
---

# Motion graphics — changelog

Never part of the read order. It exists so a later session understands why a rule is the way it
is before being tempted to revert it.

<!-- newest first: add new entries directly below this line -->

**2026-09-11 — the edit was split out into [[08 - Skills/Video editing/0 Video editing|Video
editing]], with Rick's approval.** This skill had grown two jobs in one folder: authoring frames from
code, and deciding where the cuts in existing footage go. The second had no door of its own, so
"make this video flow naturally" had nothing to open, and the finishing method sat in a pattern
library beside the entrance component.

**What left:** the multi-clip finishing section of `2 Pattern library`, and the frozen-join,
discontinuity and audio-endpoint checks from `3 Render and verify`. Both now carry pointers rather
than copies, because two authorities on one method is the drift the no-bloat rule exists to stop.

**What stayed, and why the split is not a demotion:** this skill still authors any motion a repair
needs, and a finishing composition is still a legitimate thing to build here. The boundary is stated
in the router from both sides: that skill decides the cut, this one authors the frames, and they run
together often.

**One rule was added in the same pass**, from the audit of `video-shotcraft` that produced the new
skill: a render must be deterministic, because the render-fix-re-render loop is only evidence if two
renders are comparable. That closed a gap nothing in the vault had covered.

**2026-09-11 — natural multi-clip finishing added after Hapopy song 2 v04 was approved.** v03 had
removed 2.417 seconds from a delayed action and inserted the same time as a frozen bridge, leaving
the cue unmoved and the join visibly stalled. v04 proved the replacement: accelerate only the
anticipation, rejoin at natural speed, recover duration with moving reaction footage, and choose a
transition from the actual discontinuity rather than applying one zoom punch everywhere. The
verification node now requires static-run detection, discontinuity inspection and delivered-file
audio endpoint checks. Rick approved the result as natural on the first v04 review.

**2026-08-19 — skill created, after the test rather than before it.** Rick found
`claude-remotion-skill`, an MIT-licensed Claude skill by haidrrrry for building motion graphics in
Remotion. It was read in full, cloned and inspected, then **tested before a single line of skill
was written**, on the principle the vault already applies to models and runtimes: a thing earns its
node by working.

**The test:** the second Wan hammer clip, the one judged unusable, put through a grade, grain, a
vignette, staggered typography and an end plate. Built and rendered twice in about fifteen minutes
on Rick's own machine, at no cost. Project in `Code-Project\remotion-test\`.

**Why its own skill rather than a node somewhere.** The deliverable is a rendered file. That makes
it a fourth output domain alongside `Data Apps`, `Interactive Websites` and `HTML Presentations`,
with the same shape: `Core Design` settles the brand, then the domain builds the thing. Folding it
into `Interactive Websites` would have been wrong twice over, since `5 Hero footage` is about
footage feeding a scroll-driven page and this makes standalone video.

**What was deliberately not taken.** The source skill's colour and typography rules, which
duplicate [[08 - Skills/Core Design/0 Core Design|Core Design]] and would have created a second
visual authority in the vault. Its example palettes are worse than redundant: one of them is
Anthropic's own brand, and it must never become a default in Rick's vault. Only what is specific
to motion in time was kept.

**What the test measured that the source did not say:**

- **Grain made of scattered dots does not dither.** The first render banded into visible
  concentric rings across the flat dark end plate under the vignette. Ninety dots over a 1920x1080
  frame do nothing. A full-field SVG turbulence noise blended in overlay fixed it. **The bug was
  invisible in the source and obvious in one extracted frame**, which is the whole argument for
  the verification rule.
- **Motion graphics cannot rescue bad footage.** The grade genuinely tamed the clip's blown
  highlights and pulled it into a palette. It did not fix the camera drift or the hammer leaving
  frame. This raises what a good take is worth rather than lowering the bar on generating one.
- **200 frames at 1920x1080 render in about a minute** on Rick's PC, against twenty five minutes
  for one five second clip on a rented 4090.
- **A 16fps source drops onto a 30fps timeline with no conversion**, because Remotion seeks by
  time.

**The restraint that mattered.** Bouwservice Ben de Rijk has no brand profile, and their own plan
says one is written before the first pixel. The test therefore used a palette sampled from the
footage and says on screen that it is a technique test, so it can never be mistaken later for an
approved asset.

**Left open and stated rather than skipped:** sound, which the source skill treats as half of
perceived quality and which nothing here has produced; counters, transitions and parallax, which
exist in the library and have not been run; and captions over speech, which is written down as a
route rather than a measurement.
