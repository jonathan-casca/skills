# jonathan-casca/skills

Public Agent Skills for Cursor, Codex, and Claude Code.

## Skills

| Skill | Invoke | Models | Host |
| --- | --- | --- | --- |
| [`plan-team`](./plan-team/) | `/plan-team` | Mixed (GPT + Claude + Grok + GLM) | Cursor |
| [`plan-team-codex`](./plan-team-codex/) | `/plan-team-codex` | GPT-only (`gpt-5.6`, `gpt-5.4`, `gpt-5.6-terra`, `gpt-5.4-mini`) | Codex / Cursor |
| [`plan-team-claude`](./plan-team-claude/) | `/plan-team-claude` | Claude-only (Opus / Sonnet variants) | Claude Code / Cursor |
| [`platform-readiness-prompts`](./platform-readiness-prompts/) | — | Prompt pack | Any |

## Install

### Cursor

1. **Customize → Rules → Add Rule → Remote Rule (GitHub)**
2. Paste: `https://github.com/jonathan-casca/skills`
3. Run `/plan-team`, `/plan-team-codex`, or `/plan-team-claude`

Or copy folders into `~/.cursor/skills/` / `<repo>/.cursor/skills/`.

### Codex

```bash
git clone https://github.com/jonathan-casca/skills.git
cp -R skills/plan-team-codex ~/.codex/skills/plan-team-codex
```

### Claude Code

```bash
git clone https://github.com/jonathan-casca/skills.git
cp -R skills/plan-team-claude ~/.claude/skills/plan-team-claude
```

## License

MIT
