# CLAUDE.md

Working instructions for this repo. Read this before editing anything.

## What this is

A single-page trip document for 12–23 September 2026 in Ecuador — Quilotoa Loop,
then one of four ways to spend the back half. Eleven nights. **Two people use
it**, not one: Papa Bear and Mama Bear travelling together. Write for both of
them. "We" and "both of us" are correct; second-person singular directed at one
owner is not.

It is published via GitHub Pages and is also saved offline on two phones. It has
to work in a village with no signal.

## Files

- `index.html` — the entire document. Markup, CSS and content in one file.
  GitHub Pages serves it at the bare repo URL, which is why it has that name.
- `README.md` — human-facing, short.

There is no build step, no dependencies, no package.json. Edit the HTML directly.

## Hard constraints — do not break these

1. **No JavaScript.** None. Accordions are native `<details>`/`<summary>`. Tabs
   and the option selector are hidden radio inputs driven by CSS sibling
   selectors (`#t1:checked ~ #s1`, `#o1:checked ~ * #p1`). If a feature seems to
   need JS, it doesn't go in — the file must render and function under iOS Quick
   Look, which does not execute scripts.
2. **Nothing loads over the network.** No web fonts, no CDNs, no analytics, no
   remote images, no stylesheets. Fonts are the system stack. If you add an
   asset, inline it. Anchors to external sites are permitted (see below); a
   `src=`, `<link>`, `@import` or `url(http…)` is not.
3. **No browser storage.** `localStorage` and `window.storage` are both out —
   the first is unreliable in the contexts this gets opened in, the second only
   exists inside Anthropic's artifact viewer. Checkbox ticks are session-only
   and the footer says so. Don't quietly add persistence.
4. **Single file.** Keep everything in `index.html`. Splitting the CSS out adds
   a network request and breaks the saved-to-Files copy.

## Content rules

- **Every factual claim needs a source you actually checked.** Bus times, fares,
  altitudes, opening status, road conditions, lodging prices. If it can't be
  verified, label it as unverified in the text rather than stating it cleanly.
  The footer carries the general staleness warning; specific uncertainty belongs
  next to the claim.
- **Don't invent place names, prices, or schedules.** If a lodging or operator
  can't be confirmed to exist, say "book a bed in X" rather than naming one.
  Where sources disagree — as they do on most Loop lodging prices — give the
  range and say they disagree.
- **Flag what's stale-prone.** Fares predate a 2026 interprovincial increase.
  Road, reserve and security conditions change fastest. Keep those caveats.
- **Links must read as text.** External anchors are allowed on the Transport
  tab, but the anchor text is always the bare domain — never "click here", never
  a title standing in for a URL. The page gets printed and opened without
  signal, and a link whose text is the domain still works on paper.
- **Altitudes are verified** and appear in three places that must stay in sync:
  the SVG chart paths, the day-card `meta` lines, and the footer list. Changing
  one means changing all three. This is the check that has actually caught
  errors — run it every time.

## The altitude chart

One inline SVG, `viewBox="0 0 340 100"`, structured as a common trunk plus four
branches:

- **Trunk** — 12 to 17 Sep, identical under every option. Three paths: `.fill`,
  `.maxline`, `.sleepline`.
- **Branches** — `g.br.brA` … `g.br.brD`, each carrying its own `.maxline` and
  `.sleepline` from 17 to 22 Sep. All four are drawn faded; the one matching the
  selected option is brought to full opacity by the `#o1:checked ~ *` rules, as
  are its `.dot` and `.lab`. Every branch must start at the 17 Sep trunk values
  or the fork visibly breaks.

Line meanings: dashed gold (`.maxline`) is the highest point reached that day;
solid teal (`.sleepline`) is sleeping altitude.

Coordinate mapping, if you need to move a point:

```
x = 10 + (date - 12) * 32        # 12 Sep = 10, 22 Sep = 330
y = 84 - (altitude - 1500) / 3700 * 72
```

Reference altitudes (metres): Tababela 2400 · Quito 2850 · Sigchos 2850 ·
Latacunga 2750 · Isinliví 2950 · Chugchilán 3200 · Quilotoa rim 3914 ·
Riobamba 2750 · Baños 1800 · Cotopaxi refuge 4864 · Carrel refuge 4850 ·
Whymper 5050 · Condor Cocha 5100.

The rim is drawn and labelled as 3,900 for legibility while the footer carries
the verified 3,914. That is the one deliberate rounding; everything else matches
to the metre.

## Structural conventions

- **Five tabs**: Days, Transport, Stay, Chimborazo, Prep. Radios `t1`–`t5`,
  sections `s1`–`s5`. Adding a tab means a radio, a label, a section, and three
  additions to the `:checked` selector groups.
- **Four options**: A Chimborazo, B Quito day, C Cotopaxi, D Baños ×4. Radios
  `o1`–`o4` sit at the top of `<body>`, before `<header>`, so their `~` selectors
  reach both the chart and the panes. Panes are `p1`–`p4` inside `.optbox` on the
  Days tab. Two `.optnav` bars select them — the `.mini` one under the chart and
  the full one at the branch point — and both must list all four.
- Day cards: six in the trunk (12–17 Sep), five in each pane. Twenty-six total.
- `.alertband` (rust) is for unresolved constraints and things that can ruin a
  day. Use it sparingly — currently two instances. `.bandnote` (gold) is for
  softer framing.
- `p.gate` inside a day card marks a decision point with a hard condition.
  These are load-bearing; don't soften them into prose.
- `.status` pills on the Stay tab: `lock` (book now, or already "Booked"),
  `hold` (must stay unbooked), `open` (book late). The three `hold` nights after
  the 17th are what make the four options function — never change them to `lock`.
- `.opts` / `.lodge` blocks list the real lodging choices for a night, with
  `.lodge.picked` plus a `.tick` for one that's booked.
- Checklist owner tags are `Papa Bear`, `Mama Bear`, `Both`.
- A print stylesheet lives at the end of the `<style>` block: it forces every tab
  and every day card open, one tab per page, in ink-friendly colours. Any new
  collapsible or tab-scoped content needs a rule there too, or it prints blank.

## Tone

Direct. No hedging for its own sake, no enthusiasm padding, no "don't forget to
have fun." Where something is a genuine trade-off, state both sides and say
which way it leans. Where a previous version was wrong, correct it plainly.

## Deploy

Push to `main`. GitHub Pages serves from the repo root. Live in about a minute
at `https://leftbrain847.github.io/Ecuador/`. No build, no action to run.

## Before committing

- Open `index.html` in a browser with JavaScript disabled — tabs, the option
  selector and accordions must all still work.
- Grep for `src=`, `<link`, `@import` and `url(http` — there should be no hits.
  `href` to an external site is fine; anything that *loads* is not.
- Check every `<a>`'s text is the bare domain.
- Check the three altitude locations agree. Decode the SVG rather than trusting
  it: `altitude = 1500 + (84 - y) / 72 * 3700`.
- Confirm all four branches start from the 17 Sep trunk values.
