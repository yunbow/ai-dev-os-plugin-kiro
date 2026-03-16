---
inclusion: manual
name: ai-dev-os-init
description: AI Dev OS initial setup wizard. Asks about the project's tech stack and scale, then generates an optimal 4-layer structure from templates. Used when starting a new project or introducing AI Dev OS.
---

# AI Dev OS Setup Wizard

## Execution Flow

### 1. Interview the User
- Tech stack (Next.js / Python / Go / etc.)
- Project scale (personal / team / enterprise)
- Existing rule files (.cursorrules, AGENTS.md, .kiro/steering/, etc.)

### 2. Detect and Import Existing Rules

Scan the project for existing configuration and rule files:

| Source | Action |
|--------|--------|
| `.cursorrules` | Convert to L3 guidelines |
| Existing `AGENTS.md` | Classify into L3-L4 |
| Existing `CLAUDE.md` | Classify into L3-L4 |
| `.editorconfig` | Import formatting rules into L3 common/code.md |
| `.eslintrc` / `eslint.config.*` | Extract coding rules into L3 guidelines |
| `biome.json` / `biome.jsonc` | Extract lint/format rules into L3 guidelines |
| `ruff.toml` / `pyproject.toml [tool.ruff]` | Extract Python lint rules into L3 guidelines |
| `.prettierrc` / `prettier.config.*` | Import formatting config into L3 common/code.md |
| `tsconfig.json` (strict settings) | Reference in L3 common/code.md |
| `.github/workflows/*.yml` | Reference CI/CD patterns in L3 common/cicd.md |
| Existing `.kiro/steering/` files | Merge with AI Dev OS structure |

For each detected file:
1. Read its content
2. Extract rules that map to AI Dev OS guideline categories
3. Present the extracted rules to the user for confirmation
4. Write confirmed rules into the appropriate L3 guideline files

### 3. Generate Templates

Generate the following structure:

```
ai-dev-os/
├── 01_philosophy/
│   └── core-values.md          # Minimal placeholder
├── 02_decision-criteria/
│   └── coding.md               # 5-10 basic principles
├── 03_guidelines/
│   ├── common/
│   │   ├── code.md             # Basic rules based on tech stack
│   │   ├── naming.md
│   │   └── security.md
│   └── frameworks/
│       └── [selected-stack]/
│           └── overview.md
└── 04_ai-frames/
    └── kiro.md                 # Kiro steering reference pattern
```

### 4. Generate AGENTS.md
- Auto-insert references to the ai-dev-os directory
- Set up Specificity Cascade
- Kiro recognizes AGENTS.md and always includes it in context

### 5. Set Up Kiro Steering
- Copy AI Dev OS steering rules to `.kiro/steering/`
- Configure foundational files (product.md, tech.md, structure.md) if not present

### 6. Git Submodule Setup (Optional)
- For managing ai-dev-os as a separate repository
