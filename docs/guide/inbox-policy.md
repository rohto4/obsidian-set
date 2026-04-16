# Inbox Policy

作成日: 2026-04-16

## 目的

`inbox` は、まだ分類先や正本化の判断が決まっていない情報を一時的に受け止める入口。
最初から正しい場所へ分類しようとして保存が止まることを防ぐ。

## 使う場面

- Web記事、公式docs、GitHub issue、blog などをあとで読みたい時。
- AI会話から、残す価値がありそうな論点だけ一時保存したい時。
- 開発ノウハウやAI知識を見つけたが、`guide` / `spec` / `source` のどれにするか未定の時。
- 思いつき、疑問、比較候補、未整理メモをまず失わないようにしたい時。

## 基本方針

1. `inbox` は恒久保存場所ではない。
2. `inbox` の情報は未整理・未検証として扱う。
3. 公式情報、推論、自分の判断を混ぜたまま正本化しない。
4. 週次またはまとまった作業単位で見直し、昇格・保留・破棄を決める。
5. vault のゴミ箱ではない。不要と判断した候補は `docs/Z_trash/` に移す。

## 初期配置案

実フォルダ作成は別判断にする。
採用する場合の候補は次。

```text
knowledge/
  inbox/
```

`docs/` 配下の作業メモとは役割を分ける。

- `docs/imp/`: この PJ の作業計画、判断待ち、進捗。
- `knowledge/inbox/`: Obsidian vault 側の未整理知識。

## Inbox Note Structure

```markdown
---
title: ""
type: inbox
status: draft
topic: []
source:
  - ""
created: 2026-04-16
updated: 2026-04-16
confidence: low
review_after:
tags: [inbox]
---

# Title

## Raw Note

- 

## Why Keep

- 

## Possible Destination

- 

## Next Action

- 
```

## 昇格先

| 条件 | 移動先 |
|---|---|
| 外部情報の要約と根拠として残す | `source` note |
| 継続的に守る運用ルールになった | `docs/guide/` |
| 実装対象の確定仕様になった | `docs/spec/` |
| まだ採用未確定の比較・候補 | `docs/condi-ref/` |
| この PJ の作業計画や判断待ち | `docs/imp/` |
| 使わないと判断した候補 | `docs/Z_trash/` |

## 処理ルール

1. `inbox` に入れた時点では、正しさを保証しない。
2. `source` がある場合は URL を必ず残す。
3. 自分の解釈は `Raw Note` と分けて書く。
4. 1 note に複数テーマが混ざったら、レビュー時に分割する。
5. 30日以上残るものは、昇格・保留理由・破棄のどれかを決める。

## LLM への扱わせ方

LLM に `inbox` を読ませる場合は、次を明示する。

- `inbox` は未整理情報であり、正本ではない。
- 回答の根拠に使う場合は、必ず `source` と `confidence` を確認する。
- `docs/guide/`、`docs/spec/`、source-backed note と矛盾する場合は、正本側を優先する。

## 関連

- `docs/guide/vault-operation.md`
- `docs/guide/source-backed-notes.md`
- `docs/spec/note-frontmatter.md`
- `docs/condi-ref/practical-obsidian-workflows.md`
