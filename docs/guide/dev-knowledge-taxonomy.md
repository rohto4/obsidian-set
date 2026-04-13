# Development Knowledge Taxonomy

作成日: 2026-04-14

## 目的

開発ノウハウを蓄積するための分類候補を定義する。

## 初期カテゴリ

| Category | 内容 |
|---|---|
| `git` | commit、branch、merge、conflict、GitHub運用 |
| `vscode` | VS Code拡張、workspace設定、ショートカット |
| `windows` | PowerShell、PATH、権限、Windows固有問題 |
| `testing` | テスト設計、検証手順、失敗時の切り分け |
| `debugging` | エラー解析、ログ、再現手順 |
| `docs` | Markdown、Obsidian、仕様書、運用メモ |
| `mcp` | MCP server、client設定、権限、security |
| `ai-coding` | Codex、Claude Code、Gemini CLI の使い分け |

## Note Type Mapping

- 具体的な手順: `type: guide`
- 技術選定: `type: spec`
- 作業ログ: `type: imp`
- 参照元まとめ: `type: source`
- 決定事項: `type: decision`

## 初期運用

最初は top-level directory を増やさず、frontmatter の `topic` で分類する。
Obsidian側の保存体系が決まったら `knowledge/dev/` などへ移す。

