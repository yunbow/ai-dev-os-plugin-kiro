# AI Dev OS Plugin — Kiro

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](../../../LICENSE)

AI Dev OS の4層モデルを Kiro の Steering Rules と Hooks システムに統合するプラグインです。

**[AI Dev OS](https://github.com/yunbow/ai-dev-os) の一部** — 暗黙知を強制力のある AI コーディングルールに変換するフレームワーク（[Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)）。
プロジェクトに [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) のセットアップが必要です。

## なぜこのプラグインか？

AI Dev OS ガイドラインを **Kiro のステアリングシステム** に統合：

- **11 Steering Rules** — `#ai-dev-os-check`、`#ai-dev-os-scan`、`#ai-dev-os-extract` など
- **3 Auto Steering** — 哲学アドバイザー、原則チェッカー、ガイドライン監査
- **2 File Match Rules** — コードファイルの自動チェック、L1-L2 依存性警告
- **ワンコマンドセットアップ** — `npx ai-dev-os init --rules typescript --plugin kiro`

## クイックスタート

```bash
npx ai-dev-os init --rules typescript --plugin kiro
# ステアリングルールとフックを Kiro のディレクトリにコピー:
cp -r .ai-dev-os/plugin/steering/ .kiro/steering/
cp -r .ai-dev-os/plugin/hooks/ .kiro/hooks/
```

> CLI はサブモジュールの追加と AGENTS.md テンプレートのコピーを行います。ステアリングルールとフックは別途 Kiro のディレクトリにコピーする必要があります。
> 詳細は [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli) を参照してください。

前提条件: [Kiro](https://kiro.dev/) >= 1.0.0 およびプロジェクトに AI Dev OS レイヤーファイル（L1-L3）（[TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）。

<details>
<summary>手動セットアップ</summary>

**方法A: サブモジュール**

```bash
# 1. AI Dev OS rules をサブモジュールとして追加
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Python プロジェクトの場合:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. このプラグインをサブモジュールとして追加
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/ .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/ .kiro/hooks/
```

**方法B: 直接コピー**

```bash
# 1. ルールをサブモジュールとして追加（上記と同じ）
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. プラグインをクローンしてコピー
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
```

3. Kiro チャットで `#ai-dev-os-init` を呼び出して4層構造をセットアップ
4. コーディング開始 — ステアリングルールとフックが自動的にガイドします

詳細は[運用手順書](./operation-guide.md)を参照してください。

</details>

## Steering Rules

### 手動ステアリング（チャットで `#name` で呼び出し）

| ステアリングルール | 呼び出し | 説明 |
|-------------------|---------|------|
| **Init** | `#ai-dev-os-init` | セットアップウィザード — 30分でプロジェクトに AI Dev OS を導入 |
| **Check** | `#ai-dev-os-check` | コード変更のガイドライン準拠チェック（`git diff`、ステージング、ブランチ比較に対応） |
| **Scan** | `#ai-dev-os-scan` | プロジェクト全ソースファイルの完全な準拠スキャン |
| **Review** | `#ai-dev-os-review` | PR前セルフレビュー — L3 準拠 + L2 設計レビュー + L1 整合性を統合チェック |
| **Extract** | `#ai-dev-os-extract` | コードレビューの差分から新ルールを抽出（Rule Harvesting） |
| **Why** | `#ai-dev-os-why` | ルールの根拠を L3→L2→L1 まで遡って説明 |
| **Plan** | `#ai-dev-os-plan` | 実装前にガイドラインチェックリスト付きの実装計画を作成 |
| **Ticket** | `#ai-dev-os-ticket` | 実装サマリーとチェックリスト候補付きチケットを生成（ローカルファイルまたは GitHub Issue） |
| **Audit** | `#ai-dev-os-audit` | 4層の健全性を監査：依存性ルール、鮮度、網羅性、一貫性 |
| **Evolve** | `#ai-dev-os-evolve` | 直近のコミットを分析し、L1-L2 の更新を提案（SECI スパイラル） |
| **Report** | `#ai-dev-os-report` | チーム・ステークホルダー向けの準拠サマリーレポートを生成 |

### 自動ステアリング（自動的にアクティブ化）

| ステアリングルール | アクティブ化条件 | 説明 |
|-------------------|----------------|------|
| `philosophy-advisor` | アーキテクチャ/設計の議論 | L1 に基づく判断支援 |
| `principle-checker` | コード変更の議論 | L2 準拠の検証 |
| `guideline-auditor` | ガイドラインメンテナンスの議論 | L3 の網羅性・一貫性監査 |

### ファイルマッチステアリング（マッチするファイルで自動アクティブ化）

| ステアリングルール | ファイルパターン | 説明 |
|-------------------|----------------|------|
| `guideline-compliance` | `**/*.{ts,tsx,py,go,js,jsx}` | コードファイルの軽量ガイドラインチェック |
| `layer-dependency` | `**/01_philosophy/**`, `**/02_decision-criteria/**` | 依存性ルール違反の警告 |

## Hooks

| イベント | トリガー | アクション |
|---------|---------|-----------|
| File Save | コードファイル | ガイドライン準拠の簡易チェック |
| Pre Tool Use (terminal: git commit) | コミット前 | `#ai-dev-os-check` 実行のリマインド |
| User Prompt Submit | 実装関連のプロンプト | `#ai-dev-os-plan` の提案 |

<details>
<summary>パッケージ構成</summary>

```
ai-dev-os-plugin-kiro/
├── steering/
│   ├── ai-dev-os-init.md              # セットアップウィザード（手動）
│   ├── ai-dev-os-check.md             # ガイドライン準拠チェック（手動）
│   ├── ai-dev-os-scan.md              # プロジェクト全体準拠スキャン（手動）
│   ├── ai-dev-os-review.md            # PR前セルフレビュー（手動）
│   ├── ai-dev-os-extract.md           # コードからの Rule Harvesting（手動）
│   ├── ai-dev-os-why.md               # ルールの根拠説明（手動）
│   ├── ai-dev-os-plan.md              # ガイドライン準拠の実装計画（自動）
│   ├── ai-dev-os-ticket.md            # チケット生成（手動）
│   ├── ai-dev-os-audit.md             # 4層健全性監査（手動）
│   ├── ai-dev-os-evolve.md            # SECI スパイラルフィードバック（手動）
│   ├── ai-dev-os-report.md            # 準拠レポート生成（手動）
│   ├── philosophy-advisor.md          # L1 哲学に基づく判断支援（自動）
│   ├── principle-checker.md           # L2 原則の整合性検証（自動）
│   ├── guideline-auditor.md           # L3 ガイドラインの網羅性・一貫性監査（自動）
│   ├── guideline-compliance.md        # コードファイルの自動チェック（ファイルマッチ）
│   └── layer-dependency.md            # 依存性ルール警告（ファイルマッチ）
├── hooks/
│   └── hooks.json                     # ライフサイクルイベントフック
├── checklist-templates/
│   ├── python.md                      # Python 固有チェックリスト
│   ├── go.md                          # Go 固有チェックリスト
│   └── nextjs.md                      # Next.js 固有チェックリスト
├── templates/
│   ├── AGENTS.md.template             # AGENTS.md テンプレート（カスケード付き）
│   ├── ai-dev-os-starter/             # 最小構成テンプレート
│   └── ai-dev-os-full/                # フル4層テンプレート
└── docs/
    └── operation-guide.md             # 詳細な運用手順
```

</details>

## Specificity Cascade

ルールが競合した場合: framework-specific > common > project-specific > decision criteria > philosophy。[→ 詳細](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## 関連リポジトリ

| リポジトリ | 説明 |
|---|---|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | フレームワーク仕様と理論 |
| [ai-dev-os-rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js ガイドライン |
| [ai-dev-os-rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI ガイドライン |
| [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Claude Code 向け Skills, Hooks, Agents |
| [ai-dev-os-plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor) | Cursor Rules (.mdc) |
| [ai-dev-os-cli](https://github.com/yunbow/ai-dev-os-cli) | セットアップ自動化 — `npx ai-dev-os init` |

## ライセンス

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | 日本語 | [简体中文](../zh-CN/README.md) | [한국어](../ko/README.md) | [Español](../es/README.md)
