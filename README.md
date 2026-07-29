# star26bsd-skills

Personal [Agent Skills](https://agentskills.io) collection — reusable, cross-platform skills for AI coding agents.

Each skill is a self-contained directory with a `SKILL.md` file following the [Agent Skills specification](https://agentskills.io/specification). Agents discover skills through progressive disclosure: metadata loads at startup, full instructions only when the task matches.

## Skills

| Skill | Description |
|-------|-------------|
| [analyze-session](skills/analyze-session/) | Analyze an AI coding agent session to find inefficiencies — failed tool calls, detours, re-work — and recommend concrete repo improvements |
| [de-spoon](skills/de-spoon/) | Review and tighten proposed implementation work before coding by separating current responsibility from existing contracts, false assumptions, and speculative machinery |

## Installing

### pi (custom agent harness)

```bash
cp -r skills/<skill-name> ~/.pi/agent/skills/
```

### Claude Code

```bash
# Register this repo as a plugin marketplace
/plugin marketplace add star26bsd/star26bsd-skills
```

### Other agents

Copy any skill directory into your agent's skills folder:

- **VS Code / Copilot**: `~/.copilot/skills/` or `~/.claude/skills/`
- **Codex CLI**: `~/.codex/skills/`
- **Cursor**: `~/.cursor/skills/`

## Creating a new skill

See the [Agent Skills specification](https://agentskills.io/specification) for the full format. Minimal template:

```
skill-name/
└── SKILL.md    # YAML frontmatter (name, description) + Markdown body
```

Optional subdirectories: `scripts/`, `references/`, `assets/`.

## License

[MIT](LICENSE)
