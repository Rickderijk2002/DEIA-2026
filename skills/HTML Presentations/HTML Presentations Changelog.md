---
status: active
project: meta
type: log
subtype: skill-changelog
last_updated: 2026-08-16 16:40
---

# HTML Presentations — changelog

Append-only. History and reasoning for
[[08 - Skills/HTML Presentations/0 HTML Presentations|HTML Presentations]] and its
nodes.

**The node gets edited first. This file only records that it happened, and why.** Reading it
is never required to behave correctly; it exists so a later session understands why a rule is
the way it is.

<!-- newest first: add new entries directly below this line -->

**2026-08-16 (third) — the skill audited for reusability, and three figures shipped.** Rick's
test for the skill, stated plainly: **in a month, given an entirely different context, reading
the skill should be enough to build a good presentation without rediscovering any of this.**

**The gap that audit found was the first step, not the last.** Every pattern was documented but
nothing said *which* pattern a given piece of content wants.
[[08 - Skills/HTML Presentations/Data and media motion|Data and media motion]] now opens with a
content-to-form table: quantities take bars, a value over time takes a drawn line, containment
takes nested shells, a cycle takes a closed loop, disorder becoming order takes a particle sort,
and **a claim with no data behind it takes words and no chart.** With a budget of roughly three
animated figures, one of them the opener.

**Also corrected in the audit:** `1 Deck architecture` still said a JADS deck renders Arial,
which Rick's font override made false the day before.

**Shipped into the reference build:** the vertical timeline, the pipeline with a travelling
payload, and the nested shells, as a ninth section was added for the plan.

**Which produced a measurable rule for tab labels.** Adding a ninth section made "Evaluation"
overflow at 1280px: it needed 157px and had 141. The node now states the check as arithmetic,
label width against `1280 / sectionCount`, with the worked ceiling of about nine characters at
nine tabs. **Adding a section shortens every other label**, and above nine sections tabs stop
being the right control.

**2026-08-16 (second) — diagrams that argue, and the loop that was not a loop.** Rick asked for
the stock illustration to be replaced by diagrams drawn in brand, for his particle idea built
properly, and for more timeline options. Six more experiments, and the keepers are now in
[[08 - Skills/HTML Presentations/Data and media motion|Data and media motion]].

**Three diagram patterns, each carrying an argument a list cannot.** A pipeline with a payload
that gains a ring at every stage that adds to it. Nested shells, which argue that the layers are
wrappers rather than items. And a closed loop, where the circuit completing *is* the
contribution.

**The find worth the round: a loop diagram with no direction arrows is not a loop.** It renders as
four boxes joined by lines, and the one thing the diagram exists to say is the one thing it fails
to say. Arrows now land after the nodes, one per leg.

**Two more caught by rendering.** A nested diagram had its labels sitting on the shell borders,
fixed with a white halo via `paint-order:stroke`. And the core repeated one of its own wrappers,
nesting "The task" inside a layer called "Task"; the centre is the thing being wrapped, so it is
the raw request.

**A general rule came out of the loop pulse:** every animated element needs a defined rest state,
because reduced motion, a print, a screenshot and a paused deck all land there. The pulse parked
on top of a label. Includes the specificity trap, since a rest rule at `.demo .thing` loses to
`.demo.play .thing`.

**Timelines are now three treatments rather than one**, with when each wins: horizontal on a
stage, vertical on a site, phase bars for anything a supervisor reviews. **Phase bars carry a
today marker that is allowed to be unflattering**, and on this plan it sits before the first bar.

**2026-08-16 — motion that shows data, and the chart that lied.** Rick asked for animation that
carries meaning rather than blur and sideways slides: charts drawing themselves, a timelapse over
the proposal's dates, particles, and a worked example of placing a supplied image. Seven
experiments built, each with a verdict, and the keepers written into
[[08 - Skills/HTML Presentations/Data and media motion|Data and media motion]].

**The find that justifies the node: a bar chart drew two different values as the same bar.** The
fills were flex children with percentage heights, so flex clamped them to the space the labels
left, and 74% and 85% both rendered at 171px of 250. **Nothing looked wrong** — handsome chart,
correct labels, false picture. The node now carries both the fix, absolute fills inside a plot
area of known height, and the check: assert each rendered height against the ratio it claims and
assert distinct values give distinct heights.

**A standing honesty rule came out of it.** Any figure that is not measured carries a visible tag
saying so, inside the chart frame. A placeholder chart without one is a fabricated result,
whatever was intended, and a thesis proposal is the worst place for that.

**Images: compress before embedding.** The supplied example went from 1722 KB to 92 KB at
presentation size, a 95% cut with no visible loss. Also recorded: a full-bleed illustration with
baked-in text does not crop, and the example lost its own wordmark to a 3:2 frame.

**And a judgement given rather than swallowed.** The supplied image is a neon robot with generic
AI iconography: the exact cliche `Rick - takes` rejects, and it fights the terracotta palette. It
was integrated so he could judge it in context, with the recommendation to use a diagram drawn in
brand instead. **An illustration that decorates is worth less than a diagram that argues.**

