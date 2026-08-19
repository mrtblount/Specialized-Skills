# tune-up

A mechanic for anything that drives Claude — skills, prompts, project
instructions, agent setups. You describe what you want the thing to do, how
you work, and what's going wrong (if anything); tune-up reads every file,
diagnoses where it fights your intent or your platform, fixes it, and proves
the fix using your own words before handing it back.

It works at any stage:

- **Just downloaded** — check and adapt something before you ever run it
- **Misbehaving** — "I asked it to audit my page and it started changing things"
- **Working but rough** — trim, retarget, and personalize a thing you already like

The yardstick is *your* intent and environment — not an abstract quality
rubric. Your copy of a skill belongs to you; tailoring it to one person is
the point.

## Install

**claude.ai (easiest):** download [`tune-up.zip`](https://github.com/mrtblount/Specialized-Skills/raw/main/tune-up.zip),
then in claude.ai go to **Settings → Capabilities** (where skills are
managed) and upload the zip. If you're replacing an older version, remove it
first.

**Claude Code / desktop app:** copy this `tune-up/` folder into
`~/.claude/skills/` (all projects) or `<project>/.claude/skills/` (one
project).

## Use

Just talk about the problem in your own words:

> "I have this design skill and I like what it makes, but when I asked it to
> audit my page it started editing instead. Can you look at it?"

or

> "I just downloaded this skill — check it and adapt it to how I work before
> I use it."

tune-up will find the skill's files (or ask you to attach them), interview
you lightly for what it still needs, and walk you through a "when you say X,
it will now do Y" map before anything ships.

## Files

| File | Role |
|------|------|
| `SKILL.md` | The operating loop: Listen → Read → Diagnose → Fix → Prove → Hand back |
| `references/examination.md` | The six-part exam: intent routing, platform fit, packaging, model fit, scope fit, coherence |
| `references/repairs.md` | Repair patterns: trigger surgery, platform substitution, de-quota pass, packaging, prove-it protocol |
