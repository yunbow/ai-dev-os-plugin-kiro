---
inclusion: manual
name: ai-dev-os-report
description: Generates an AI Dev OS compliance report for teams and stakeholders. Includes compliance rate trends, major violations, and improvement proposals for a specified period. Used for weekly or monthly reporting.
---

# AI Dev OS Compliance Report Generation

## Execution Flow

### 1. Determine Period

Determine the target period from the user's request (default: 1w).

### 2. Collect Data

- Retrieve commits for the target period using `git log`
- Identify relevant guidelines for each changed file
- Aggregate past check results if available

### 3. Generate Report

Output in the following format:

```markdown
## AI Dev OS Compliance Report
**Period**: YYYY-MM-DD — YYYY-MM-DD

### Summary
- Total commits: N
- Checked: N
- Compliance rate: N%

### Compliance Rate Trend
| Week | Compliance Rate | Violations | Main Violations |
|------|----------------|------------|-----------------|

### Major Violation Patterns
| Pattern | Occurrences | Guideline | Improvement Proposal |
|---------|-------------|-----------|---------------------|

### Improvement Proposals
1. ...
2. ...
```
