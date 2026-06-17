# Color Palette + Tokens

Goal: a **reasoned, accessible, implementation-ready palette** derived from the persona strategy and brand intent — not a swatch grab. Every color earns its place.

## Process

1. **Anchor on intent + context.** The brand intent and persona context of use (from the strategy) set the temperature, saturation, and contrast budget. High-frequency, long-session, low-light tools → calmer, lower-saturation surfaces and a restrained accent to reduce fatigue. Consumer, low-frequency, delight-driven → more saturated, more expressive. State this link explicitly.
2. **Build the palette in layers**, not as a flat list of favorite colors:
   - **Brand / primary** — the one color the product is remembered by. Usually one hue + a tint/shade ramp (e.g. 50→900).
   - **Accent** — used sparingly for the primary action and key emphasis. This is where you spend boldness (one signature color).
   - **Neutrals** — a full gray ramp for text, borders, surfaces. The workhorse; most of the UI is neutrals. Decide warm vs. cool grays deliberately and say why.
   - **Surfaces** — background, raised/card, sunken, overlay. Define for both light and dark if the product needs dark mode (long-session and low-light tools usually do).
   - **Semantic** — success / warning / error / info, each with a foreground and a subtle background variant.
3. **Assign semantic tokens, not raw hues, at the app layer.** Map raw ramp values to roles: `text.default`, `text.muted`, `surface.base`, `surface.raised`, `border.default`, `accent.default`, `accent.hover`, `status.error.fg/bg`, etc. Code consumes the role tokens; the ramp is the source.
4. **Check contrast on every pair you ship.** For each text-on-surface and accent-on-surface pairing, state the WCAG ratio and AA/AAA result. Body text must clear 4.5:1; large text and UI components 3:1. Call out and fix any failures rather than shipping them.
5. **Stress-test for color-vision deficiency.** Don't rely on red/green alone for status; pair with icon/shape/text. Note this in the output.

## Output format

- **Inline rationale** (3–6 sentences): how the intent + persona context produced this palette; what the signature color is and why.
- **Visual swatch sheet** via the `visualize` tool (`art`/`mockup` modules): show each token group as labeled swatches with hex and the semantic role; show light and dark surfaces side by side if applicable.
- **Contrast table**: Pair | Ratio | Result (AA/AAA). Include the worst cases, not just the comfortable ones.
- **Tokens written to `design-tokens.json`** (color section) in the outputs directory.
- **Suggestions**: 1–2 alternative directions you considered and rejected (one line each), and what you'd test (e.g. the accent against the real product screenshots / under the personas' actual lighting).

## Tokens (color section of design-tokens.json)

Populate the `color` object: `brand` (ramp), `accent`, `neutral` (ramp), `surface` (base/raised/sunken/overlay, per mode), `text` (default/muted/inverse), `border`, and `status` (success/warning/error/info, each fg + bg). Hex strings. Mirror under `light` and `dark` where the product is dual-mode. Use Python's `json` module to write it so it stays valid.

Avoid the AI-default palettes (cream+terracotta, near-black+acid-green) unless the brief asks for one — derive the hue from the subject's own world and the personas instead.
