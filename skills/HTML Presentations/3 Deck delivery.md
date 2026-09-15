---
status: active
project: meta
type: guide
subtype: skill-node
last_updated: 2026-08-15 23:05
---

# 3 Deck delivery

Navigation, printing, and the constraint that governs both. Read before handing anything
over.

## The single-file rule

**One HTML file that opens anywhere and works offline.** Styles inline, scripts in the file,
images embedded as data URIs. No CDN, no external stylesheet, no fetched font, no remote
image.

This is the house style across every project of Rick's, and it is stricter than it looks:
the deck has to survive being emailed, opened on a university machine, and presented from a
room with no network.

### Frameworks are vendored, not fetched

**Working assumption, set 2026-08-10, pending Rick's confirmation.** Reveal.js and anything
like it is embedded in the file rather than loaded from a CDN. The offline rule wins.

Three consequences worth knowing before choosing to use one at all:

- A vendored framework is tens of kilobytes of someone else's code inside the artifact, and
  it has to be pinned, because a deck rebuilt against a different version is a different
  deck.
- **A plain deck needs very little of what a framework provides.** A fixed stage, keyboard
  navigation and a print stylesheet are roughly eighty lines. Reach for the framework when
  the deck genuinely needs its features, not by default.
- The agent building the deck has no web access, so it cannot fetch a framework even if the
  rule were lifted. Anything vendored has to be supplied to it.

**If Rick lifts the offline rule for decks, this section is the only thing that changes.**
Everything else in this skill is unaffected.

## Navigation

**Discrete, linear, and keyboard first.** A deck is driven from a clicker or the arrow keys
by someone who is not looking at the screen they are touching.

- Arrow keys and space advance and retreat. Home and End reach the first and last slide.
- Click advances, in the same direction as the arrow keys.
- **The current position is always visible**, through the page badge.
- **If the deck writes its position into the URL, it must also listen for `hashchange`.**
  Added 2026-08-15, after Rick tried to jump slides by editing the address bar and the deck
  ignored him. Reading the hash once on load makes the URL look like a jump control while
  being only a starting point, and nothing on screen reveals the difference. Clamp an
  out-of-range number to a real slide and correct the URL to match, so the address bar never
  claims a slide that is not showing.
- **Never trap focus** and never require the pointer to reach a specific target. A presenter
  cannot aim.
- No scroll. A deck that scrolls has stopped being a deck.

## Never hide content in the stylesheet and rely on script to reveal it

**Added 2026-08-15, after it produced two entirely blank pages in one session.** A reveal
written as `.thing{opacity:0}` in the base stylesheet, with a script adding the class that
brings it back, has a single point of failure: **if the observer does not fire, the page is
blank and nothing reports an error.** The markup is correct, the console is clean, the content
is simply not there.

Two rules, and they cost three lines:

- **Gate the hidden state on script being alive.** Set a `js` class on the root element from an
  inline script, and write the hidden rule as `.js .thing{opacity:0}`. No script, no hiding.
- **Add a failsafe timeout.** If nothing has been revealed after roughly a second, reveal
  everything. Motion is an enhancement; the content is the point.

The same applies to a deck's own slide switching, which is why `.slide{display:none}` is safe:
the very next rule shows the active one from the same stylesheet, with no script in between.

## Printing to PDF

**One slide per page, and it is tested, not assumed.**

- A print stylesheet fixes the page to landscape at the stage's ratio and forces a page
  break after each slide.
- Progressive reveals print in their final state, with everything visible. A printed deck
  that hides half its content is a broken handout.
- Backgrounds print. A deck whose title slide comes out white has lost its structure.

**Print it and open the PDF.** This is the check most likely to be skipped and it fails
silently: the deck looks perfect on screen and the export is wrong.

## Before handing over

- **Step through every slide in a browser and look at it.** Not the first three. Layout that
  collapses under real content is invisible in the source and obvious on screen.
- Check every declared type size against the floor from
  [[08 - Skills/HTML Presentations/1 Deck architecture|1 Deck architecture]].
- Confirm no external host is referenced anywhere in the file.
- **No dashes as punctuation.** A deck leaves the vault, so the writing rule in `CLAUDE.md`
  applies in full. No em dash, no en dash, no spaced hyphen. Hyphens inside compound words
  are unaffected.
- Run [[08 - Skills/Core Design/5 Quality checks|5 Quality checks]].
