# jidoka

[![skills.sh](https://skills.sh/b/jparavisini/skills)](https://skills.sh/jparavisini/skills)

Agent skills by Joe Paravisini, packaged as the `jidoka` plugin. Jidoka is the Toyota principle of automation with a human touch: the line stops itself when something goes wrong, and a person fixes the cause. Each skill here does the least that gets the job done.

Every skill follows the [Agent Skills spec](https://agentskills.io/specification). CI validates each skill on every push.

## Skills

| Skill                                                          | What it does                                                                                              |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| [catch-me-up](skills/catch-me-up/SKILL.md)                     | Summarizes a stale session: blocker, goal, decisions, remaining work.                                     |
| [dafuq](skills/dafuq/SKILL.md)                                 | Rebuilds a long, vague agent response so it leads with the decision you must make.                        |
| [disambiguate](skills/disambiguate/SKILL.md)                   | Rewrites skills, prompts, and agent instruction files so each sentence is necessary, clear, and testable. |
| [strategic-programming](skills/strategic-programming/SKILL.md) | Applies John Ousterhout's _A Philosophy of Software Design_ when you plan or review software design.      |

## Output style

[action-first](output-styles/action-first.md) shapes every response so you can act on it: the next action first, numbered steps, no preamble or closer. `dafuq` applies the same rules to one response.

The Claude Code plugin installs it. Select it with `/output-style`. In other agents, paste it into `AGENTS.md`.

## Install

Install with the [skills CLI](https://skills.sh) for Claude Code, Codex, Cursor, and other agents:

```bash
npx skills add jparavisini/skills
```

Install one skill, for every project:

```bash
npx skills add jparavisini/skills --skill dafuq -g
```

Or install everything as a Claude Code plugin:

```
/plugin marketplace add jparavisini/skills
/plugin install jidoka@jparavisini
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

Each output style is one Markdown file under `output-styles/`.

`skills.sh.json` groups the skills on the [skills.sh page](https://skills.sh/jparavisini/skills). Add each new skill to a group there.

## Validate locally

Run the same check CI runs:

```bash
for skill in skills/*/; do
  uvx --from 'git+https://github.com/agentskills/agentskills.git#subdirectory=skills-ref' \
    skills-ref validate "$skill"
done
```

## Credits

`strategic-programming` condenses John Ousterhout's [_A Philosophy of Software Design_](https://web.stanford.edu/~ouster/cgi-bin/book.php). The ideas and terms are his. Read the book.

## License

MIT. See [LICENSE](LICENSE).
