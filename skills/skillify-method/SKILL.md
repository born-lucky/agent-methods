---
name: skillify-method
description: Turn a working practice the user has named ("let's call this the X method") into a reusable method doc + Claude Code skill + memory, and publish it to the user's methods repo. Use on /skillify-method, "turn this into a skill", "make this a method", "systematize this for future sessions", or whenever the user names a new method mid-project.
---

# Skillify: turn a named practice into a method and a skill

When the user names a way of working ("call this the reader method"), capture it while the example is fresh, so future
sessions apply it without re-explaining. Model it on the Spreadsheet Method's shape: why, rules, steps, tools, output.

## Steps

1. **Name and trigger.** Use the user's name for it. Write one sentence: what problem it solves and when to use it,
   with the phrases that should trigger it.
2. **Capture the founding example.** What went wrong without it, and what it found or fixed with it, with concrete
   numbers. This is the "Why" section; it is what makes future agents take the method seriously.
3. **Write the rules.** The few non-negotiables (safety limits, approvals, what counts as evidence, when to stop).
4. **Write the steps.** Ordered, tool-agnostic where possible, with the project-specific tools listed separately.
5. **Write the output contract.** What the user sees at the end, in plain words, lead with the result.
6. **Save in four places:**
   - project method doc: `docs/methods/<NAME>-METHOD.md` (with the project's tools and paths);
   - personal skill: `~/.claude/skills/<name>/SKILL.md` (generic, no project paths in the steps);
   - memory: a feedback memory linking both, plus its index line;
   - the user's public methods repo (generic doc + skill), committed and pushed, after the user confirms the repo.
7. **Keep content clean.** No proprietary data, secrets, user names or private paths in the published copy. Methods
   copied from someone else are linked with credit, not republished.

## Output to the user

One line per place it was saved, plus the trigger phrase to invoke it next time.
