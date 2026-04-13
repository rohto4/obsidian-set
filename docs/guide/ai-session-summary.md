# AI Session Summary Guide

作成日: 2026-04-14

## 目的

Codex / Claude Code / Gemini CLI とのやり取りを、後から分析しやすい形で保存する。

## ユーザ方針

- ユーザのプロンプトは全文保存する。
- AIの出力は要約保存する。
- AIがどういうプロセスで回答したかが分析できる程度の手がかりを残す。

## 保存方針

保存する:

- ユーザプロンプト全文
- AI出力の要約
- 実行した主な操作
- 参照した主なファイル
- 参照した主なURL
- 判断待ち
- 次アクション

保存しない:

- API key、token、private credential
- 長いAI出力全文
- 推論の内部ログ
- 著作権上そのまま保持すべきでない長文引用

## Template

~~~markdown
---
title: ""
type: source
status: draft
topic: [ai-session]
source: []
created: 2026-04-14
updated: 2026-04-14
confidence: medium
review_after:
tags: [ai-session]
---

# AI Session Summary

## User Prompt

```text

```

## AI Output Summary

- 

## Process Summary

- 読んだファイル:
- 調査したURL:
- 作成・更新したファイル:
- 実行したコマンド:

## Decisions

- 

## Waiting

- 

## Next Actions

- 
~~~

## 注意

「プロセス」は、再現や分析に必要な外形情報だけを残す。
LLMの内部推論を保存する運用にはしない。
