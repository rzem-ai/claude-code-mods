# context-bar

Your context window as a stacked bar above the prompt, a colour per category, with token counts and the compaction point.

The bar follows `/context`'s breakdown (system prompt, tools, MCP tools, memory files, skills, messages, free space), gives each used category its own colour, and draws the messages slice in the accent colour since that's the one that grows. A legend underneath lists tokens and shares, and a mark shows where auto-compaction runs. It refreshes after each turn and after a `/compact`, using Claude Code's own local estimate, so it makes no token-count calls.

`/context-bar` hides or shows it, and the choice is kept across sessions.

It shares the space above the prompt with the other band mods; see [Stacking bands](../README.md#stacking-bands) to set the order.

## Install

In a Claude Code session (2.1.287 or later):

```
/plugin marketplace add rzem-ai/claude-code-mods
/plugin install context-bar@claude-code-mods
```

Or load this folder for one session: `claude --plugin-dir ./context-bar`

## What it reaches

| Mod | Network | Runs processes | Files | Calls a model | Sends data anywhere |
| --- | --- | --- | --- | --- | --- |
| context-bar | No | No | Reads the band order file | No | No |

Run `claude plugin validate ./context-bar` to list every event it hooks and every call it makes. See the [repository README](../README.md#security) for the full security notes.

Part of [claude-code-mods](https://github.com/rzem-ai/claude-code-mods) by [rzem-ai](https://github.com/rzem-ai). MIT licensed.
