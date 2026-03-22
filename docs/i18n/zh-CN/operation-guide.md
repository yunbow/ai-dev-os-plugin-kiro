# AI Dev OS Plugin — Kiro — 操作指南

## 目录

1. [前提条件](#1-前提条件)
2. [安装](#2-安装)
3. [初始设置](#3-初始设置)
4. [日常工作流](#4-日常工作流)
5. [定期维护](#5-定期维护)
6. [团队引导](#6-团队引导)
7. [语言策略](#7-语言策略)
8. [故障排除](#8-故障排除)

---

## 1. 前提条件

- [Kiro](https://kiro.dev/) >= 1.0.0
- 项目中已设置 AI Dev OS 层文件（L1-L3）（模板：[TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）

---

## 2. 安装

### 方式A：复制转向规则（推荐）

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
cp -r ai-dev-os-plugin-kiro/checklist-templates/ .kiro/checklist-templates/
```

### 方式B：Git Submodule

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/* .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/* .kiro/hooks/
```

### 钩子设置

Kiro 钩子也可以通过 Hook UI 配置：

1. 打开命令面板（`Ctrl+Shift+P` / `Cmd+Shift+P`）
2. 输入 "Kiro: Open Kiro Hook UI"
3. 根据 `hooks/hooks.json` 的配置创建钩子

---

## 3. 初始设置

在 Kiro 聊天中调用：

```text
#ai-dev-os-init [tech-stack]
```

示例：

```text
#ai-dev-os-init nextjs
```

---

## 4. 日常工作流

### 4.1 实现前规划

```text
#ai-dev-os-plan 添加JWT用户认证
```

### 4.2 创建工单而非直接实现

```text
#ai-dev-os-ticket 添加JWT用户认证
```

### 4.3 编写代码

照常编写代码。转向规则和钩子会自动引导。

### 4.4 提交前

```text
#ai-dev-os-check
```

### 4.5 代码审查后

```text
#ai-dev-os-extract [file-path]
```

### 4.6 理解规则

```text
#ai-dev-os-why "为什么禁止使用 any 类型？"
```

---

## 5. 定期维护

### 每月：健康审计

```text
#ai-dev-os-audit
```

### 每季度：SECI 螺旋进化

```text
#ai-dev-os-evolve
```

### 每周/每月：合规报告

```text
#ai-dev-os-report 1w
#ai-dev-os-report 1m
```

---

## 6. 团队引导

### 新成员入门

1. 阅读 `ai-dev-os/01_philosophy/core-values.md`（5分钟）
2. 浏览 `ai-dev-os/02_decision-criteria/`（10分钟）
3. 对不清楚的规则调用 `#ai-dev-os-why`
4. 开始编码——转向规则和钩子会自动引导

### 团队采用 AI Dev OS

1. 在项目上调用 `#ai-dev-os-init`
2. 从 **starter** 模板（仅 L3）开始
3. 每次代码审查后使用 `#ai-dev-os-extract`
4. 2-4周后调用 `#ai-dev-os-audit` 识别差距
5. 通过 `#ai-dev-os-evolve` 逐步构建 L1-L2

---

## 7. 语言策略

所有源文件（steering rules、hooks、templates）均以**英文**维护。翻译文档在 `docs/i18n/` 下作为参考。

---

## 8. 故障排除

### 转向规则未激活

- 确认转向文件在 `.kiro/steering/` 目录中
- 检查 YAML frontmatter 是否有效
- 手动转向通过 `#name` 在聊天中调用
- 自动转向确保 `description` 字段与对话上下文匹配

### 钩子未触发

- 确认钩子在 `.kiro/hooks/` 目录中
- 或通过 Kiro Hook UI 配置（`Ctrl+Shift+P` → "Kiro: Open Kiro Hook UI"）
- 检查 `jq` 是否已安装

### Kiro Specs 与 AI Dev OS 配合

Kiro 的规格驱动开发（需求 → 设计 → 任务）补充 AI Dev OS：

- 用 Kiro Specs 进行功能规划和任务分解
- AI Dev OS 指南作为规格任务执行时的质量门控

---

Languages: [English](../../operation-guide.md) | [日本語](../ja/operation-guide.md) | 简体中文 | [한국어](../ko/operation-guide.md) | [Español](../es/operation-guide.md)
