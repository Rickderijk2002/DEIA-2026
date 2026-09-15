---
status: active
project: meta
type: guide
subtype: skill-node
description: The tabbed presentation site. A third artifact between a deck and a website, approved by Rick on 2026-08-15 after five rounds of his feedback. Conditional, loads only when the presentation is a link rather than a talk.
last_updated: 2026-08-16 16:40
---

# Presentation sites

**Conditional. It loads only when the presentation is something Rick sends rather than
something he stands in front of.** For a talk, the deck is still the answer and the numbered
nodes govern.

**Approved by Rick on 2026-08-15**, in these words: *"i really like the tabbed site really
great job... this is clean also with the tabs above, the font is clean."* The build he approved
is the reference, named at the bottom of this file.

## Why a third thing exists at all

The skill's hard rule is that **a deck is not a website**, and that still holds. What the rule
was missing is that there is a artifact between them, and Rick found it by refusing to take the
rule on trust. He asked for the web version to be built at full strength so he could judge it,
which was the right instinct.

**What the test settled:**

| | A deck | A presentation site |
|---|---|---|
| Delivered by | a speaker in a room | a link, read alone |
| Driven with | a clicker, no pointer | keyboard **and** a mouse |
| Reader controls pace | no | yes |
| Density | a prompt for speech | can carry the full sentence |
| Wins when | you are presenting | you are sending |

**Neither replaces the other.** A site presented in a room is worse than a deck: reveal motion
means the audience watches a blank panel every time you arrive, and hover effects need a mouse
nobody is holding. A deck emailed as a link is worse than a site: it says too little to read
alone. Ask which one the artifact is before building either.

## The form: tabs, not scroll

**A scrolling version was built first and rejected.** The tab bar won because it makes the
whole argument visible at once: a reader sees there are eight parts, where they are, and can
jump. Scroll snap hides that structure behind a gesture.

- **One fixed bar across the top**, every section listed, numbered from zero, current one
  filled with the accent.
- **One section visible at a time.** Not a long page with anchors. Switching is discrete, so it
  behaves like a deck and reads like a page.
- **A progress bar under the tabs**, width proportional to position.
- Labels are **one word wherever possible, two at most**, and the constraint is measurable rather
  than aesthetic.

> **Every tab label must fit at 1280px wide**, which is the common laptop and the width to design
> against. Measure it: render the label text at the tab's own font and letter spacing, add the
> horizontal padding, and assert it is narrower than `1280 / sectionCount`.

**Worked numbers, so the ceiling is concrete.** At 19px with 0.07em tracking and 11px padding, a
tab holds roughly **9 characters at nine sections**, 11 at eight, 13 at seven. "Core problem" and
"The system" were cut to "Agent" and "System" at eight sections; "Evaluation" had to become
"Measure" when a ninth section was added, because at nine it needed 157px and had 141.

**Adding a section shortens every other label.** That is the real cost of a ninth tab and it is
worth weighing before adding one. **Above nine sections, stop using tabs.**

## Navigation contract

Rick asked for this explicitly, and it is what makes the site usable without a mouse.

- **Arrow keys, both axes.** Right and Down advance, Left and Up retreat.
- **Home and End** reach the first and last section. **Clamped at both ends**, no wrapping.
- **Tabs are clickable**, and every section has a hash so it can be linked directly.
- **The hash is live**, not just a starting point: editing it in the address bar moves the site.
- **Never call `closest()` on an event target without guarding it.** The target can be the
  document, which has no such method, and the whole key handler dies silently. This cost a
  round on 2026-08-15.

## Motion, and it is a small deliberate set

**Four patterns, chosen from a public reference after building all of them side by side and
looking.** The test bench that compared them is kept beside the reference build.

| Pattern | Timing | Fires on |
|---|---|---|
| **Fade and slide up** | 28px, 550ms, `cubic-bezier(.16,1,.3,1)` | Every revealable block. The default |
| **Clip wipe** | `inset(0 0 100% 0)` to `inset(0 0 -12% 0)`, 700ms | Headings only. The one piece of craft |
| **Stagger** | 80 to 90ms between siblings | Lists, cards, stages, in reading order |
| **Parallax** | 12 to 16px against scroll | The title and closing headline only |

Rules that outrank the list:

- **Stagger is reading order, not decoration.** Eyebrow, heading, body, in the order the reader
  takes them. If the stagger does not match the reading order it is noise.
- **Nothing loops, nothing drifts, nothing moves once the section has settled.**
- **Motion fires on section entry and never again**, so moving back and forth does not replay.
- **`prefers-reduced-motion` switches all of it off**, in the stylesheet.
- **Do not add a fifth pattern.** The set is small on purpose; an unvetted flourish is the
  AI-slop signature this skill exists to prevent.

### What was deliberately rejected from the reference

