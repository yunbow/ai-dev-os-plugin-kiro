# AI Dev OS Plugin — Kiro — Operation Guide

English | [日本語](./i18n/ja/operation-guide.md) | [简体中文](./i18n/zh-CN/operation-guide.md) | [한국어](./i18n/ko/operation-guide.md) | [Español](./i18n/es/operation-guide.md)

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Installation](#2-installation)
3. [Initial Setup](#3-initial-setup)
4. [Daily Workflow](#4-daily-workflow)
5. [Periodic Maintenance](#5-periodic-maintenance)
6. [Team Onboarding](#6-team-onboarding)
7. [Language Policy](#7-language-policy)
8. [Troubleshooting](#8-troubleshooting)

---

## 1. Prerequisites

- [Kiro](https://kiro.dev/) >= 1.0.0
- AI Dev OS layer files (L1-L3) set up in your project (see templates: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python))

---

## 2. Installation

### Option A: Copy Steering Rules (Recommended)

Copy the steering rules and hooks into your project's `.kiro/` directory:

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
cp -r ai-dev-os-plugin-kiro/checklist-templates/ .kiro/checklist-templates/
```

### Option B: Git Submodule

Add as a submodule to keep AI Dev OS updates separate from your project:

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
```

Then symlink or copy the steering rules:

```bash
cp -r .kiro/plugins/ai-dev-os/steering/* .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/* .kiro/hooks/
```

### Hook Setup

Kiro hooks can also be configured via the Hook UI:
1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Type "Kiro: Open Kiro Hook UI"
3. Create hooks matching the configurations in `hooks/hooks.json`

---

## 3. Initial Setup

### Run the Setup Wizard

In Kiro chat, invoke:
```
#ai-dev-os-init [tech-stack]
```

Example:
```
#ai-dev-os-init nextjs
```

The wizard will:
1. Ask about your tech stack, project scale, and existing rule files
2. Detect and import existing rules (`.cursorrules`, `AGENTS.md`, `.eslintrc`)
3. Generate the 4-layer directory structure
4. Create an `AGENTS.md` with guideline references and Specificity Cascade
5. Optionally set up Kiro foundational files (product.md, tech.md, structure.md)

### Verify Setup

After initialization, confirm the structure:

```
ai-dev-os/
├── 01_philosophy/
├── 02_decision-criteria/
├── 03_guidelines/
│   ├── common/
│   └── frameworks/
└── 04_ai-frames/
```

---

## 4. Daily Workflow

### 4.1 Planning Before Implementation

For non-trivial changes, create a guideline-aware plan first. The `ai-dev-os-plan` steering rule has `inclusion: auto`, so Kiro will automatically suggest it when you discuss implementation tasks. You can also invoke it explicitly:

```
#ai-dev-os-plan Add user authentication with JWT
```

This will:
1. Analyze your request and identify affected files
2. Map files to relevant AI Dev OS guidelines
3. Generate a checklist of applicable rules
4. Present the plan for your approval before any code is written

### 4.2 Creating Tickets Instead of Implementing

When you want to defer implementation — e.g., for team assignment or backlog management — create a ticket instead:

```
#ai-dev-os-ticket Add user authentication with JWT
```

This will:
1. Perform the same analysis as `#ai-dev-os-plan` (affected files, guideline mapping, checklist)
2. Ask where to create the ticket (if not configured in AGENTS.md):
   - **Local file**: saves as `TICKET-001-add-user-auth.md` in the specified directory
   - **GitHub Issue**: creates an issue via `gh issue create`
3. Present a preview for your approval
4. Create the ticket — **without writing any code**

To pre-configure the ticket destination, add to your project's `AGENTS.md`:

```markdown
## Ticket Settings
- output: file
- path: docs/tickets/phase1
```

Or for GitHub Issues:

```markdown
## Ticket Settings
- output: github-issue
```

### 4.3 Writing Code

Write code as usual. The steering rules and hooks will automatically:
- Check guideline compliance when saving code files (via `guideline-compliance` fileMatch steering)
- Warn about dependency rule violations when editing L1-L2 files (via `layer-dependency` fileMatch steering)
- Remind you to run compliance checks before committing

### 4.4 Before Committing

Run the compliance check:

```
#ai-dev-os-check
```

This will:
1. Parse `AGENTS.md` to find applicable guidelines
2. Get changed files from `git diff`
3. Map files to relevant guidelines
4. Check compliance and output a report

### 4.5 After Code Review

When you fix AI-generated code during review, extract new rules:

```
#ai-dev-os-extract [file-path]
```

This will:
1. Analyze the diff to identify *why* changes were made
2. Generate rule candidates in `MUST` / `MUST NOT` format
3. Propose target guideline files and L2 principle links
4. Add rules to guidelines upon approval

### 4.6 Understanding Rules

When a team member questions a rule:

```
#ai-dev-os-why [rule-or-guideline]
```

Example:
```
#ai-dev-os-why "why is any type prohibited?"
```

---

## 5. Periodic Maintenance

### Monthly: Health Audit

```
#ai-dev-os-audit
```

Checks:
- Dependency rule compliance (no tool-specific terms in L1, no framework details in L2)
- Freshness (L1: 5yr, L2: 3yr, L3: 12mo, L4: 4mo)
- Traceability (L3→L2 links, orphaned rules)
- Coverage (guidelines for all file patterns)
- Consistency (no contradicting rules)

### Quarterly: SECI Spiral Evolution

```
#ai-dev-os-evolve
```

Analyzes recent commits and review patterns to propose updates to L1 philosophy and L2 principles. This is the "knowledge spiral" — extracting tacit knowledge from daily practice into explicit principles.

### Weekly/Monthly: Compliance Report

```
#ai-dev-os-report 1w
#ai-dev-os-report 1m
```

Generates a summary report suitable for team meetings or stakeholder updates.

---

## 6. Team Onboarding

### For New Team Members

1. Read `ai-dev-os/01_philosophy/core-values.md` (5 min)
2. Skim `ai-dev-os/02_decision-criteria/` (10 min)
3. Invoke `#ai-dev-os-why` for any rules that seem unclear
4. Start coding — steering rules and hooks will guide compliance automatically

### For Teams Adopting AI Dev OS

1. Invoke `#ai-dev-os-init` on the project
2. Start with the **starter** template (L3 only)
3. Use `#ai-dev-os-extract` after each code review session
4. After 2-4 weeks, run `#ai-dev-os-audit` to identify gaps
5. Gradually build L1-L2 through `#ai-dev-os-evolve`

---

## 7. Language Policy

All source files (steering rules, hooks, templates) are maintained in **English**. This ensures optimal LLM accuracy and broad accessibility. Translated documentation is provided under `docs/i18n/` for reference, but English remains the single source of truth.

---

## 8. Troubleshooting

### Steering rules not activating

- Verify steering files are in `.kiro/steering/` directory
- Check YAML frontmatter is valid (correct `inclusion` mode, proper `fileMatchPattern`)
- For manual steering, invoke with `#name` in chat
- For auto steering, ensure the `description` field matches your conversation context

### Hooks not triggering

- Verify hooks are configured in `.kiro/hooks/` directory
- Alternatively, configure hooks via Kiro Hook UI (`Ctrl+Shift+P` → "Kiro: Open Kiro Hook UI")
- Check that `jq` is installed for command-type hooks (`jq --version`)
- On Windows, ensure bash is available in PATH

### False positive violations

- If a check is too strict, edit the corresponding guideline in `03_guidelines/`
- Use `#ai-dev-os-why` to understand the rule's rationale before removing it
- Consider relaxing the rule rather than removing it entirely

### Performance

- FileMatch steering rules run whenever matching files are in context — keep patterns specific
- For heavy operations, invoke steering rules manually rather than relying on auto inclusion
- Consider splitting large guideline files into smaller, more focused files

### Using Kiro Specs with AI Dev OS

Kiro's spec-driven development (requirements → design → tasks) complements AI Dev OS:
- Use Kiro specs for feature planning and task decomposition
- Use AI Dev OS guidelines as quality gates during spec task execution
- The `Pre Spec Task` and `Post Spec Task` hook events can trigger guideline checks
