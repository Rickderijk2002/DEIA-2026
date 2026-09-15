# Icon assets

**Supplied by Rick, 2026-08-15, from Icons8.** Only the **static, monochrome outline** files
are kept here. They are pure black with alpha, which is what makes them usable: they are applied
as a **CSS mask** and filled with a brand colour, so one file works in every palette.

| File | Used for |
|---|---|
| `icons8-laptop-50.png` | work done at a machine |
| `icons8-user-groups-50.png` | people, teams, more than one actor |
| `icons8-calendar-50.png` | time, recurrence, history |
| `icons8-handshake-50.png` | the client relationship |

## What was refused, and why

**The six animated GIFs are not used.** Each carries 21 to 26 frames of looping motion, and the
skill's motion rule is that nothing loops and nothing moves once a section has settled. A
looping icon is ambient motion competing with the content, and it is the single fastest way to
make a professional deck look like clip art. They were also the coloured two-tone style, which
does not sit with a terracotta palette, and mixing two icon styles in one artifact breaks the
one-aesthetic-theme rule.

## Licence

**Rick confirmed on 2026-08-16 that these were downloaded free.** The vendor's free tier
requires a visible credit, so **a deck using them carries one line of attribution** in the
closing slide metadata or a footer. It costs a few words and it settles the question
permanently.

## This folder is the home. Drop new icons here

**The smartest arrangement, and the reason it is this one:** the skill owns the assets, and a
build embeds them as data URIs at build time. That gives one copy on disk, no duplication per
deck, and every output still a single offline file.

- **Add a new icon by putting the file in this folder.** Nothing else needs changing.
- **Prefer SVG.** It removes the resolution ceiling and masks just as cleanly.
- **Monochrome only.** A coloured icon cannot be tinted, so it fights whichever palette it lands
  in. Colour comes from the brand at build time, never from the file.
- **Static only.** Animated files are refused, see above.

## Known limits

- **50 px source.** Fine masked at 24 to 28 px, soft above roughly 40 px. **SVG is the fix**, and
  Icons8 offers it.
- **The set is incomplete** for the thesis narrative. Icons go where they genuinely fit and
  nowhere else; a decorative icon is worse than none.
