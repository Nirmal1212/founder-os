# Typography System

Goal: a type system that carries the product's personality and stays legible for the personas' real context of use. Typeface choice and scale are derived from the strategy, not picked for taste.

## Process

1. **Match faces to intent + readability budget.** Long-session, data-dense, professional tools need a highly legible body face with good numerals and tight vertical rhythm; expressive consumer products can carry a more characterful display face. Pick deliberately — not the same families used on every project.
2. **Assign roles**, typically:
   - **Display / heading** — characterful, used with restraint for hierarchy and brand moments.
   - **Body / UI** — the workhorse; optimized for legibility at small sizes, with a clear set of weights.
   - **Utility / mono** (optional) — for data, code, IDs, timestamps, tabular numbers. Essential for dashboards, dev tools, and anything with figures.
   Prefer pairings with a clear contrast of role; if using one superfamily, justify it. Default to widely-available / system or open-source faces unless the brand calls for licensed type — and name the fallback stack.
3. **Set a type scale.** Define a modular scale (e.g. 1.20 minor third for dense UI, 1.25–1.333 for expressive) with named steps: `display`, `h1`, `h2`, `h3`, `body-lg`, `body`, `body-sm`, `caption`, `overline`. Give size / line-height / weight / letter-spacing for each. Tighter line-height for headings, looser for body.
4. **State usage rules.** When to use each step, max heading levels per view, sentence vs. title case, number formatting (tabular for tables), and minimum body size for the personas' device (don't go below 14px body on data-dense desktop; 16px on consumer mobile).
5. **Accessibility.** Body ≥ chosen minimum; never rely on weight alone for hierarchy; ensure the chosen sizes pass contrast at their weight; support user font-scaling (use rem).

## Output format

- **Inline rationale** (3–6 sentences): which faces, why this pairing serves these personas and this intent, and the one type decision that's the signature move.
- **Specimen visual** via `visualize` (`art`/`mockup`): render the scale top-to-bottom with real sample copy from the product domain (not "Lorem ipsum"), labeling each step's size/weight/line-height.
- **Scale table**: Token | px/rem | line-height | weight | letter-spacing | use.
- **Tokens written to `design-tokens.json`** (typography section): `fontFamily` (display/body/mono with fallback stacks), `fontSize`, `lineHeight`, `fontWeight`, `letterSpacing`, and the named `textStyles` combining them.
- **Suggestions**: one alternative pairing considered, and what to test (e.g. the body face at the personas' real density and distance).
