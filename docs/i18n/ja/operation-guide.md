# AI Dev OS Plugin — Kiro — 運用手順書

## 目次

1. [前提条件](#1-前提条件)
2. [インストール](#2-インストール)
3. [初期セットアップ](#3-初期セットアップ)
4. [日常ワークフロー](#4-日常ワークフロー)
5. [定期メンテナンス](#5-定期メンテナンス)
6. [チームオンボーディング](#6-チームオンボーディング)
7. [言語ポリシー](#7-言語ポリシー)
8. [トラブルシューティング](#8-トラブルシューティング)

---

## 1. 前提条件

- [Kiro](https://kiro.dev/) >= 1.0.0
- プロジェクトに AI Dev OS のレイヤーファイル（L1-L3）がセットアップ済みであること（テンプレート: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)）

---

## 2. インストール

### 方法A: ステアリングルールのコピー（推奨）

ステアリングルールとフックをプロジェクトの `.kiro/` ディレクトリにコピーします:

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
cp -r ai-dev-os-plugin-kiro/checklist-templates/ .kiro/checklist-templates/
```

### 方法B: Git Submodule

AI Dev OS の更新をプロジェクトと分離して管理できます:

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
```

その後、ステアリングルールをコピーまたはシンボリックリンクします:

```bash
cp -r .kiro/plugins/ai-dev-os/steering/* .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/* .kiro/hooks/
```

### フックの設定

Kiro フックは Hook UI からも設定できます:

1. コマンドパレットを開く（`Ctrl+Shift+P` / `Cmd+Shift+P`）
2. "Kiro: Open Kiro Hook UI" と入力
3. `hooks/hooks.json` の設定に合わせてフックを作成

---

## 3. 初期セットアップ

### セットアップウィザードの実行

Kiro チャットで呼び出します:

```text
#ai-dev-os-init [tech-stack]
```

例:

```text
#ai-dev-os-init nextjs
```

ウィザードの動作:

1. 技術スタック、プロジェクト規模、既存ルールファイルをヒアリング
2. 既存ルールの検出と取り込み（`.cursorrules`, `AGENTS.md`, `.eslintrc`）
3. 4層ディレクトリ構造の生成
4. ガイドライン参照と優先度カスケードを含む `AGENTS.md` の作成
5. Kiro基盤ファイル（product.md, tech.md, structure.md）の設定（オプション）

### セットアップの確認

初期化後、以下の構造を確認します:

```text
ai-dev-os/
├── 01_philosophy/
├── 02_decision-criteria/
├── 03_guidelines/
│   ├── common/
│   └── frameworks/
└── 04_ai-frames/
```

---

## 4. 日常ワークフロー

### 4.1 実装前の計画

重要な変更の前に、ガイドライン準拠の計画を作成します。`ai-dev-os-plan` ステアリングルールは `inclusion: auto` なので、実装タスクを議論すると Kiro が自動的に提案します。明示的に呼び出すこともできます:

```text
#ai-dev-os-plan JWT認証機能を追加
```

実行内容:

1. リクエストを分析し、影響を受けるファイルを特定
2. ファイルと関連する AI Dev OS ガイドラインをマッピング
3. 適用可能なルールのチェックリストを生成
4. コードを書く前にプランを提示して承認を得る

### 4.2 実装せずにチケットを作成する

実装を後回しにしたい場合（チームへのアサインやバックログ管理など）、チケットを作成します:

```text
#ai-dev-os-ticket JWT認証機能を追加
```

実行内容:

1. `#ai-dev-os-plan` と同じ分析を実行
2. チケットの出力先を確認（AGENTS.md に設定がない場合）:
   - **ローカルファイル**: 指定ディレクトリに `TICKET-001-add-user-auth.md` として保存
   - **GitHub Issue**: `gh issue create` で Issue を作成
3. プレビューを表示して承認を得る
4. チケットを作成 — **コードは書かない**

チケットの出力先を事前設定するには、プロジェクトの `AGENTS.md` に追加します:

```markdown
## Ticket Settings
- output: file
- path: docs/tickets/phase1
```

### 4.3 コーディング

通常通りコードを書きます。ステアリングルールとフックが自動的に:

- コードファイル保存時にガイドライン準拠をチェック（`guideline-compliance` ファイルマッチステアリング）
- L1-L2ファイル編集時に依存性ルール違反を警告（`layer-dependency` ファイルマッチステアリング）
- コミット前に準拠チェックの実行をリマインド

### 4.4 コミット前

準拠チェックを実行します:

```text
#ai-dev-os-check
```

### 4.5 コードレビュー後

AIが生成したコードをレビューで修正した場合、新ルールを抽出します:

```text
#ai-dev-os-extract [file-path]
```

### 4.6 ルールの理解

チームメンバーがルールに疑問を持った時:

```text
#ai-dev-os-why "なぜany型が禁止なの？"
```

---

## 5. 定期メンテナンス

### 月次: 健全性監査

```text
#ai-dev-os-audit
```

### 四半期: SECI螺旋進化

```text
#ai-dev-os-evolve
```

### 週次/月次: 準拠レポート

```text
#ai-dev-os-report 1w
#ai-dev-os-report 1m
```

---

## 6. チームオンボーディング

### 新メンバー向け

1. `ai-dev-os/01_philosophy/core-values.md` を読む（5分）
2. `ai-dev-os/02_decision-criteria/` をざっと確認（10分）
3. 不明なルールには `#ai-dev-os-why` を呼び出し
4. コーディング開始 — ステアリングルールとフックが自動的にガイド

### AI Dev OS を導入するチーム向け

1. プロジェクトで `#ai-dev-os-init` を呼び出し
2. **starter** テンプレート（L3のみ）から開始
3. コードレビューのたびに `#ai-dev-os-extract` を使用
4. 2-4週間後に `#ai-dev-os-audit` でギャップを特定
5. `#ai-dev-os-evolve` で L1-L2 を段階的に構築

---

## 7. 言語ポリシー

ソースファイル（steering rules, hooks, templates）はすべて**英語**で管理します。これはLLMの精度を最大化し、幅広いユーザーがアクセスできるようにするためです。翻訳ドキュメントは `docs/i18n/` に参考として提供しますが、英語が唯一の正（Single Source of Truth）です。

---

## 8. トラブルシューティング

### ステアリングルールがアクティブにならない

- ステアリングファイルが `.kiro/steering/` ディレクトリにあるか確認
- YAML frontmatter が有効か確認（正しい `inclusion` モード、適切な `fileMatchPattern`）
- 手動ステアリングはチャットで `#name` で呼び出し
- 自動ステアリングは `description` フィールドが会話のコンテキストに合致していることを確認

### フックが発火しない

- フックが `.kiro/hooks/` ディレクトリに設定されているか確認
- または Kiro Hook UI で設定（`Ctrl+Shift+P` → "Kiro: Open Kiro Hook UI"）
- コマンドタイプのフックでは `jq` がインストールされているか確認
- Windows の場合、bash が PATH に含まれているか確認

### 偽陽性の違反

- チェックが厳しすぎる場合、`03_guidelines/` の該当ガイドラインを編集
- 削除前に `#ai-dev-os-why` でルールの根拠を確認
- 削除ではなく緩和を検討

### パフォーマンス

- ファイルマッチステアリングは対象ファイルがコンテキストにある時に実行 — パターンを具体的に
- 重い操作は自動ではなく手動でステアリングルールを呼び出し
- 大きなガイドラインファイルは小さく分割を検討

### Kiro Specs と AI Dev OS の連携

Kiro のスペック駆動開発（要件 → 設計 → タスク）は AI Dev OS を補完します:

- Kiro Specs で機能計画とタスク分解
- AI Dev OS ガイドラインはスペックタスク実行時の品質ゲートとして機能
- `Pre Spec Task` / `Post Spec Task` フックイベントでガイドラインチェックをトリガー可能

---

Languages: [English](../../operation-guide.md) | 日本語 | [简体中文](../zh-CN/operation-guide.md) | [한국어](../ko/operation-guide.md) | [Español](../es/operation-guide.md)
