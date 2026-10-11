# Explaining clearly, with the right picture

Shared reference for `explain-doc`, `explain-term`, and `name-the-concept`. Two parts: how to *write* an explanation someone with no context can follow, and how to *pick and draw* the visual that carries it.

## ELI5 writing rules

"ELI5" means genuinely from zero — not dumbed down, but assuming no prior context and building it up fast.

- **Ground a term before you lean on it.** The first time a word carries weight, define it in that spot. An explanation that uses jargon to explain jargon has explained nothing.
- **Concrete before abstract.** Open with a specific, real example the reader can picture; derive the general rule from it. Never the reverse.
- **One mental model, not three.** Pick the single clearest way to think about it and commit. Offering three analogies splits attention and teaches none.
- **An analogy must hold — and you name where it breaks.** A good analogy maps onto the real thing part-for-part. State the one place it stops being true, so the reader doesn't over-trust it.
- **TL;DR first, then depth.** Lead with the three-sentence version. Layer the detail below it so the reader stops when they've got what they need — progressive disclosure, aimed at the human.
- **Check the handoff.** End with what this now lets them do, or what to read next. Understanding is testable: could they explain it back?

## Picking the visual

Pick the form by *what you're explaining*. The picture must show the real mechanism — one picture that carries the idea beats three that redecorate the text. If a sentence already makes it clear, don't draw.

| You're explaining… | Use | 
|---|---|
| A process or a decision with branches | **Flowchart** |
| How parts fit together (components, layers, services) | **Architecture / box diagram** |
| An interaction over time (who calls whom, in order) | **Sequence diagram** |
| A thing that moves between states | **State diagram** |
| A comparison, distribution, or trend in numbers | **Table or chart** (see the `dataviz` skill) |
| Something layered or interactive the reader should explore | **HTML artifact** |

## Drawing it so it reads

- **Label everything**; an unlabeled box or arrow is a question, not an answer.
- **One direction of flow** — left-to-right or top-down — and keep it.
- **~7 nodes per view.** More than that, split into a high-level view plus a drill-down; don't cram.
- **Legible in light and dark.** Define colors as tokens and give an explicit background; never rely on a default that vanishes in one theme.
- Keep the mechanism visible: the arrows and states should map to how the thing actually works, not to a decorative shape.

## Mechanics

- **Diagrams**: Mermaid or inline SVG. In Claude Code, load the host `artifact-diagramming` skill for the SVG/legibility mechanics before drawing.
- **HTML / interactive**: publish an artifact. In Claude Code, load `artifact-design` first for the page contract (title, theming, layout). Use `dataviz` before any chart.
- Portable fallback (no host skills): a Mermaid code block renders on most platforms; a self-contained `.html` file works anywhere a browser does.