**2026-08-16 — icons arrived, the build procedure became explicit, and JADS lost its font.**

**Rick supplied ten icons; four are used.** The kept four are static monochrome outlines, so
they are applied as a **CSS mask filled with a brand colour** rather than placed as images. That
one decision is why a single asset now serves Terracotta, JADS and Violet Tide instead of three
recoloured copies. **Six animated GIFs were refused**: 21 to 26 frames of looping motion each,
against a motion rule that says nothing loops once a section has settled.

**The router now carries an ordered build procedure**, on Rick's instruction that the skill
should know step one, step two, the font and the animation without deciding any of it again.
The settled-defaults table is the point: brand, font, scale, stage, motion, icons and output all
have one answer, and the six verification checks below it have each caught a real defect this
week.

**JADS no longer overrides the font.** It mandated Arial in its own style guide and Rick ruled
that the house Inter wins. The guide's section 2 is struck through rather than deleted, so the
override reads as deliberate rather than as drift, and the JADS deck was rebuilt and
re-verified because a font swap is a layout change.

**2026-08-15 (seventh) — a third artifact exists, and Rick found it by testing the hard rule.**
He was told a deck is not a website and asked to see the website version built at full strength
rather than take it on trust. That was the right call: the test produced
[[08 - Skills/HTML Presentations/Presentation sites|Presentation sites]], the tabbed format he
then approved.

**The rule survives, better stated.** A deck is still not a website. What the rule was missing
is the question that comes first: **is this presented, or is it sent?** A site presented in a
room makes the audience watch blank panels animate in; a deck sent as a link says too little to
read alone. The router now asks that before anything else.

**The new node carries the parts that were only in one build's CSS:** the tab navigation
contract, the four-pattern animation set with its timings, and two layout rules that came
straight out of his review. Sections were vertically centred, so the heading landed at a
different height on every section and the page appeared to jump; they are now top-aligned to one
value, verified by measuring all eight. And a five-stage pipeline is five explicit columns,
because `auto-fit` wrapped it 4+1 and orphaned the last stage.

**One rule is recorded because he had to give it twice:** a long statement under a heading is
body text one size up, not a second headline. Bolding it and tightening the tracking made it
read as a different typeface, since Inter's optical sizing genuinely changes letterforms with
size. The second time it went into the skill rather than into the CSS.

**Also banked: how this got good.** Every real improvement in five rounds came from Rick looking
at a render, not from anyone reading markup. That list is at the end of the new node, because it
is the transferable part.

**2026-08-15 (sixth) — Terracotta replaces JADS as the default brand, on Rick's instruction.**
He saw the same narrative in four brands and picked this one. The profile lives in Core Design
with its measured palette; this skill only records that the default moved and what that costs.

**What it costs is worth stating plainly:** JADS was the default *because* most decks are
handed to the university. That reason did not disappear, so the router now carries an explicit
instruction to ask before building coursework in Terracotta. A default that is right most of
the time and silently wrong for submissions is a worse failure than a slightly inconvenient one.

**Also his instruction: stop building one deck in several brands to compare.** He called it
token waste. Build the default; rebuild in another brand when asked.

**And a hard-won delivery rule, in `3 Deck delivery`:** never hide content in the base
stylesheet and rely on script to reveal it. A scroll-reveal built as `opacity:0` plus an
IntersectionObserver rendered two pages completely blank when the observer did not fire, with
no error anywhere. Gate the hidden state on a `js` root class and add a timeout failsafe.

**2026-08-15 (fifth) — Inter now ships inside the deck, and the Segoe UI stopgap is retired.**
Rick supplied the font himself and approved embedding it. The entry below recorded Segoe UI as
the house face **because Inter was not installed**; that reasoning is now void and the stack
leads with Inter.

**Subsetting is what made it affordable.** The raw variable font is 854 KB. Subset to 202
codepoints and flavoured as woff2 it is **51 KB**, about 68 KB once base64'd, so an Inter deck
is roughly 97 KB against 28 KB for the JADS deck that carries no face. Without subsetting the
same embed cost 894 KB, which is why it was worth the detour. `fonttools` was run through
`uv tool run`, so nothing was installed into Rick's Python.

**The asset is committed beside the skill** rather than regenerated per deck, with its OFL text
and codepoint list, because every future presentation wants the same file.

**Two things worth carrying forward.** Inter runs taller than the fallbacks and pushed the
densest slide past the safe margin, so a font swap is a layout change and needs the overflow
check re-run. And **Helvetica Neue was offered and refused**: commercial face, embedding is
redistribution, and these decks are handed to a university.

**2026-08-15 (fourth) — the type scale is now house, not brand. Rick's decision.** He saw one
narrative built in four brands, picked the Terracotta build's typography and made it the
standard for every presentation. Colour, radius and shadow stay with the brand; the scale, the
font stack, the archetypes and the motion do not.

