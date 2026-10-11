---
name: explain-doc
description: Read a document — Confluence page, article, PDF, spec, or link — and explain it from zero context, ELI5, with a visual artifact (flowchart, diagram, or HTML) so the reader can follow it without background. Use when the user hands over a doc or URL and wants it made understandable.
---

Turn a document the reader has no context for into something they can follow and explain back. Follow `../../references/explain-visually.md` for the ELI5 rules and for picking and drawing the visual.

## Steps

1. **Ingest the whole thing.** Read the full source, not a skim — fetch the URL, read the file/PDF, pull the Confluence page. Note what it *assumes* the reader already knows; those assumptions are exactly what you'll have to ground.
2. **Find the spine.** In one sentence: what is this document actually about, why does it exist, and what is the one thing the reader must walk away with? Everything else hangs off that.
3. **Rebuild from zero.** Explain assuming the reader knows nothing — ground every term the first time it carries weight, concrete example before the abstract rule, one mental model. Don't inherit the document's jargon; translate it.
4. **Draw the mechanism.** Pick the visual that fits what the doc describes — a flowchart for a process, an architecture diagram for a system, a sequence diagram for an interaction, an HTML page for something layered or interactive. The picture shows how the thing actually works; it is not decoration.
5. **Layer the delivery.** TL;DR first (the spine in three sentences), then the walkthrough built around the visual, then the detail for a reader who wants to go deeper. Let them stop when they've got enough.
6. **Hand off.** End with what this now lets them do, and what to read next if they want more.

## Completion

A reader with zero prior context can explain the document's core idea back; every term is grounded before it's leaned on; the visual shows the real mechanism and is legible in light and dark. The explanation stands on its own without the original doc open.
