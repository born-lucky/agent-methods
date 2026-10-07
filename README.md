# agent-methods

Working methods for AI coding agents doing large rewrites and ports, packaged as Claude Code skills. Each one came out
of a real project where the default way of working failed, and is written so the next session applies it without being
told.

| Method | Use it when | Skill |
|---|---|---|
| **Staging** | A big rewrite is moving on every front and the user can't actually use anything yet | `skills/staging` |
| **Proof-first** | An agent is about to build or "fix" part of a port without having proved how the original works | `skills/proof-first` |
| **Reader** | The port matches the original's code on paper but still comes out wrong | `skills/reader-method` |
| **Skillify** | The user names a new way of working and it should stick for future sessions | `skills/skillify-method` |
| **PDF Reference Synthesis Insight** | A hard-won understanding of a mechanism must never be lost or re-derived | `skills/pdf-reference-synthesis` |

Related, by others: the **Spreadsheet Method** and **Database Method** from
[phoenixfire808/rustports](https://github.com/phoenixfire808/rustports) (evidence-first specs and decomp-to-database).

## Install

Copy a skill folder into `~/.claude/skills/` (personal) or `.claude/skills/` (one project):

```sh
git clone https://github.com/born-lucky/agent-methods
cp -r agent-methods/skills/* ~/.claude/skills/
```

Claude Code picks them up on the next session. Invoke with `/staging`, `/proof-first`, `/reader-method`,
`/skillify-method`, `/pdf-reference-synthesis`, or just describe the situation; each skill's description lists its triggers.

## How they fit together

Staging decides **what** to work on and when it counts as done. Proof-first decides **when you may write code**: only
after proving how the original works. Reader checks **what the original actually produces** at runtime when a proved port
still looks wrong. Skillify turns the next lesson into another method like these.

## License

MIT
