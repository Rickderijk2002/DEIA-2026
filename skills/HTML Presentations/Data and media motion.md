---
status: active
project: meta
type: guide
subtype: skill-node
description: Animating data, time and images in a presentation. Charts that draw, timelines that assemble, particles that resolve, and how to place a supplied picture. Conditional, loads when a presentation needs a chart, a timeline or an image.
last_updated: 2026-08-16 16:40
---

# Data and media motion

**Conditional.** Loads when a presentation needs a chart, a timeline, a headline number or an
image. Applies to both a deck and a
[[08 - Skills/HTML Presentations/Presentation sites|presentation site]]; only the trigger differs,
slide activation in one, section entry in the other.

**Built 2026-08-16** on Rick's instruction to stop animating blur and sideways slides and start
animating things that mean something. Reference builds, both in `03 - School/Thesis/Presentation/`:
`Animation experiments - data and media.html`, seven chart and media experiments, and
`Animation experiments 2 - diagrams.html`, six diagram and timeline experiments. Every one
carries a verdict.

## The rule that outranks everything else here

**Any figure that is not measured carries a visible tag saying so.**

A chart is the easiest place in a presentation to imply evidence that does not exist, and a
thesis proposal is the worst possible place to do it by accident. **A placeholder chart with no
tag is a fabricated result**, whatever was intended. The tag is a small dark label reading
*"Illustrative figures, not measured"*, sitting inside the chart frame where it cannot be
cropped away in a screenshot.

**Real data never gets the tag**, and the difference should be visible at a glance. The proposal
timeline carries real dates and is deliberately untagged.

## Start here: choose the form from the content

**This is the step that makes the rest reusable.** Given a body of content that has nothing to do
with any previous presentation, read what the content *is* and the form follows. Do not start
from the patterns and look for somewhere to use them.

| When the content is | Use | Because |
|---|---|---|
| Quantities compared across a few named things | **Bar chart**, grown from the axis | Length is the most accurate comparison a human eye makes |
| One value moving over time | **Line drawn along its path** | The drawing *is* the direction |
| A single number that is the whole point | **Counter** | It earns the attention it takes |
| A share of a whole, at two values | **Ring** | Arc reads as proportion. Four rings read as nothing |
| Dated milestones | **Timeline**, and pick the treatment from the table below | |
| Something transformed step by step | **Pipeline with a travelling payload** | Shows accumulation, not just sequence |
| Things that contain or wrap each other | **Nested shells** | Argues containment, which a list cannot |
| A cycle that returns to where it began | **Closed loop with direction arrows** | The closing is the claim |
| Disorder becoming order | **Particle sort into labelled groups** | States a problem and its solution in one gesture |
| Two options weighed against each other | **Two matched columns**, the recommendation marked | |
| A claim with no data behind it | **Words.** No chart | A chart implies measurement. If there is none, do not draw one |

**Budget: roughly three animated figures in a presentation, and one of them is the opener.** More
than that and it becomes a showreel, the audience starts watching the motion instead of the
argument, and every figure loses the emphasis it was given.

**One idea per figure.** If a diagram needs two sentences to explain what it shows, it is two
diagrams or it is a table.

## The patterns, with what each one is for

| Pattern | Timing | Use it when |
|---|---|---|
| **Bar chart, grown from the axis** | 900ms, stagger 110ms, values count in step | Comparing quantities. **The strongest of the set** |
| **Line drawn along its path** | `stroke-dashoffset` 1.4s, area fades in 550ms behind | Anything over time. Slower on purpose |
| **Number counting up** | 1.1s ease-out, stagger 140ms | One number that is the point of the slide |
| **Progress ring** | sweep 1.1s from twelve o'clock | A proportion of a whole, at two values, never four |
| **Timeline on a rail** | rail 1.2s, then steps stagger 180ms | A plan or a sequence of dates |
| **Particles that assemble** | 3.0s settle, then still | Once per deck, when disorder becoming order *is* the argument |

### The rules inside the patterns

- **Grow a bar from the axis, never fade it in.** A bar that fades carries no direction and says
  nothing about magnitude. The growth is the information.
- **Draw the rail before the dots land.** Reversed, the milestones look scattered rather than
  scheduled.
- **A counting number demands attention, so a slide with four of them has none.** Note the
  strongest use is counting to **zero**: it lands harder for having moved.
- **The area fill follows the line by about half a second.** Together they read as a blob;
  sequenced they read as a trend.
- **Particles must resolve and stop.** Ambient drifting particles are pure slop and are banned by
  the motion rule. This one survives only because it settles into order and then holds still. **If
  it looped it would be decoration.**

## The bug that made the chart lie

**Found 2026-08-16, and worth the whole node on its own.** The bars were flex children with a
percentage height, alongside a value and a label in the same column. **Flex clamped the fill to
whatever space the text left**, so 74% and 85% both rendered at 171px out of 250. Two different
numbers drew as the same bar.

**Nothing looked wrong.** The chart was handsome, the labels were right, and the picture was
false.

**The fix, and the rule:** the fill is absolutely positioned inside a plot area of known height,
so its percentage is of the plot and nothing can compress it. The value rides on top of the fill,
the label hangs below the plot, and neither takes height from the bar.

