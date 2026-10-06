---
name: reader-method
description: The reader method for game/app reimplementations: read the ORIGINAL's live runtime state (read-only memory read of the running original, offline, no anti-cheat) and diff it value by value against the rewrite in the same state, to find exactly which link is wrong when the port "matches the code" but still looks or behaves wrong. Use on /reader-method, "read it from the game", "read the real values", or when a rewrite's visual/numeric result differs from the original despite cited proofs.
---

# Reader method

When a reimplementation matches the original's code on paper and still comes out wrong, stop theorising and read the
original's actual runtime values. One read beats hours of hypotheses: it shows which value differs and where.

## Rules

1. **Read only.** Use ReadProcessMemory or an equivalent read-only dump. Never write to the original's memory or
   inject code.
2. **Offline, no anti-cheat.** Run the original locally (single-player / local play), never on online servers. Before
   reading, confirm no anti-cheat process or service is running. If one is, stop and find a launch path without it.
3. **The user approves it.** Memory reads are blocked by default in auto mode; the user grants the permission for the
   reader script. Don't try to route around a denial.
4. **Same state on both sides.** Match loadout, view, stance, look angle and animation time as closely as possible,
   and record what the original was doing at the moment of the read.

## Steps

1. **Find the chain to the values.** Use symbols (PDB/exports) for globals and the type layouts (from the PDB or the
   decompiler) for field offsets. For an Unreal game the usual chain is GWorld -> OwningGameInstance ->
   LocalPlayers[0] -> PlayerController -> Pawn -> Mesh -> ComponentSpaceTransforms, plus ComponentToWorld,
   ControlRotation and the camera manager's cached POV. Verify each hop with a sanity check (bone count, pointer
   plausibility) and fail loudly when one doesn't hold.
2. **Write a small read-only reader script** that dumps the values to JSON with names, keeping the offsets and their
   sources in its header.
3. **Dump ours in the same state** through a probe in the rewrite (a test that poses the same character and writes the
   same JSON shape).
4. **Diff in a shared frame:** component/mesh space; each bone relative to its parent and to a reference bone; and
   both against the reference pose, which shows which bones the original moves at all. Rank by size.
5. **Trace the largest differences to their source in the rewrite** (decoder, pose builder, procedural layer, attach,
   camera), prove the original's behaviour from its code (proof-first), fix, and **re-read to confirm** the diff closes.

## Output to the user

Lead with the biggest mismatch in plain words ("our shoulders sit 13 cm off; the real game keeps them at the
skeleton's length"), then the table of the top differences, then the fix and its confirmation read.
