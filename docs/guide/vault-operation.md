# Vault Operation Guide

作成日: 2026-04-12
更新日: 2026-04-19

## 目的

`obsidian-set` は設計・検証・運用ルールの拠点。
本運用 vault は `G:\knowledge-vault`。

## 本運用 vault 方針

- 正本はローカル Markdown。
- `G:\knowledge-vault` は初期 GitHub repo 化しない。
- backup は `H:\bk\knowledge-vault-snapshots\` 配下の日付付き snapshot。
- `G:\devwork` 配下の各開発PJは、必要に応じて個別に GitHub repo 化する。

## 本運用 vault 構成

| Path | 役割 |
|---|---|
| `memory/` | LLM 用の想起・圧縮レイヤー |
| `knowledge/` | 人間向け整理済みナレッジ |
| `tasks/` | タスク単位の作業記録 |
| `sources/` | 根拠資料 |
| `prompts/` | ユーザプロンプト全文と AI 回答要約 |
| `inbox/` | 未整理情報の一時置き場 |
| `templates/` | note template |
| `attachments/` | 添付 |

## 重複管理

- 同じ事実セットの正本は1つ。
- `memory/` は正本ではなく、リンク・要約・想起用。
- `sources/` は根拠の正本。
- `tasks/` は実施履歴の正本。
- `knowledge/` は再利用知識の正本。
- `inbox/` は未整理であり正本ではない。

## P1 Query 方針

- Obsidian内一覧: Dataview。
- CLI / SQL検索: SQLite index。
- Markdown note が正本。Dataview結果と SQLite DB は派生物。

