---
name: staging
description: Staging method for big rewrites/ports: build and sign off the product one player/user-judgeable stage at a time (e.g. UI, then combat, then content), judged side by side against the original, with the user's sign-off in a real build gating the next stage. Use on /staging, "do it in stages", "one stage at a time", or when work spread across the whole product isn't producing anything the user can actually use.
---

# Staging: one judgeable stage at a time

A rewrite that works on everything at once passes its own tests and still ships nothing the user can use. Staging makes
the user's experience of one area the unit of work.

## Rules

1. **Split the product into stages the user can judge on their own** (open it and use it: the menus, the combat, the
   editor...). The user sets the order; keep it in a stages file.
2. **One stage at a time.** Work only on the current stage. Pause the rest and log where it stopped. Exceptions: what
   the user explicitly asks for out of order, and blockers (crashes, leaks) that stop testing.
3. **The bar is the original.** Compare side by side with the real thing at the same settings (captures, footage).
   Tests and offscreen captures prepare a build; they never prove a stage.
4. **Ship a playable build for every fix**, with one line on what changed and how to see it.
5. **No regressions.** Don't switch a default or hide a working path until its replacement is at least as good in the
   playable build.
6. **A stage is done only when the user signs off** in a real build. Then the next stage starts.

## Output to the user

Current stage, what changed in the latest build and how to try it, and what's left before sign-off.
