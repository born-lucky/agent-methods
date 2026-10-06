---
name: proof-first
description: Proof-first method for reimplementing or porting an existing system (decomp rewrites, game ports, clones of a reference app). Before writing code for a system, the agent proves from the original how it actually works (architecture, stored data, behaviour, ground truth) in a cited proof spec, gets it reviewed, and only then builds. Use on /proof-first, "prove it first", "proof before building", or whenever an agent is about to build or "fix" part of a rewrite whose original architecture hasn't been proved yet, especially after a result "looks wrong" despite passing its own tests.
---

# Proof-first

No proof, no code. When you are rewriting something that already exists, the original is the specification. Agents go
wrong when they build on a plausible model of the original and then test against their own reading. Proof-first makes
them prove the model first.

## When it applies

- Building a system of a port/rewrite for the first time.
- Changing a system whose behaviour the user says is wrong ("nothing like the original", "it's the wrong anims").
- Any time a fix would assume an architecture (one mesh vs two, which object owns a value, when a branch runs) that
  hasn't been cited.

Small local fixes inside an already-proved system skip a new spec, but they cite the spec they rely on.

## Step 1: write the proof spec

One file per system (in a project that has a methods/state folder, use it, e.g. `state/proofs/<system>.md`). Every claim
carries a citation: a decompiled function with its address or line, a symbol name, an asset/package path with its
property, a config file and key, a script/bytecode location, or a capture file. "Engines usually do it like this" is not
a citation.

1. **Architecture.** The objects, components, instances and assets that make up the system in the original, and how
   they connect: ownership, attachment, what runs when. List alternatives you ruled out and why.
2. **Data.** Every stored value the system uses, with its exact value and source. Numbers, not impressions.
3. **Behaviour.** The control flow: entry points, branches and their conditions (mode, perspective, authority,
   platform gates), timing and order.
4. **Ground truth.** The observable result to match: captures of the real thing at the same settings, footage of the
   right version, recorded data, or a live read (only with the user's permission). Say which reference is the bar and
   why it's the right version.
5. **Ours vs proof.** What the current implementation does and every difference, each tied to a file and line.
6. **Open questions.** Anything unproved, marked UNCONFIRMED, with how to prove it. An open architecture question
   blocks acceptance.

If the user has stated how the original works, the spec confirms or refutes that statement explicitly, with citations.

## Step 2: adversarial review

A separate reviewer with fresh context (another agent, or a second model given the cited excerpts) checks each claim
against its citation and tries to break the spec. Disputed points go back to the author until resolved. Then the
orchestrator or the user accepts it.

## Step 3: build against the proof

Only now write code. Tests and captures check against the spec's data and ground truth, never against values our own
code produced. Report results as "matches proof item N" or "differs from proof item N".

## Step 4: when it still looks wrong

If the build matches the spec but still looks wrong next to the original, the spec is wrong or incomplete. Return to
Step 1. Do not tune by eye.

## Output to the user

Lead with the verdict (model confirmed, or model wrong and what the original actually does), then the key evidence in
plain words, then the proposed build plan. Keep citations in the spec file, not the chat.
