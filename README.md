# Ecuador

Trip document for 12–23 September 2026 — Quilotoa Loop, then Chimborazo,
Cotopaxi, Quito or Baños. Eleven nights, two people.

**Live:** https://leftbrain847.github.io/Ecuador/

## Using it

Five tabs: the day-by-day, every transport leg, night-by-night lodging with
booking status and the real alternatives for each, the Chimborazo day in detail,
and prep checklists split by owner.

Everything through sunrise on the crater rim on the 18th is fixed. After that
the plan branches four ways — A Chimborazo, B Quito day, C Cotopaxi, D Baños ×4
— and you pick one with the A/B/C/D buttons. The altitude chart redraws to match,
with the other three options left faded behind it. Decide on the evening of the
17th.

Works with no internet. Save the page to Files as a backup for the Loop, where
there's no signal — nothing in it loads from the network. The Transport tab links
out to sources, and those need signal like any link, but every one of them reads
as a plain domain so it still makes sense offline and on paper.

It also prints. Every tab and every day card comes out open, one tab per page.

Checkbox ticks last until you reload. That's deliberate: no scripts, no storage,
so the file survives being opened anywhere, including iOS Quick Look.

## Editing

`index.html` is the whole thing — markup, styles and content in one file.

See `CLAUDE.md` before changing anything. There are hard constraints (no
JavaScript, nothing loading over the network, no browser storage) that keep the
offline guarantee true, and altitudes appear in three places that have to agree.

## Setup

Settings → Pages → Deploy from a branch → `main` → `/ (root)`.
