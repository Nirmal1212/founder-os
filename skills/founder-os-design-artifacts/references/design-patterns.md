# Design Patterns / Component Language

Goal: the rules and tokens for how the product is *built* — spacing, radius, elevation, motion, and the behavior of core components and their states — all tied back to the use cases. This is what makes screens feel like one product.

## Process

1. **Set the foundational tokens** (derived from intent + density target from the strategy):
   - **Spacing scale** — a base unit (commonly 4px) and a ramp (4/8/12/16/24/32/48/64). Dense tools lean on the lower end; spacious consumer UIs on the higher.
   - **Radius** — corner-radius scale (e.g. 0/4/8/12/full). A signal of personality: sharp = serious/technical, soft = friendly. Pick deliberately and state why.
   - **Elevation** — a shadow/overlay system for layering (flat → raised → overlay → modal). Define each as a token.
   - **Motion** — duration and easing tokens (e.g. fast 120ms / base 200ms / slow 320ms; standard/enter/exit easings). State the motion idiom and respect `prefers-reduced-motion`.
   - **Borders / focus** — default border token and a **visible focus ring** spec (keyboard accessibility is non-negotiable).
2. **Define the core components for *this* product**, chosen from the use cases — not a generic kitchen sink. Identify the 5–10 components that carry the core loop (e.g. for an ITSM console: ticket row, status badge, priority tag, filter bar, detail panel, bulk-action bar). For each, specify the tokens it uses and its key variants.
3. **Specify every state, not just default.** For interactive components define: default, hover, active/pressed, focus, selected, disabled, loading. For data surfaces define: **empty**, **loading/skeleton**, **error**, and partial/over-full states. Most weak systems only style the default — this is where Director rigor shows.
4. **Write the UX copy tone for states.** Empty states invite action; errors say what happened and how to fix it in the interface's voice; nothing apologizes or goes vague. Tie the tone back to the brand intent.
5. **State layout/density rules.** Grid, max content width, table row height, touch-target minimums (≥44px on touch), and breakpoints if multi-device.

## Output format

- **Inline rationale** (3–6 sentences): how density target and intent drove spacing/radius/motion; the signature interaction idiom.
- **Component sheet visual** via `visualize` (`mockup`): render the core components in their key states, using the real palette and type tokens so it reads as the actual product.
- **Token + component tables**: the foundational scales, then a per-component table (Component | Variants | States | Tokens used | Use case it serves).
- **State/empty/error copy examples** for the 2–3 most important surfaces.
- **Tokens written to `design-tokens.json`** (`spacing`, `radius`, `elevation`, `motion`, `border`, `focus`).
- **Suggestions & hand-off**: the one risk to validate, and the pointer to `frontend-design` to build actual screens against these tokens.
