---
inclusion: fileMatch
fileMatchPattern: ["**/ai-dev-os/01_philosophy/**", "**/ai-dev-os/02_decision-criteria/**"]
name: layer-dependency
description: Warns about dependency rule violations when editing AI Dev OS L1 philosophy or L2 principle files. Ensures upper layers remain tool-agnostic.
---

# AI Dev OS Layer Dependency Rules

## When Editing L1 Philosophy Files

⚠️ **L1 philosophy files must remain tool-agnostic.**

- Do NOT include tool-specific terms (Kiro, Claude Code, Cursor, VS Code, etc.)
- Do NOT include framework-specific terms (Next.js, React, Django, etc.)
- Do NOT include language-specific implementation details
- L1 should express universal values that transcend any specific technology

## When Editing L2 Principle Files

⚠️ **L2 principle files must remain framework-agnostic.**

- Do NOT include framework-specific implementation details
- Do NOT reference specific libraries or packages
- L2 should express design and architecture principles applicable across frameworks
- Language-specific nuances are acceptable, but keep them abstract

## Dependency Direction

The one-way dependency rule must be maintained:

```text
L1 Philosophy → L2 Principles → L3 Guidelines → L4 AI Frames
(most abstract)                              (most specific)
```

Upper layers must NEVER reference lower layers. Each layer should be understandable without knowledge of the layers below it.
