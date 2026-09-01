# Skills

Agent skills by Joe Paravisini. Every skill follows the [Agent Skills spec](https://agentskills.io/specification). CI validates each skill on every push.

## Skills

| Skill | What it does |
|-------|--------------|
| [catch-me-up](skills/catch-me-up/SKILL.md) | Summarizes a stale session: goal, decisions, blocker, remaining work. |
| [dafuq](skills/dafuq/SKILL.md) | Rewords the agent's last response when it confused you. |

## Install

Install everything as a Claude Code plugin:

```
/plugin marketplace add jparavisini/skills
/plugin install joe-skills@jparavisini-skills
```

Or copy one skill into your personal skills folder:

```bash
cp -r skills/dafuq ~/.claude/skills/
```

## Layout

Each skill is one directory under `skills/`. The directory name matches the `name` field in its SKILL.md.

```
skills/skill-name/
├── SKILL.md      # required: frontmatter + instructions
├── scripts/      # optional: executable code
├── references/   # optional: docs loaded on demand
└── assets/       # optional: templates, data files
```

## Validate locally

Run the same check CI runs:

```bash
uvx --from 'git+https://github.com/agentskills/agentskills.git#subdirectory=skills-ref' \
  skills-ref validate skills/dafuq
```

## License

MIT. See [LICENSE](LICENSE).