Scroll snap and IntersectionObserver as the *primary* driver, mobile breakpoints as a design
tool, glitch and scramble text, neon glow, and 3D tilt as anything more than a small hover
reward. **Tilt survives only because a site has a pointer**; it never appears in a deck.

## The rule that nearly shipped two blank pages

**Never hide content in the base stylesheet and rely on script to reveal it.** A reveal written
as `opacity:0` plus an observer that adds a class has one failure mode that hides everything,
reports nothing, and looks like a broken file.

- **Gate the hidden state on script being alive:** an inline script sets a `js` class on the
  root, and the rule is written `.js .rv{opacity:0}`.
- **Add a failsafe timeout.** If nothing has been revealed after about a second, reveal it all.

The full statement of this is in
[[08 - Skills/HTML Presentations/3 Deck delivery|3 Deck delivery]], because it applies to any
artifact this skill produces.

## Layout rules that came out of Rick's review

**Both of these were things he saw immediately and I had not.**

- **Every section starts its content at the same height.** Sections were vertically centred,
  so a short section and a long one put their heading in different places and the page appeared
  to jump as he moved through it. **Top-align every section to one padding value.** Verified by
  measuring: the first block sits at the same pixel on all eight, and the six content headings
  are identical. The intro and closing legitimately differ, because they are different
  archetypes.
- **Use an explicit column count where the count is the meaning.** A five-stage pipeline is
  `repeat(5,1fr)`. `auto-fit` wrapped it 4+1 and orphaned the last stage, turning a diagram
  into whatever happened to fit.

## Type

**The house scale from [[08 - Skills/HTML Presentations/1 Deck architecture|1 Deck architecture]]
governs, expressed as `clamp()` because the viewport is unknown.** Ratios hold; the sizes flex.

**One rule Rick had to give twice, so it is written in full.** A long statement under a heading
is **body text one size up, not a second headline**. Set it at the weight, colour and line
height of the lede, and let size alone carry the emphasis:

> *"the font of this text is not very nice, use the same as on slide 2"*

Bolding it and tightening its tracking made it read as a different typeface at a smaller
optical size, because Inter's optical sizing axis genuinely changes the letterforms. **Weight
400, the body colour, line height about 1.4.**

## Icons

**Rick supplied a set on 2026-08-15 and it is installed** at
`08 - Skills/HTML Presentations/assets/icons/`, with a README recording what was kept and what
was refused.

**How they are used, and this is what makes one file work in every palette:** the icons are
monochrome with alpha, so they are applied as a **CSS mask** and filled with a brand colour,
never placed as a coloured image.

> `.ic{width:28px;height:28px;background:var(--accent-fill);`
> `mask:var(--i) center/contain no-repeat}`

- **28 px displayed from a 50 px source.** That is inside its resolution. **Above roughly 40 px
  they go soft**, and the fix is SVG, which the vendor also offers.
- **An icon goes where it carries meaning and nowhere else.** A decorative icon is worse than
  none, and it is the fastest route back to looking generated.
- **Where no icon genuinely fits, use the geometric mark** rather than forcing a near-match.

**Six animated GIFs from the same set were refused.** Each carried 21 to 26 frames of looping
motion, and the motion rule is that nothing loops and nothing moves once a section has settled.
A looping icon competes with the content and reads as clip art. They were also the coloured
two-tone style, which mixes badly with a single-accent palette.

**Attribution is unresolved.** The vendor's free tier requires a visible credit. **Check the
licence before a deck goes to the university or to a Bryn client.**

## How this got good, and it is the transferable part

Five rounds, and **every real improvement came from Rick looking at a render, not from me
reading my own markup.** The pattern worth repeating:

1. **Build it at full strength before judging it.** The scroll version had to exist properly
   before either of us could say the tabbed one was better. A strawman would have proved nothing.
2. **Render and measure, do not reason.** Every defect this artifact had was invisible in the
   source: the blank pages, the jumping alignment, the orphaned fifth stage, the dead arrow keys.
3. **Take a repeated complaint as a rule, not a fix.** The statement type came back twice. The
   second time it went into this file instead of just into the CSS.
4. **When he says a colour looks strange, measure it.** Support blue on the terracotta fill was
   1.92:1 both times he flagged it. He was reading a real contrast failure, not a preference.
5. **Ask what the artifact is for before choosing the form.** Half the reference material was
   irrelevant the moment "presented" versus "sent" was settled.

## Reference build

`03 - School/Thesis/Presentation/Thesis proposal - tabbed site.html` — nine sections, the
approved one, carrying three animated figures chosen from the experiment pages. **Look at it
before building a new presentation site.**

Beside it: `Animation patterns - test bench.html`, the four patterns on identical content, kept
because the next argument about motion should start from a comparison rather than an opinion.
`Thesis proposal - scroll site.html` is frozen, not maintained, and kept only as the losing side
of the test.
