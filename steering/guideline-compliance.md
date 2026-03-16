---
inclusion: fileMatch
fileMatchPattern: ["**/*.ts", "**/*.tsx", "**/*.js", "**/*.jsx", "**/*.py", "**/*.go"]
name: guideline-compliance
description: Lightweight AI Dev OS guideline compliance guidance for code files. Automatically active when editing code files.
---

# AI Dev OS Guideline Compliance

When editing code files in this project, follow the AI Dev OS guidelines.

## Behavior

1. Check if the project has an `ai-dev-os/` directory with guidelines
2. If guidelines exist, ensure your changes comply with the applicable rules
3. Only flag clear violations — do not block for minor warnings
4. When a violation is found, explain:
   - Which rule was violated
   - Which guideline file contains the rule
   - The L2 principle behind it (if traceable)

## Quick Reference

- Check `ai-dev-os/03_guidelines/common/code.md` for basic coding rules
- Check `ai-dev-os/03_guidelines/frameworks/` for framework-specific rules
- Refer to AGENTS.md for the full guideline file list and priority cascade
