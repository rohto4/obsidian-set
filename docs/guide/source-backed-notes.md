# Source-Backed Notes Guide

作成日: 2026-04-14
更新日: 2026-04-19

## 目的

根拠資料を `G:\knowledge-vault\sources\` に保存する。
LLM回答時に、事実、解釈、未確定を分けられる状態にする。

## 保存先

```text
G:\knowledge-vault\sources\
```

Web Clipper は現時点では見送り。
手動保存または後段導入時も保存先は `sources/` に寄せる。

## Source Classes

- `official`: 公式docs、仕様、reference
- `primary`: GitHub repo、release notes、issue、PR
- `secondary`: blog、解説記事、動画
- `local`: このPJやvault内docs
- `experiment-result`: 実験結果
- `inference`: LLMや人間の推論

## ルール

- source facts と local interpretation を分ける。
- URL、取得日、review_after を残す。
- 長文引用を避け、要約中心。
- LLM推論を事実として扱わない。
- Dataview / SQLite で拾えるよう frontmatter を維持する。

## Template

正本:

```text
G:\knowledge-vault\templates\source-note.md
```

