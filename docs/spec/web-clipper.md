# Obsidian Web Clipper Evaluation

作成日: 2026-04-14

## 何がうれしいツールか

Obsidian Web Clipper は、WebページをObsidian vaultへ保存するための公式ブラウザ拡張。
開発ノウハウやAI情報を蓄積する場合、次がうれしい。

- ページURL、タイトル、本文、選択箇所をnote化しやすい。
- templateで保存形式を揃えられる。
- highlightや引用元を残しやすい。
- 読んだWeb情報を「あとでLLMに聞ける材料」に変換できる。
- AI / 開発情報の一次資料リンクを保存しやすい。

## このPJでの使いどころ

- 公式 docs の更新を保存する。
- AI / MCP / Obsidian / Git 関連の記事を `source` note として保存する。
- 長いページを丸ごと保存せず、要点と参照URLを残す。
- LLMに聞く前の材料として、source-backed note を作る。

## 注意点

- Webページ全文の大量保存は著作権と検索ノイズの問題がある。
- クリップした内容は後から古くなる。
- 公式情報、個人ブログ、AI生成記事を同じ信頼度で扱わない。
- 保存先とfrontmatterを決めてから使う。

## 初期テンプレート案

```markdown
---
title: "{{title}}"
type: source
status: draft
topic: []
source:
  - "{{url}}"
created: "{{date}}"
updated: "{{date}}"
confidence: medium
review_after:
tags: [web-clip]
---

# {{title}}

## Summary

- 

## Useful Points

- 

## Quote / Evidence

> 

## Source

- {{url}}
```

## 初期判断

今すぐ必須ではない。
ただし、AI / 開発情報のWeb収集を本格化するなら有用。

導入前に決めること:

1. 保存先 directory。
2. frontmatter。
3. 引用量ルール。
4. 公式情報と二次情報の分類。

## References

- https://help.obsidian.md/web-clipper

