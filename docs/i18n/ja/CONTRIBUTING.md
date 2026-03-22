# AI Dev OS Plugin — Kiro への貢献

貢献に興味を持っていただきありがとうございます！

## 貢献方法

### 問題の報告

- [GitHub Issues](https://github.com/yunbow/ai-dev-os-plugin-kiro/issues) をご利用ください
- 影響を受けるステアリングルール、フック、またはテンプレートを明記してください

### プルリクエスト

1. リポジトリをフォークする
2. フィーチャーブランチを作成する
3. 変更を加える
4. わかりやすいメッセージでコミットする
5. プルリクエストを開く

### 貢献できる内容

| ディレクトリ | 求めている貢献 | ガイドライン |
|-----------|-------------|------------|
| `steering/` | ステアリングルールの改善、新規ルール | ステアリングルールフォーマット（`inclusion`, `name`, `description` を含む YAML フロントマター）に従ってください。ルールは焦点を絞り簡潔にしてください。 |
| `hooks/` | フックの改善、新しいイベントハンドラー | Kiro フックフォーマット（`event`, `filePattern`, `actionType` を含む JSON 配列）に従ってください。徹底的にテストしてください。 |
| `templates/` | テンプレートの改善 | テンプレートは Two-Tier Context Strategy（10-15 個の重要なルールのみ）に従ってください。 |
| `checklist-templates/` | 新しい言語のチェックリスト、改善 | チェックリストは実行可能かつ検証可能なものにしてください。 |

### ステアリングルール開発ガイドライン

- 各ステアリングルールは `steering/{name}.md` に配置します
- 必須フロントマター: `inclusion`（例: `always`, `manual`）, `name`, `description`
- ルールの内容は明確で実行可能なものにしてください
- ルールは単一の関心事に焦点を当ててください
- 可能な限り具体的な例を使用してください

### フック開発ガイドライン

- フックは `hooks/hooks.json` で定義されています
- 各フックは `event`, `filePattern`, `actionType` を含む JSON オブジェクトです
- ソースファイル以外（node_modules, dist, 画像など）をフィルタリングしてください
- TypeScript と Python の両方のプロジェクトでテストしてください

### クロスプラグイン機能の同等性

このプラグインに新機能を追加する際は、以下への同等機能の追加も検討してください：

- [ai-dev-os-plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code)（スキルまたはフックとして）
- [ai-dev-os-plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor)（.mdc ルールとして）

### 翻訳ガイド

- 翻訳は `docs/i18n/{lang}/` にあります
- 現在サポートされている言語: `ja`, `zh-CN`, `ko`, `es`

## 行動規範

敬意を持ち、建設的で、包括的であること。

---

Languages: [English](../../../CONTRIBUTING.md) | 日本語
