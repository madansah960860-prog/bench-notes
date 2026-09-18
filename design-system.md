# Bench Notes — Design System
Bread baking with real baker's math. The reader is scaling a formula by hand,
probably on paper, probably with flour on their fingers.

## 1. Colour

| Token | Hex | Role |
|---|---|---|
| `--ink` | `#1B2A4A` | Ink navy. All text |
| `--ground` | `#FCFCF7` | Page |
| `--surface` | `#F4F6FA` | Table heads and the formula total row |
| `--brand` | `#1B2A4A` | Ink navy |
| `--accent` | `#B5651D` | Crust. **Non-text only** — timeline marks and rules |
| `--crust-deep` | `#9A5417` | **Derived.** Crust where it must carry small text |
| `--rule` | `#DCE6F2` | Grid blue. The 24px graph paper and every 1px rule |
| `--muted` | `#5A6478` | Derived secondary text |

**Contrast, measured:**
- `--ink` on `--ground` = **13.82:1** (AAA) · on `--surface` 13.14:1 (AAA)
- `--muted` on `--ground` = 5.78:1 (AA+)
- **`--accent` crust is 4.21:1 on ground**, which misses AA for normal text by a
  little. It is therefore used only for non-text marks: the fermentation
  timeline's stops and the rule beneath a heading.
- Where crust has to carry a word, `--crust-deep` is used instead at **5.58:1**.
- `--rule` grid blue is never used for text at all — it draws the graph paper.

## 2. Type

*Newsreader* 400 — **all prose**, and only prose.
*JetBrains Mono* 400/500 — **every number on the site**: hydration percentages,
gram weights, timings, temperatures, dates, quantities.

The split is absolute and it is the point. Monospace is justified here and
*only* here among these ten sites, because the site is a ledger: figures have
to align in columns so a reader can scale a formula down a page by eye.

Scale ratio **1.200** — a quiet scale for a reference document.

```css
--step--1: clamp(0.85rem, 0.84rem + 0.06vw, 0.88rem);
--step-0:  clamp(1.0625rem, 1.05rem + 0.08vw, 1.10rem);
--step-1:  clamp(1.275rem, 1.25rem + 0.14vw, 1.32rem);
--step-2:  clamp(1.53rem, 1.49rem + 0.25vw, 1.59rem);
--step-3:  clamp(1.84rem, 1.77rem + 0.42vw, 1.90rem);
--step-4:  clamp(2.20rem, 2.09rem + 0.66vw, 2.29rem);
--step-5:  clamp(2.64rem, 2.46rem + 1.05vw, 2.75rem);
```

- Body line-height **1.7**, measure **70ch**
- Numerals use `font-variant-numeric: tabular-nums` everywhere

## 3. Space

**Everything snaps to the 24px graph grid.** All vertical spacing is a multiple
of 24: `24 48 72 96 120`. Section rhythm 96px. The grid is not decoration —
it is the measure the layout is built on.

## 4. Shape

- **Radius: 0 everywhere.**
- 1px `--rule` grid-blue rules and nothing heavier.
- **No shadows.**

## 5. Layout

A **24px graph-paper background drawn in CSS** with two
`repeating-linear-gradient` layers, one horizontal and one vertical. Content
sits directly on the paper in a **780px column**; formula tables are allowed to
break wider than the column, up to 980px, because a table is the one thing that
should not be squeezed.

```
┌ · · · · · · · · · · · · · · · · · · · ┐
│ BENCH NOTES                           │
│ Country loaf · 75% hydration          │
│ ┌────────────┬───────┬──────┐         │
│ │ bread flour│ 800 g │ 100% │         │
│ │ water      │ 600 g │  75% │         │
│ │ starter    │ 160 g │  20% │         │
│ │ salt       │  18 g │ 2.2% │         │
│ └────────────┴───────┴──────┘         │
│ 09:00 mix ──── 13:00 shape ── 07:00 bake│
└ · · · · · · · · · · · · · · · · · · · ┘
```

## 6. Components

- **Formula table — the primary component.** Ingredient, grams, baker's
  percentage, with a **total dough weight row** on `--surface`. Every figure is
  mono and right-aligned so the column reads as a column.
- **Fermentation timeline** — a labelled horizontal rule with timestamps along
  it: a 1px grid-blue line, crust-coloured stops, mono times beneath. Not a
  progress bar and not an animation.
- **Nav** — one row, mono, small.
- **Button** — **underlined mono text**, no box, no fill. That is the whole
  button.
- **Cards — none.** The recipe index is a list of formulas with their hydration.
- **Form field** — 0 radius, 1px grid blue, ground fill, mono input text.
- **Footer** — navy field, ground text, four columns.

## 7. The one memorable thing

**Every loaf is published as a proper baker's-percentage table that the reader
can scale by hand — on paper that already looks like the notebook they would
scale it in.** The graph grid and the formula table are the same idea expressed
twice, and the site tells you the thing most bread writing hides: that a
starter is itself flour and water, so the hydration on the tin is not the
hydration of your dough. Each formula carries both the simple figure and the
true one.

## Checked against the banned list
- Not cream + serif + terracotta: the ground is a cool near-white, the rule
  colour is a pale blue, and the crust brown appears as a 4px timeline stop
  rather than as a warm headline colour.
- No dark page with an acid accent. No cards. No shadows. Radius 0.
- No tracked-out caps eyebrows, no `·`-joined meta strings in prose, no `→`,
  no coloured word inside a headline, no gradients **as decoration** (the two
  repeating-linear-gradients draw the graph paper and are structural), no
  emoji, no scroll animation. One transition, on the button underline.

## Sameness test
No typeface here is used anywhere else in the ten. **Halstead Mysore** is the
other site that sets figures in monospace, so this one does not touch IBM Plex:
Halstead Mysore is Space Grotesk + IBM Plex Sans + IBM Plex Mono on a high-key
white with blue table tints and a numbered index rail; this is Newsreader +
JetBrains Mono on graph paper with a 780px column and formula tables. Even the
shared *idea* — numbers in a fixed-width face — lands differently: there it
counts breaths against a clock, here it aligns percentages down a column so a
formula can be scaled by eye. Against the other recipe sites: Long Braise is
oat and enamel blue with a sticky rail, Twenty Flat is mustard colour-blocks,
The Spice Base is cotton and indigo with printed dividers. No shared image,
palette or skeleton.
