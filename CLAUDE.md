# CLAUDE.md

Working instructions for this repo. Read this before editing anything.

## What this is

A single-page trip document for a September 2026 trip to Ecuador — Quilotoa Loop,
Chimborazo, Baños. Eleven days. **Two people use it**, not one: J and a friend
travelling together. Write for both of them. "We" and "both of us" are correct;
second-person singular directed at one owner is not.

It is published via GitHub Pages and is also saved offline on two phones. It has
to work in a village with no signal.

## Files

- `index.html` — the entire document. Markup, CSS and content in one file.
  GitHub Pages serves it at the bare repo URL, which is why it has that name.
- `README.md` — human-facing, short.

There is no build step, no dependencies, no package.json. Edit the HTML directly.

## Hard constraints — do not break these

1. **No JavaScript.** None. Accordions are native `<details>`/`<summary>`. Tabs
   are hidden radio inputs driven by CSS sibling selectors (`#t1:checked ~ #s1`).
   If a feature seems to need JS, it doesn't go in — the file must render and
   function under iOS Quick Look, which does not execute scripts.
2. **No external requests.** No web fonts, no CDNs, no analytics, no remote
   images. Fonts are the system stack. If you add an asset, inline it.
3. **No browser storage.** `localStorage` and `window.storage` are both out —
   the first is unreliable in the contexts this gets opened in, the second only
   exists inside Anthropic's artifact viewer. Checkbox ticks are session-only
   and the footer says so. Don't quietly add persistence.
4. **Single file.** Keep everything in `index.html`. Splitting the CSS out adds
   a network request and breaks the saved-to-Files copy.

## Content rules

- **Every factual claim needs a source you actually checked.** Bus times, fares,
  altitudes, opening status, road conditions. If it can't be verified, label it
  as unverified in the text rather than stating it cleanly. The footer carries
  the general staleness warning; specific uncertainty belongs next to the claim.
- **Don't invent place names, prices, or schedules.** If a lodging or operator
  can't be confirmed to exist, say "book a bed in X" rather than naming one.
- **Flag what's stale-prone.** Fares predate a 2026 interprovincial increase.
  Road, reserve and security conditions change fastest. Keep those caveats.
- **Altitudes are verified** and appear in three places that must stay in sync:
  the SVG chart paths, the day-card `meta` lines, and the footer list. Changing
  one means changing all three.

## The altitude chart

Two lines in one inline SVG, `viewBox="0 0 340 100"`:

- Dashed gold (`.maxline`) — highest point reached that day.
- Solid teal (`.sleepline`) with gradient fill — sleeping altitude. Ends at
  Day 10; Day 11 is a flight, there is no sleep point.

Coordinate mapping, if you need to move a point:

```
x = 10 + (day - 1) * 32          # D1 = 10, D11 = 330
y = 84 - (altitude - 1500) / 3700 * 72
```

Reference altitudes (metres): Sigchos 2850 · Isinliví 2950 · Chugchilán 3200 ·
Quilotoa rim 3914 · Riobamba 2750 · Baños 1800 · Quito 2850 · Carrel refuge 4850 ·
Whymper 5050 · Condor Cocha 5100.

## Structural conventions

- Five tabs: Days, Transport, Stay, Chimborazo, Prep. Radios `t1`–`t5`, sections
  `s1`–`s5`. Adding a tab means a radio, a label, a section, and three additions
  to the `:checked` selector groups.
- `.alertband` (rust) is for unresolved constraints and things that can ruin a
  day. Use it sparingly — currently two instances. `.bandnote` (gold) is for
  softer framing.
- `p.gate` inside a day card marks a decision point with a hard condition.
  These are load-bearing; don't soften them into prose.
- `.status` pills on the Stay tab: `lock` (book now), `hold` (must stay
  unbooked), `open` (book late). The night-8 `hold` is what makes the flex
  block function — never change it to `lock`.
- Checklist owner tags are `J`, `Friend`, `Both`.

## Tone

Direct. No hedging for its own sake, no enthusiasm padding, no "don't forget to
have fun." Where something is a genuine trade-off, state both sides and say
which way it leans. Where a previous version was wrong, correct it plainly.

## Deploy

Push to `main`. GitHub Pages serves from the repo root. Live in about a minute
at `https://leftbrain847.github.io/Ecuador/`. No build, no action to run.

## Before committing

- Open `index.html` in a browser with JavaScript disabled — tabs and accordions
  must still work.
- Grep for `http` in the file. There should be no hits: domains appear as plain
  text rather than links, so they stay readable offline and on paper.
- Check the three altitude locations agree.
