# AI Knowledge Taxonomy

作成日: 2026-04-14

## 目的

AI関連知識を、あとからLLMに問い合わせやすい形で分類する。

## 初期カテゴリ

| Category | 内容 |
|---|---|
| `models` | モデル仕様、強み、制限、価格や提供状況 |
| `agents` | Codex、Claude Code、Gemini CLI、multi-agent運用 |
| `prompting` | プロンプト設計、出力形式、制約 |
| `tools` | tool use、MCP、ブラウザ、検索、local shell |
| `rag` | 検索、埋め込み、知識参照、Obsidian連携 |
| `eval` | 回答評価、回帰テスト、品質確認 |
| `security` | prompt injection、secret管理、MCP権限 |
| `workflow` | AI会話保存、タスク分解、作業ステータス |

## Freshness Policy

AI情報は古くなりやすい。

- 公式docsがあるものは `source` に公式URLを入れる。
- model / API / tool の仕様は `review_after` を設定する。
- 「最新」「現行」「今おすすめ」は回答時に再調査する。
- LLMの推論は `confidence: medium` 以下にする。

## Query Example

```text
この vault を前提に、MCPについて今どう把握しているか整理してください。
公式仕様、このPJでの判断、未決、次アクションを分けてください。
```

