# Source-Backed Notes Guide

作成日: 2026-04-14

## 目的

AI / 開発 / Obsidian / MCP の知識を、根拠つきで蓄積する。
LLMに問い合わせる時に、事実、推論、未確定を分けられる状態にする。

## 使う場面

- Web Clipperや手動メモで外部情報を保存する時。
- 公式docs、GitHub repo、個人ブログ、AI出力を混ぜずに保存したい時。
- `query-protocol` でLLMに読ませる根拠資料を作る時。

## カテゴリ追加の余地

現時点のsource classは最小構成。
必要になったら次を追加候補にする。

- `official-docs`
- `github-source`
- `blog-practice`
- `ai-output`
- `user-note`
- `experiment-result`

## 重複管理を避ける方針

このファイルは「根拠資料の保存形式」だけを扱う。
検索や問い合わせ形式は `query-protocol`、全体運用は `vault-operation` に任せる。

## Source Classes

| Class | 例 | 扱い |
|---|---|---|
| official | 公式docs、仕様、reference | 最優先の根拠 |
| primary | GitHub repo、release notes、issue、PR | 実装・運用の根拠 |
| secondary | blog、解説記事、動画 | 参考。公式で裏取りする |
| local | このPJのdocs、user prompt、decision | PJ内の現在地 |
| inference | LLMや人間の推論 | 事実と分ける |

## Note Structure

```markdown
---
title: ""
type: source
status: draft
topic: []
source:
  - ""
created: 2026-04-14
updated: 2026-04-14
confidence: medium
review_after:
tags: []
---

# Title

## Source Facts

- 

## Local Interpretation

- 

## Open Questions

- 

## Next Actions

- 
```

## Rules

1. 公式情報と推論を同じ箇条書きに混ぜない。
2. source URL を残す。
3. 日付に依存する情報は `review_after` を入れる。
4. 長文引用を避け、要約中心にする。
5. LLMが生成した要約は `Local Interpretation` へ置く。
