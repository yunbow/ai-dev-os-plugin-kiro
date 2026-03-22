# AI Dev OS Plugin — Kiro

[![Lint & Link Check](https://github.com/yunbow/ai-dev-os-plugin-kiro/actions/workflows/lint.yml/badge.svg)](https://github.com/yunbow/ai-dev-os-plugin-kiro/actions/workflows/lint.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](../../../LICENSE)

将 AI Dev OS 4层模型集成到 Kiro 的 Steering Rules 和 Hooks 系统中的插件。

**[AI Dev OS](https://github.com/yunbow/ai-dev-os) 的一部分** — 将隐性知识转化为可执行的 AI 编码规则的框架（[Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)）。
需要在项目中设置 [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript)。

## 为什么选择这个插件？

将 AI Dev OS 指南集成到 **Kiro 的转向系统**：

- **11 Steering Rules** — `#ai-dev-os-check`、`#ai-dev-os-scan`、`#ai-dev-os-extract` 等
- **3 Auto Steering** — 哲学顾问、原则检查器、指南审计
- **2 File Match Rules** — 代码文件自动检查、L1-L2 依赖警告
- **一条命令安装** — `npx ai-dev-os init --rules typescript --plugin kiro`

![AI Dev OS Check & Fix Report](../../../docs/images/ai-dev-os-check.png)

## 快速开始

```bash
npx ai-dev-os init --rules typescript --plugin kiro
```

> CLI 会添加子模块、复制 AGENTS.md 模板，并将转向规则和钩子自动复制到 `.kiro/`。
> 详情请参阅 [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli)。

前提条件：[Kiro](https://kiro.dev/) >= 1.0.0 以及项目中已设置 AI Dev OS 层文件（L1-L3）（[TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）。

<details>
<summary>手动设置</summary>

**方法A：子模块**

```bash
# 1. 将 AI Dev OS rules 添加为子模块
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Python 项目：
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. 将此插件添加为子模块
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/ .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/ .kiro/hooks/
```

**方法B：直接复制**

```bash
# 1. 将规则添加为子模块（同上）
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. 克隆并复制插件文件
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
```

3. 在 Kiro 聊天中调用 `#ai-dev-os-init` 设置4层结构
4. 开始编码 — 转向规则和钩子会自动引导你

详情请参阅[操作指南](./operation-guide.md)。

</details>

## Steering Rules

### 手动转向（在聊天中用 `#name` 调用）

| 转向规则 | 调用 | 说明 |
|---------|------|------|
| **Init** | `#ai-dev-os-init` | 设置向导 — 30分钟内为项目引入 AI Dev OS |
| **Check** | `#ai-dev-os-check` | 检查代码变更的指南合规性（支持 `git diff`、暂存、分支比较） |
| **Scan** | `#ai-dev-os-scan` | 全项目所有源文件的完整合规扫描 |
| **Review** | `#ai-dev-os-review` | PR 前自审 — L3 合规 + L2 设计审查 + L1 一致性 |
| **Extract** | `#ai-dev-os-extract` | 从代码审查差异中提取新规则（Rule Harvesting） |
| **Why** | `#ai-dev-os-why` | 追溯规则原理 L3→L2→L1 |
| **Plan** | `#ai-dev-os-plan` | 编码前创建包含指南检查清单的实现计划 |
| **Ticket** | `#ai-dev-os-ticket` | 生成包含实现摘要和检查清单候选的工单（本地文件或 GitHub Issue） |
| **Audit** | `#ai-dev-os-audit` | 审计4层健康状态：依赖规则、新鲜度、覆盖率、一致性 |
| **Evolve** | `#ai-dev-os-evolve` | 分析最近提交，提议 L1-L2 更新（SECI 螺旋） |
| **Report** | `#ai-dev-os-report` | 为团队和利益相关者生成合规摘要报告 |

### 自动转向（自动激活）

| 转向规则 | 激活条件 | 说明 |
|---------|---------|------|
| `philosophy-advisor` | 架构/设计决策 | L1 哲学判断支持 |
| `principle-checker` | 代码变更讨论 | L2 原则一致性验证 |
| `guideline-auditor` | 指南维护讨论 | L3 覆盖率与一致性审计 |

### 文件匹配转向（匹配文件时自动激活）

| 转向规则 | 文件模式 | 说明 |
|---------|---------|------|
| `guideline-compliance` | `**/*.{ts,tsx,py,go,js,jsx}` | 代码文件的轻量级指南检查 |
| `layer-dependency` | `**/01_philosophy/**`, `**/02_decision-criteria/**` | 依赖规则违规警告 |

## Hooks

| 事件 | 触发条件 | 动作 |
|------|---------|------|
| File Save | 代码文件 | 指南合规快速检查 |
| Pre Tool Use (terminal: git commit) | 提交前 | 提醒运行 `#ai-dev-os-check` |
| User Prompt Submit | 实现相关提示 | 建议使用 `#ai-dev-os-plan` |

<details>
<summary>包结构</summary>

```
ai-dev-os-plugin-kiro/
├── steering/
│   ├── ai-dev-os-init.md              # 设置向导（手动）
│   ├── ai-dev-os-check.md             # 指南合规检查（手动）
│   ├── ai-dev-os-scan.md              # 全项目合规扫描（手动）
│   ├── ai-dev-os-review.md            # PR 前自审（手动）
│   ├── ai-dev-os-extract.md           # 代码 Rule Harvesting（手动）
│   ├── ai-dev-os-why.md               # 规则原理说明（手动）
│   ├── ai-dev-os-plan.md              # 指南感知的实现规划（自动）
│   ├── ai-dev-os-ticket.md            # 工单生成（手动）
│   ├── ai-dev-os-audit.md             # 4层健康审计（手动）
│   ├── ai-dev-os-evolve.md            # SECI 螺旋反馈（手动）
│   ├── ai-dev-os-report.md            # 合规报告生成（手动）
│   ├── philosophy-advisor.md          # L1 哲学判断支持（自动）
│   ├── principle-checker.md           # L2 原则一致性验证（自动）
│   ├── guideline-auditor.md           # L3 覆盖率与一致性审计（自动）
│   ├── guideline-compliance.md        # 代码文件自动检查（文件匹配）
│   └── layer-dependency.md            # 依赖规则警告（文件匹配）
├── hooks/
│   └── hooks.json                     # 生命周期事件钩子
├── checklist-templates/
│   ├── python.md                      # Python 专用检查清单
│   ├── go.md                          # Go 专用检查清单
│   └── nextjs.md                      # Next.js 专用检查清单
├── templates/
│   ├── AGENTS.md.template             # AGENTS.md 模板（含级联）
│   ├── ai-dev-os-starter/             # 最小配置模板
│   └── ai-dev-os-full/                # 完整4层模板
└── docs/
    └── operation-guide.md             # 详细操作指南
```

</details>

## Specificity Cascade

规则冲突时：framework-specific > common > project-specific > decision criteria > philosophy。[→ 详情](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## 相关项目

| 仓库 | 说明 |
|------|------|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | Framework specification and theory |
| [rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js guidelines |
| [rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI guidelines |
| [plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Skills, Hooks, and Agents for Claude Code |
| [plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor) | Cursor Rules (.mdc) |
| [cli](https://github.com/yunbow/ai-dev-os-cli) | `npx ai-dev-os init` |
| [benchmark](https://github.com/yunbow/ai-dev-os-benchmark) | Quantitative benchmark — guideline impact data |

## 许可证

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | [日本語](../ja/README.md) | 简体中文 | [한국어](../ko/README.md) | [Español](../es/README.md)
