---
name: analyze-session
description: Analyze an AI coding agent session to find inefficiencies — failed tool calls, detours, re-work — and recommend repo improvements that would help agents reach goals faster at equal or higher quality. Use when the user wants to improve their repo's agent-friendliness, debrief a session, or asks "what went wrong in that session" / "how could the agent have done this faster".
license: MIT
metadata:
  author: star26bsd
  version: "1.0"
---

# Analyze Session

Analyze a coding agent session log to find inefficiencies and recommend concrete repo improvements.

## Prerequisites

The agent must produce session logs in JSONL format where each line is a JSON object with a `type` field. See [Session format](#session-format) for the expected schema.

## Quick start

1. **Locate the session log**: the user provides a file path or describes which session to analyze. If unsure, ask.
2. **Read the session JSONL file**.
3. **Parse and categorize** entries: user messages, assistant thinking, tool calls, tool results, model changes.
4. **Identify inefficiencies** — see [Patterns](references/patterns.md) for the full catalog.
5. **Map each inefficiency** to a concrete repo improvement recommendation.

## Session format

The log is a JSONL file. Each line is a JSON object with `type`. The key entry types:

| type | content |
|------|---------|
| `session` | Header: version, working directory, timestamp |
| `message` | Wraps a message object (user, assistant, toolResult, or custom) |
| `model_change` | Model switch during session |
| `thinking_level_change` | Thinking level toggle |

The actual message is nested under `.message`:

- **user**: `.message.role === "user"` — `.message.content` is text or content array
- **assistant**: `.message.role === "assistant"` — `.message.content` array with thinking/text/toolCall blocks
- **toolResult**: `.message.role === "toolResult"` — `.message.toolName`, `.message.isError`

## Analysis method

1. **Count tool calls and failures**: grep for `toolResult` entries with `isError: true`. Group by tool name.
2. **Detect repeated attempts**: same tool called multiple times with tweaked args before succeeding — especially shell commands and file edits.
3. **Find detours**: many read calls exploring unrelated files; writes/edits later undone; shell exploration producing nothing useful; switching approaches between turns.
4. **Spot re-work**: multiple edits on the same file where one would suffice; re-reading files already seen.

See [references/patterns.md](references/patterns.md) for detailed patterns and a full recommendation mapping table.

## Output format

Present findings as:

1. **Session summary**: duration, turns, tools used, model(s)
2. **Inefficiency log**: chronological or grouped by pattern, with entry line numbers
3. **Top recommendations**: 3–5 highest-impact repo improvements, each with:
   - What to add (file, section, or tool)
   - Which inefficiencies it addresses
   - Expected impact (fewer turns, fewer failures, faster completion)

Keep recommendations actionable and concrete — specific file paths and section names.
