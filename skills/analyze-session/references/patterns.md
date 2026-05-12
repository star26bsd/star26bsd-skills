# Inefficiency Patterns & Recommendations

## Patterns

### Failed tool calls

`.message.role === "toolResult"` with `.message.isError === true`. Note the tool, args, preceding context, and whether the same op succeeded later.

### Repeated attempts

Same tool called multiple times with tweaked args before succeeding — especially `bash`. Group by tool + similar args, count attempts.

### Detours

Many `read` calls exploring unrelated files; `write`/`edit` later undone; `bash` exploration producing nothing useful; switching approaches between turns.

### Re-work

Multiple `edit` calls on the same file where one would suffice. Re-reading files already seen.

## Recommendation mapping

For each inefficiency found, recommend a concrete repo addition:

| Inefficiency | Recommendation |
|---|---|
| `bash` commands fail from wrong assumptions | Add environment setup to CLAUDE.md / AGENTS.md |
| Many `read` calls exploring codebase | Add architecture doc, better file index in CLAUDE.md |
| Wrong tool used repeatedly | Add tool usage examples to a skill or CONTEXT.md |
| Failed `write`/`edit` from type errors | Add type-check, improve test infrastructure |
| Sandbox restrictions block work | Add escape-hatch extension, document sandbox boundaries |
| Agent re-reads same files | Improve compaction strategy, context window notes |
| Long detour finding right approach | Add tracer-bullet examples or how-to sections to docs |
| Repeated edit cycles on same file | Add format/lint auto-fix, code conventions doc |

## Scoring impact

When prioritizing recommendations, consider:

1. **Frequency**: how many times did this inefficiency occur?
2. **Cost**: how many extra turns did each occurrence cost?
3. **Preventability**: how easy is the fix? (doc change vs. tooling change vs. architectural change)
4. **Side benefits**: does the fix help in other scenarios too?
