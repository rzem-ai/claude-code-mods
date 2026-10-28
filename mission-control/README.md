# mission-control

Live map of the main agent, its subagents and every tool call, plus a code map of the files they touch.

`/mission` opens a pane with two views of the current turn:

- **who**: the main loop, its subagents and every tool call they make, live.
- **code**: a rendered map of the files Claude reads and edits, the imports between them, a glow on what it is touching right now, and one plain line on each change.

`/mission who` and `/mission code` open straight to a view; `w`, `c` and `q` switch or close it from the pane. A band above the prompt sums the turn up while Claude works and for 30 seconds after.

On macOS and Linux the code map is drawn by headless Chrome or Chromium (it looks for Google Chrome in `/Applications`, then the usual Linux paths) with its own throwaway profile, never your browser's. On Windows it is written as a page and opened in your default browser, which redraws it as things change.

It shares the space above the prompt with the other band mods; see [Stacking bands](../README.md#stacking-bands) to set the order.

## Install

In a Claude Code session (2.1.287 or later):

```
/plugin marketplace add rzem-ai/claude-code-mods
/plugin install mission-control@claude-code-mods
```

Or load this folder for one session: `claude --plugin-dir ./mission-control`

## What it reaches

| Mod | Network | Runs processes | Files | Calls a model | Sends data anywhere |
| --- | --- | --- | --- | --- | --- |
| mission-control | No | Headless Chrome or Chromium to draw the code map (macOS, Linux); `explorer.exe` to open it (Windows) | Reads the files Claude touches, to find their imports; writes the map to `$TMPDIR/mission-control/` (`%TEMP%` on Windows); reads the band order file | Yes, Haiku: after each turn that edits files, the paths and up to 1,500 characters of the edits per file | Only to your Claude model |

The change notes are written from the text of each edit, so whatever goes into a file goes to Haiku with it, whether or not the pane is open.

Run `claude plugin validate ./mission-control` to list every event it hooks and every call it makes. See the [repository README](../README.md#security) for the full security notes.

Part of [claude-code-mods](https://github.com/rzem-ai/claude-code-mods) by [rzem-ai](https://github.com/rzem-ai). MIT licensed.