**The font recorded is Segoe UI, not Inter, and that is deliberate.** The Terracotta deck
declared `Inter, 'Segoe UI', ...`, but Inter is not installed on Rick's machine and neither is
Helvetica Neue, so what he actually approved was the fallback. Naming Inter as the standard
would have changed the look the day someone installed it. Segoe UI leads; Inter stays in the
stack as the better face if it arrives. **Check what a font stack actually resolves to before
recording a preference based on a render.**

**One conflict left open rather than decided:** the JADS style guide mandates Arial, and a JADS
deck is handed to the university. Not overridden on JARVIS's authority; parked in
`Active Priorities` and JADS keeps Arial meanwhile.

Also written down: the single entrance animation the decks use, as the house pattern, with an
explicit instruction not to invent a second one. A vetted library is parked for Rick to work
through, since an unvetted flourish is the AI-slop signature the skill exists to prevent.

**2026-08-15 (third) — the display rule corrected, after the first correction was wrong.**
The entry below about specificity was right about the cause and **wrong about the fix**, and
the wrong fix shipped. Raising the archetype to `.slide.is-active.title-slide` makes the active
slide centre properly but leaves the bare `.title-slide{display:flex}` in place, which still
beats `.slide{display:none}` by source order. Result: five slides visible at once, the last one
painting over the deck, and Rick seeing nothing but slide 18 no matter what he pressed.

**An archetype must not declare `display` at all.** Both halves are needed and the node now
says so.

Also added to the node: the verification that actually catches this. Counting `is-active`
elements never fails, because exactly one slide carries the class throughout. Only stepping the
deck and asserting on **computed `display`** finds it, and a contact sheet cannot, because each
slide is rendered in isolation. That gap is why it shipped twice.

**2026-08-15 (later) — a deck that writes its position to the URL must listen for it too.**
Rick opened a finished deck from disk, edited the address bar to `#5`, and the deck stayed
where it was. The hash was read once on load and never again, so the URL advertised a jump
control the deck did not implement.

Worth recording because the first diagnosis was wrong and cost a step: the suspicion was that
`history.replaceState` throws on a `file://` origin. Tested in headless Chrome against a real
`file://` URL, and it does not throw; the hash was updating correctly all along. **Test the
origin assumption before rewriting anything around it.** Rule added to
[[08 - Skills/HTML Presentations/3 Deck delivery|3 Deck delivery]].

**2026-08-15 — two CSS specificity traps banked into `1 Deck architecture`.** Found while
building the thesis proposal deck in four brands, both by rendering rather than by reading.

The first cost the most: `.slide.is-active{display:block}` outranks `.title-slide{display:flex}`,
so every title, divider and closing slide ignored its own centring without erroring. It was
invisible in the markup and obvious the moment a slide was looked at. The fix is a
three-class selector for the full-field archetypes.

The second only shows up once a deck has more than one brand: a theme layer written at lower
specificity than the base rule it means to override loses, which put white eyebrow text on a
pale title field in the theme that inverts that archetype. Stated as a rule because the
skill now expects one narrative to be built in several brands at once.

Also added: draw step and flow connectors as pseudo elements, which closes the 2026-08-01
silent-grid-wrap trap at the source rather than by counting children.

**2026-08-10 — created, from knowledge that already existed in the wrong place.** Rick's
architecture decision: three output domains reading from one Core Design foundation.

Deck mechanics had been filed inside the JADS brand profile since 2026-07-31, which caused
two visible problems. A session building a non-JADS deck had no source for the archetypes at
all. And `Streamlit` had to carry an instruction to read "sections 1, 2 and 7 only" of the
JADS file, because the rest was deck physics that does not transfer to a browser. That
instruction was a workaround for a filing error and is now removed.

**What moved, and the test applied:** an archetype is deck physics, a terracotta page badge
is JADS. So the seven archetypes, the component list, the density budget, the pt-to-px
conversion and the repeated-component alignment rule came here as brand-agnostic
composition. The JADS file keeps its own styling of those same components.

**Two rules from `Design` came with them.** The HTML-not-PowerPoint default, Rick's call on
2026-08-01 after building the same deck both ways. And the wrapped-grid trap from the same
day, where a three-column grid received five children because the connectors between cards
are also children, and a slide silently overlapped its own footer.

**The brand default changed at the same time.** Any presentation is now JADS unless Rick
names a custom palette, rather than JADS only for work handed to the university. His
instruction, and it matches what he actually builds. Row 1 of the ladder in
[[08 - Skills/Core Design/0 Core Design|Core Design]].

**One thing is deliberately unresolved.** Whether Reveal.js and similar frameworks are
vendored locally or loaded from a CDN. The offline rule says vendored and that is written as
the working assumption, marked as such in
[[08 - Skills/HTML Presentations/3 Deck delivery|3 Deck delivery]]. Rick's Reveal.js
documentation is expected to settle it, and only that section changes when it does.
