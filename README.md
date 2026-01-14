# MTG ManaBase Calculator

A lightweight, browser-based tool that implements Frank Karsten–style heuristics for:
1) estimating **recommended land count** for a deck, and  
2) estimating **required coloured mana sources** to cast spells **with >90% consistency**.

This repo is intended to be simple, fast, and easy to host (local file, GitHub Pages, or any static host).

## What’s included

### 1) Deck Land Calculator
Estimates the recommended number of lands from:
- **Deck size** (40 / 60 / 80)
- **Average mana value** (avg MV / “curve”)
- **# of cheap draw/ramp** cards
- **Companion** adjustment
- **MDFCs** (separate weights for non-mythic vs mythic MDFCs)

The calculator uses the linear formula popularised in Karsten’s updated land-count analysis.

### 2) Colour Base Calculator
Outputs the recommended number of **coloured sources** required for a selected **mana cost pattern** (e.g., `1C`, `CC`, `2CCC`, `4CCC`) and deck size (40 / 60 / 80), targeting **>90% cast-on-time consistency**.

## Demo

- Local: open `index.html` in your browser.
- Hosted: enable GitHub Pages (instructions below).

Tip: This is pure HTML/CSS/JS—no build step.

## How to use

### Deck Land Calculator
1. Select deck size (40/60/80)
2. Enter average mana curve (avg MV)
3. Enter number of cheap draw/ramp spells
4. Toggle companion if relevant
5. Enter MDFC counts (non-mythic and mythic)
6. Click **Calculate Lands**

Output: `Number of Lands Needed: X.XX`

Notes:
- The MDFC adjustment is intended to account for MDFCs being “partial lands” rather than full lands.
- The 40- and 80-card outputs are scaled from the 60-card baseline via deck-size ratio.

### Colour Base Calculator
1. Select deck size (40/60/80)
2. Select mana cost pattern (e.g., `1C`, `CC`, `2CC`, `CCC`, etc.)
3. Click **Calculate Color Base**

Output: `Number of Colour Sources Needed: N`

Interpretation:
- “Colour sources” means cards/lands that can produce that colour (including duals/triomes, etc.). The tool gives the *target count*; it does not build the mana base for you.

## Data sources / Attribution

This project is based on the methodology and published tables described by Frank Karsten in the following articles:
- **How Many Lands Do You Need in Your Deck? An Updated Analysis**  
- **How Many Sources Do You Need to Consistently Cast Your Spells? (2022 Update)**  

All credit for the underlying analysis and recommendations belongs to the original author/publisher. This repo provides a convenience implementation of the published heuristics.

## Known limitations (important)

- These are **heuristics**, not simulations. Unusual deck mechanics (extreme cantrip density, free spells, heavy tutoring, atypical mulligan decisions, etc.) can shift optimal counts.
- The colour-source calculator currently uses a **lookup table** keyed by (deck size × mana cost pattern). It assumes the consistency target described in the source article and does not model your specific spell distribution.
- The current HTML includes some duplicated mana-cost options (e.g., `3CC` appears more than once). If you extend this tool, consider deduplicating the dropdown options.
