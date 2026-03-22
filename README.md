# AI Dev OS Plugin — Kiro

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)

A Kiro plugin that integrates the **AI Dev OS** 4-layer model into Kiro's Steering Rules and Hooks system.

**Part of [AI Dev OS](https://github.com/yunbow/ai-dev-os)** — a framework for turning tacit knowledge into enforceable AI coding rules ([Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)).
Requires [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) set up in your project.

## Why This Plugin?

Integrate AI Dev OS guidelines into **Kiro's steering system**:

- **11 Steering Rules** — `#ai-dev-os-check`, `#ai-dev-os-scan`, `#ai-dev-os-extract` and more
- **3 Auto Steering** — Philosophy advisor, principle checker, guideline auditor
- **2 File Match Rules** — Auto-check on code files, L1-L2 dependency warnings
- **One command setup** — `npx ai-dev-os init --rules typescript --plugin kiro`

![AI Dev OS Check & Fix Report](docs/images/ai-dev-os-check.png)

## Quick Start

```bash
npx ai-dev-os init --rules typescript --plugin kiro
```

> The CLI adds submodules, copies the AGENTS.md template, and copies steering rules and hooks to `.kiro/` automatically.
> See [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli) for details.

Requires [Kiro](https://kiro.dev/) >= 1.0.0 and AI Dev OS layer files (L1-L3) in your project ([TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)).

<details>
<summary>Manual Setup</summary>

**Option A: Submodule**

```bash
# 1. Add AI Dev OS rules as submodule
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# For Python projects:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. Add this plugin as submodule
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/ .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/ .kiro/hooks/
```

**Option B: Direct Copy**

```bash
# 1. Add rules as submodule (same as above)
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. Clone and copy plugin files
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
```

3. Invoke `#ai-dev-os-init` in Kiro chat to set up the 4-layer structure
4. Start coding — steering rules and hooks will guide you automatically

See [Operation Guide](./docs/operation-guide.md) for detailed instructions.

</details>

## Steering Rules

### Manual Steering (invoke via `#name` in chat)

| Steering Rule | Invocation | Description |
|---------------|------------|-------------|
| **Init** | `#ai-dev-os-init` | Setup wizard — introduces AI Dev OS to a project in 30 minutes |
| **Check** | `#ai-dev-os-check` | Checks code changes against guidelines (supports `git diff`, staged, branch comparison) |
| **Scan** | `#ai-dev-os-scan` | Full project-wide compliance scan of ALL source files |
| **Review** | `#ai-dev-os-review` | Pre-PR self-review combining L3 compliance + L2 design review + L1 alignment |
| **Extract** | `#ai-dev-os-extract` | Extracts new rules from code review diffs (Rule Harvesting) |
| **Why** | `#ai-dev-os-why` | Traces a rule back through L3→L2→L1 to explain its rationale |
| **Plan** | `#ai-dev-os-plan` | Creates an implementation plan with guideline checklists before coding |
| **Ticket** | `#ai-dev-os-ticket` | Generates a ticket (local file or GitHub Issue) with implementation summary and checklist candidates |
| **Audit** | `#ai-dev-os-audit` | Audits 4-layer health: dependency rule, freshness, coverage, consistency |
| **Evolve** | `#ai-dev-os-evolve` | Analyzes recent commits to propose L1-L2 updates (SECI spiral) |
| **Report** | `#ai-dev-os-report` | Generates compliance summary for teams and stakeholders |

### Auto Steering (activated automatically)

| Steering Rule | Activation | Description |
|---------------|------------|-------------|
| `philosophy-advisor` | Architecture/design decisions | L1-based judgment support |
| `principle-checker` | Code change discussions | L2 alignment verification |
| `guideline-auditor` | Guideline maintenance discussions | L3 coverage & consistency audit |

### File Match Steering (activated on matching files)

| Steering Rule | File Pattern | Description |
|---------------|-------------|-------------|
| `guideline-compliance` | `**/*.{ts,tsx,py,go,js,jsx}` | Lightweight guideline check on code files |
| `layer-dependency` | `**/01_philosophy/**`, `**/02_decision-criteria/**` | Dependency rule violation warning |

## Hooks

| Event | Trigger | Action |
|-------|---------|--------|
| File Save | Code files | Guideline compliance quick check |
| Pre Tool Use (terminal: git commit) | Before commit | Reminder to run `#ai-dev-os-check` |
| User Prompt Submit | Implementation-related prompts | Suggests `#ai-dev-os-plan` |

<details>
<summary>Package Structure</summary>

```
ai-dev-os-plugin-kiro/
├── steering/
│   ├── ai-dev-os-init.md              # Setup wizard (manual)
│   ├── ai-dev-os-check.md             # Guideline compliance check (manual)
│   ├── ai-dev-os-scan.md              # Full project-wide compliance scan (manual)
│   ├── ai-dev-os-review.md            # Pre-PR self-review (manual)
│   ├── ai-dev-os-extract.md           # Rule Harvesting from code (manual)
│   ├── ai-dev-os-why.md               # Explain rule rationale (manual)
│   ├── ai-dev-os-plan.md              # Guideline-aware implementation planning (auto)
│   ├── ai-dev-os-ticket.md            # Ticket generation (manual)
│   ├── ai-dev-os-audit.md             # 4-layer health audit (manual)
│   ├── ai-dev-os-evolve.md            # SECI spiral feedback (manual)
│   ├── ai-dev-os-report.md            # Compliance report generation (manual)
│   ├── philosophy-advisor.md          # L1-based architecture judgment (auto)
│   ├── principle-checker.md           # L2 alignment verification (auto)
│   ├── guideline-auditor.md           # L3 coverage & consistency audit (auto)
│   ├── guideline-compliance.md        # Auto check on code files (fileMatch)
│   └── layer-dependency.md            # Dependency rule warning (fileMatch)
├── hooks/
│   └── hooks.json                     # Lifecycle event hooks
├── checklist-templates/
│   ├── python.md                      # Python-specific checklist
│   ├── go.md                          # Go-specific checklist
│   └── nextjs.md                      # Next.js-specific checklist
├── templates/
│   ├── AGENTS.md.template             # AGENTS.md template with cascade
│   ├── ai-dev-os-starter/             # Minimal setup template
│   └── ai-dev-os-full/                # Full 4-layer template
└── docs/
    └── operation-guide.md             # Detailed usage instructions
```

</details>

## Specificity Cascade

When rules conflict: framework-specific > common > project-specific > decision criteria > philosophy. [→ Details](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## Related

| Repository | Description |
|---|---|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | Framework specification and theory |
| [ai-dev-os-rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js guidelines |
| [ai-dev-os-rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI guidelines |
| [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Skills, Hooks, and Agents for Claude Code |
| [ai-dev-os-plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor) | Cursor Rules (.mdc) |
| [ai-dev-os-cli](https://github.com/yunbow/ai-dev-os-cli) | Setup automation — `npx ai-dev-os init` |

## License

[MIT](./LICENSE)

---

Languages: English | [日本語](docs/i18n/ja/README.md) | [简体中文](docs/i18n/zh-CN/README.md) | [한국어](docs/i18n/ko/README.md) | [Español](docs/i18n/es/README.md)
