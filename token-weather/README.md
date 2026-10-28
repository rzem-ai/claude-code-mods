# token-weather

A live forecast of the context window above the prompt, with a prompt-cache countdown.

Context use reads as weather: Clear up to 25%, then Cloudy, Showers, Storm, and Compact soon past 90%, with a sparkline of the last dozen turns. Beside it, a countdown of how long the prompt cache stays warm after the last request. It moves in 15 or 30 second steps, ticks every second in the last two minutes, and warns in the last one.

The cache lifetime (5 minutes or 1 hour) is detected from the usage Claude writes into the session transcript and remembered for the next session. To force one, set `cacheTtl` to `5m` or `1h` in `/config` (or `pluginConfigs` in settings); `auto` is the default. A `/clear` or resume resets the countdown. If your status line runs cache-clock, the countdown steps aside for its exact one.

It shares the space above the prompt with the other band mods; see [Stacking bands](../README.md#stacking-bands) to set the order.

## Install

In a Claude Code session (2.1.287 or later):

```
/plugin marketplace add rzem-ai/claude-code-mods
/plugin install token-weather@claude-code-mods
```

Or load this folder for one session: `claude --plugin-dir ./token-weather`

## What it reaches

| Mod | Network | Runs processes | Files | Calls a model | Sends data anywhere |
| --- | --- | --- | --- | --- | --- |
| token-weather | No | `tail` (the end of this session's transcript) | Reads this session's transcript, your settings, and the band order file | No | No |

Run `claude plugin validate ./token-weather` to list every event it hooks and every call it makes. See the [repository README](../README.md#security) for the full security notes.

Part of [claude-code-mods](https://github.com/rzem-ai/claude-code-mods) by [rzem-ai](https://github.com/rzem-ai). MIT licensed.