> **Measure the rendered bar heights against the ratio they claim.** For each bar, assert
> `height ≈ plotHeight × value / scaleMax`, and assert that distinct values produce distinct
> heights. It takes one probe and it is the only check that catches a chart drawing the wrong
> shape.

## Diagrams that argue

**Round two, 2026-08-16.** Rick asked for the stock illustration to be replaced by diagrams drawn
in brand. Three were built, and each one says something a bullet list cannot. Reference:
`Animation experiments 2 - diagrams.html`.

| Diagram | The thing it argues | Motion |
|---|---|---|
| **Pipeline with a travelling payload** | Something specific is accumulated, in order, and one stage is where the work happens | Stages land, then a payload crosses gaining a ring at each stage that adds to it |
| **Nested shells** | The items are not a list, they are wrappers, and the centre is never delivered bare | Core first, then shells outward, 180ms apart |
| **Closed loop** | The circuit completes, which is the whole contribution | Path draws, nodes land, then a pulse travels the full circuit |

### The rules these produced

- **A loop diagram without direction arrows is not a loop.** Four boxes joined by lines read as
  four boxes. One arrow per leg, landing after the nodes, is what makes the circuit legible.
  This was missed on the first build and was obvious the moment it was rendered.
- **Let a loop pulse run exactly twice.** Once reads as an accident, twice reads as a loop, three
  times is a screensaver.
- **Five shells is the ceiling** on a nested diagram. A sixth is unreadable from the back of a
  room.
- **Label a nested shell with a halo, not on the line.** `stroke:#fff; stroke-width:7;
  paint-order:stroke` lifts the text clear of the border it sits on.
- **Never let the core repeat one of the wrappers.** The first build nested "The task" inside a
  layer also called "Task". The centre is the thing being wrapped, so it is the raw request.

### Unorganised becoming organised

**Rick's own idea and the strongest single thing here.** Fragments arrive scattered, drifting and
indistinguishable, then sort themselves into the named layers. **Colour only arrives once a
fragment knows where it belongs**, so the palette itself carries the argument.

**It is the opening slide.** It states the problem and the solution in one gesture with no words,
then settles and stops. **The settling is what makes it legal** under the motion rule.

## Timelines: three treatments, and they are not interchangeable

| Treatment | Wins when |
|---|---|
| **Horizontal rail** | A fixed stage. Width is available and there is no scroll |
| **Vertical rail** | A site or a handout. Each milestone gets a real sentence, and it scales past four |
| **Phase bars** | The plan slide. **Duration and overlap, not dates** |

**Prefer phase bars for anything a supervisor reviews.** The real question is whether phases are
long enough and where they overlap, and only that shape answers it.

**Mark today, and let it be unflattering.** On the proposal plan the marker sits before the first
bar, so the diagram states plainly that nothing has started. **A plan diagram that hides where you
actually are is decoration.**

## Every animated element needs a defined rest state

**Added after the loop pulse parked on top of a label** when motion was reduced. An element whose
position only exists inside an animation has no correct place to sit when the animation does not
run, and reduced motion is not the only case: a print, a screenshot and a paused deck all land
there.

**Check every animated element with motion disabled**, and give it either a sensible resting
position or `opacity:0`. Note the specificity trap: a rest rule written as `.demo .thing` loses to
`.demo.play .thing`, so it needs equal weight or `!important`.

## Images

**Compress before embedding, and the saving is not marginal.** The supplied example was
1536px and **1722 KB**; at 1100px wide and JPEG quality 80 it is **92 KB**, a 95% cut with no
visible loss at presentation size. **Anything over about 150 KB in a deck has not been
processed.**

- **1100px wide is enough** for a full-width figure on a 1280 stage or a web section.
- **Fix the frame, never the image.** Give the container an aspect ratio and use `object-fit`, so
  the layout cannot shift when the picture loads.
- **Caption it with provenance.** Where it came from, and whether it was made for this deck.
- **Reveal it with the house clip wipe**, not a fade, so it matches everything else on the page.
- **A full-bleed illustration with text baked into it does not crop.** The example lost its own
  wordmark to a 3:2 frame. Prefer images with quiet edges, or do not crop them.

### The judgement Rick should hear when an image is supplied

**Rick supplied a stock-style AI illustration on 2026-08-16: a glowing robot, neon blue, generic
AI iconography.** It was integrated so he could judge it in context, and the recommendation was
against shipping it:

- **It is the cliche the brand explicitly rejects.** `Rick - takes` names robot heads, generic AI
  symbols and neon bloom as things to avoid, and this is all three.
- **It fights the palette.** Cool neon blue against warm paper and terracotta, on the same page.
- **It carries illegible baked-in text.**

**What to use instead: a diagram drawn in brand that says something the words do not.** The car
wash model, the five context layers and the feedback loop are all better as drawn diagrams than
as any stock picture. **An illustration that decorates is worth less than a diagram that argues.**

## Where the patterns came from

Two public references, neither adopted wholesale:
`github.com/zarazhangrui/frontend-slides` for the entrance and background vocabulary, and
`github.com/neonwatty/css-animation-skill` for the self-contained, CSS-first, no-dependency
approach and its point that a coded animation stays sharp, stays small and stays editable in a
way a GIF does not.

**Both were treated as menus, not recipes.** What transferred was technique; what was rejected
was every effect that needed a scrollbar, a mouse, or a reason to exist.
