# Contributing to AI Dev OS Plugin — Kiro

Thank you for your interest in contributing!

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](https://github.com/yunbow/ai-dev-os-plugin-kiro/issues)
- Specify which steering rule, hook, or template is affected

### Pull Requests

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Commit with a descriptive message
5. Open a Pull Request

### What to Contribute

| Directory | What We Need | Guidelines |
|-----------|-------------|------------|
| `steering/` | Steering rule improvements, new rules | Follow steering rule format (YAML frontmatter with `inclusion`, `name`, `description`). Keep rules focused and concise. |
| `hooks/` | Hook improvements, new event handlers | Follow Kiro hooks format (JSON array with `event`, `filePattern`, `actionType`). Test thoroughly. |
| `templates/` | Template improvements | Templates should follow Two-Tier Context Strategy (10-15 high-impact rules only). |
| `checklist-templates/` | New language checklists, improvements | Keep checklists actionable and verifiable. |

### Steering Rule Development Guidelines

- Each steering rule lives in `steering/{name}.md`
- Required frontmatter: `inclusion` (e.g., `always`, `manual`), `name`, `description`
- Rule content should be clear and actionable
- Keep rules focused on a single concern
- Use concrete examples where possible

### Hook Development Guidelines

- Hooks are defined in `hooks/hooks.json`
- Each hook is a JSON object with `event`, `filePattern`, and `actionType`
- Filter non-source files (node_modules, dist, images, etc.)
- Test with both TypeScript and Python projects

### Cross-Plugin Feature Parity

When adding a new feature to this plugin, consider adding the equivalent to:
- [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) (as skill or hook)
- [ai-dev-os-plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor) (as .mdc rule)

### Translation Guide

- Translations are in `docs/i18n/{lang}/`
- Currently supported: `ja`, `zh-CN`, `ko`, `es`

## Code of Conduct

Be respectful, constructive, and inclusive.

---

Languages: English | [日本語](docs/i18n/ja/CONTRIBUTING.md)
