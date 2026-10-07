---
name: pdf-reference-synthesis
description: The PDF Reference Synthesis Insight method - when a hard-won understanding of how a system works is reached (especially one that was missed or misunderstood before), synthesize it into a durable, illustrated PDF reference with real evidence, so it is never forgotten or re-derived. Use freely whenever a session uncovers a fundamental mechanism, on "/pdf-reference-synthesis", "make a pdf on it", "so we don't forget", "record this understanding", and at the start of related work to consult the existing references.
---

# PDF Reference Synthesis Insight method

Insights that took hours to reach (and were missed before) get lost in logs and chat. Turn each one into a short,
illustrated PDF reference that explains the mechanism, shows the real evidence, and records how to verify it - then
read it before touching that system again.

## When
- A session finally understands a mechanism after being wrong about it (the "why we missed it" is part of the value).
- The user names something fundamental ("this is fundamental to the feel", "so we don't forget").
- Before working on a system that already has a reference: open and follow it.

## Structure (keep it to a few pages)
1. **Title + one-paragraph scope**, sources (code locations, data files, recordings).
2. **The one-sentence version** in a highlighted box: the insight in plain words.
3. **How the system is built**: its layers and the order they run in, with code/rva/file citations.
4. **What you feel / see -> mechanism -> real measured values** table: one row per effect.
5. **What it is NOT**: things that look related but don't apply (prevents re-chasing dead ends).
6. **Real evidence images** (screenshots/frames/charts from the original, captioned with what to notice).
7. **How to verify** (lessons learned, including the wrong turns and why they were wrong).
8. **Where things live**: files, recordings, tests, sheets.

## How
- Write it as HTML with embedded images (base64) via a small generator script kept next to it, then print to PDF
  (Edge/Chrome `--headless --print-to-pdf`, no headers/footers). Keep the generator so the PDF can be rebuilt.
- Use only verified facts and real measurements; mark anything unconfirmed.
- Save under the project's `docs/fundamentals/` (or equivalent), add a memory pointer, and mention it in the log.
- Plain language first, jargon defined on first use.

## Output to the user
The PDF path, one line on the insight, and where it will be consulted from.
