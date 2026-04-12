# Note Frontmatter Specification

作成日: 2026-04-12

## 目的

Obsidian、VS Code、Git、LLM、将来の MCP 連携で扱いやすい note metadata を定義する。

## Minimal Schema

```yaml
---
title: ""
type: guide
status: draft
topic: []
source: []
created: 2026-04-12
updated: 2026-04-12
confidence: medium
review_after:
tags: []
---
```

## Field Rules

| Field | Required | 値 |
|---|---|---|
| `title` | yes | 人間向けタイトル |
| `type` | yes | `guide`, `spec`, `imp`, `source`, `decision`, `wait` |
| `status` | yes | `draft`, `active`, `decided`, `deprecated` |
| `topic` | yes | `dev`, `ai`, `obsidian`, `mcp`, `git`, `vscode`, `ops` など |
| `source` | no | URL、repo path、issue など |
| `created` | yes | `YYYY-MM-DD` |
| `updated` | yes | `YYYY-MM-DD` |
| `confidence` | yes | `low`, `medium`, `high` |
| `review_after` | no | 再確認が必要な日付 |
| `tags` | no | Obsidian / search 用タグ |

## Defaults

- 新規 guide: `type: guide`, `status: draft`, `confidence: medium`
- 新規 spec: `type: spec`, `status: draft`, `confidence: medium`
- 判断済み: `status: decided`, `confidence: high`
- 最新情報に依存: `confidence: medium`, `review_after` を設定

## Example

```markdown
---
title: "Obsidian Sync Strategy"
type: spec
status: draft
topic: [obsidian, sync, git]
source:
  - https://help.obsidian.md/sync
created: 2026-04-12
updated: 2026-04-12
confidence: medium
review_after: 2026-05-12
tags: [obsidian, sync]
---

# Obsidian Sync Strategy

...
```

## LLM Handling

LLM は frontmatter を次のように扱う。

- `status: decided` は現時点の決定として扱う。
- `status: draft` は提案または作業中として扱う。
- `confidence: low` は回答時に不確実性を明示する。
- `review_after` を過ぎている場合は、最新情報の再確認を提案する。

