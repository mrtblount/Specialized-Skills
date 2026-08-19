# Specialized Skills

A collection of specialized [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills for various workflows and integrations. Each skill gives Claude a focused capability you can drop into your setup and use immediately.

## What Are Claude Skills?

Claude Skills are reusable instruction sets (`.md` files) that extend Claude Code with specialized abilities. Place a skill folder in `~/.claude/skills/` and invoke it by name.

## Skills

| Skill | Description |
|-------|-------------|
| [notion-ai-orchestrator](./notion-ai-orchestrator/) | Orchestrate Notion AI through the Claude Chrome Extension — create databases, search content, modify pages, and set up automations by delegating to Notion's built-in AI agent. |
| [tune-up](./tune-up/) | Audit, adapt, and repair any skill, prompt, or agent setup so it does exactly what its owner intends — diagnose intent-routing, platform-fit, and packaging problems, fix them, and prove the fix with the owner's own words. Works on claude.ai and Claude Code ([one-click zip](./tune-up.zip)). |

## Usage

1. Clone this repo (or copy individual skill folders)
2. Place skill folders in `~/.claude/skills/`
3. Invoke skills by name in Claude Code

## Related Repos

- [Spec-to-Ship](https://github.com/mrtblount/Spec-to-Ship) — Product development pipeline (PRD builder + Spec-Driven Development) for one-shot implementation
- [Skill Ecosystem](https://github.com/mrtblount/skill-ecosystem) — Framework, builder tools, and skill development infrastructure

## Links

- [tonyblount.com](https://tonyblount.com) — Portfolio
- [Four30.co](https://four30.co) — Consulting
- [LinkedIn](https://www.linkedin.com/in/williamblount/)

## License

MIT
