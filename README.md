# project-readme-skill

A Claude Code skill that creates, updates, and audits `README.md` files for any project. When invoked, it walks through the project structure and writes a complete, accurate README covering setup, tech stack, models, API endpoints, tests, contributing guidelines, and more.

## Table of Contents

- [Setup](#setup)
- [Contributing](#contributing)
- [License](#license)

## Setup

This skill is installed into Claude Code by placing the `SKILL.md` file in a location Claude Code scans for skills. The recommended approach is to add it to your user-level skills directory so it is available across all projects.

**Prerequisites**

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and authenticated

**Install**

Clone the repository and symlink (or copy) `SKILL.md` into your Claude Code skills directory:

```bash
git clone https://github.com/alon-p/project-readme-skill.git
mkdir -p ~/.claude/skills
cp project-readme-skill/SKILL.md ~/.claude/skills/project-readme-skill.md
```

Once installed, the skill is available in any Claude Code session as `/project-readme-skill`.

**Usage**

Open a project in Claude Code and run:

```
/project-readme-skill
```

Claude will check for an existing `README.md`, ask a few setup questions, analyze the project structure, and write or update the README section by section.

## Contributing

Contributions are welcome. Please follow these guidelines:

- **Branch naming:** use `feat/<short-description>` for new features and `fix/<short-description>` for bug fixes
- **Pull requests:** open a PR against `main` with a clear description of what changed and why
- **Code style:** keep the skill instructions in `SKILL.md` clear and imperative — each step should tell Claude exactly what to do, not describe it loosely
- **Testing:** manually run the skill against a sample project before submitting to confirm the output is correct and complete

## License

This project is licensed under the MIT License. See [LICENSE.md](LICENSE.md) for details.
