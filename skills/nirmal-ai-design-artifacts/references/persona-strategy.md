# Persona-Led Design Strategy

Goal: turn the PRD's personas and use cases into a **design strategy** — the reasoning layer that justifies every later visual decision. Skipping this is how you end up with a pretty palette that fights the product. This is the most important artifact; the palette, type, and patterns are downstream of it.

## Process

1. **Restate the thesis and brand intent.** One or two lines: problem / for whom / why now, plus the emotional intent in a phrase ("calm and authoritative", "fast and playful"). Pull this from the PRD; don't reinvent it.
2. **Profile each primary persona for *design*, not product.** For each, capture the design-relevant context — this is what the PRD usually doesn't spell out:
   - **Context of use**: device(s), screen size, environment (office/mobile/field), lighting, posture.
   - **Frequency & session length**: glanced at twice a week vs. lived in 8 hours a day. Drives density, contrast comfort, and how much "delight" vs. "calm" the UI should carry.
   - **Expertise & stakes**: novice vs. power user; low-stakes vs. error-is-costly. Drives affordance explicitness, confirmation patterns, information density.
   - **Emotional state on arrival**: stressed (incident response), bored (data entry), excited (creative tool). The UI should meet them there.
   - **Accessibility needs**: known constraints (low vision, motor, situational like one-handed/sunlight). Treat as design input, not afterthought.
3. **Derive design principles.** Convert the persona profiles into 3–5 sharp, opinionated principles unique to *this* product — each phrased as a directive with a reason. Good: "Density over whitespace — operators triage 40+ tickets a shift, so default to compact rows and let them scan, not scroll." Bad/generic: "Keep it clean and simple."
4. **Set the design tensions.** Name the 2–3 real trade-offs this product forces (density vs. clarity, speed vs. guidance, brand expression vs. neutrality) and state where you land and why. This is where Director judgment shows.
5. **Define the experience principles for states.** Briefly state the intended tone for empty, error, and loading — these carry the brand as much as the hero does.

## Output format (in chat)

- **Brand intent** — one phrase + one sentence.
- **Persona design profiles** — a tight table: Persona | Context of use | Frequency | Expertise/stakes | Key accessibility/design need.
- **Design principles** — 3–5 numbered directives, each with its reason.
- **Design tensions & where we land** — 2–3 bullets.
- **Suggestions & open questions** — what you'd validate (e.g. "confirm operators are on 1080p displays, not 4K — it changes our density target"), and the one risk you'd flag.

End with the checkpoint: confirm the strategy and brand intent before building the palette/type/patterns on it.
