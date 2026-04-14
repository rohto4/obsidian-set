# Vault Operation Guide

作成日: 2026-04-12

## 目的

`obsidian-set` は、Obsidian でも VS Code でも扱える Markdown knowledge base として運用する。
最初から複雑な分類を作らず、Git 管理しやすい小さなルールから始める。

## 使う場面

- 新しい情報をどこに保存するか迷った時。
- `docs/` と将来の `knowledge/` の役割が混ざりそうな時。
- AI agent が作業中にどのファイルへ書くべきか判断する時。
- 週次レビューで一時メモを恒久noteへ昇格する時。

## 重複管理を避ける方針

`vault-operation` はメタルールだけを書く。
個別カテゴリの説明、検索方法、source noteの形式は別ファイルに置き、ここには重複させない。

同期してアップデートすべき同じ内容を複数ファイルに置かない。
迷った場合は、より具体的なファイルを正本にし、このファイルからは参照だけにする。

## 基本方針

1. 正本は Markdown file と Git history。
2. Obsidian は閲覧、リンク、検索、将来のモバイル同期のために使う。
3. VS Code は普段の編集、AI agent 操作、Git 操作の主入口にする。
4. LLM が読む情報は、根拠、推論、判断待ちを分ける。
5. 生ログをそのまま貯めず、要約と決定事項を貯める。

## Directory Roles

| Path | 役割 |
|---|---|
| `AGENTS.md` | 全 agent / tool 共通の最上位ルール |
| `PROJECT.md` | PJ 固有の目的、優先度、情報配置 |
| `docs/guide/` | 恒久的な運用ガイド、判断基準 |
| `docs/spec/` | 実装対象として確定した仕様、要件、設計前提 |
| `docs/condi-ref/` | 条件付き参考資料、実現可能性確認、候補比較 |
| `docs/imp/` | 作業計画、進捗、判断待ち、作業ログ |
| `.agents/skills/` | ECC 由来の作業別 workflow |

## Note Types

初期 note type は増やしすぎない。

- `guide`: 継続的に守る運用ルール
- `spec`: 技術選定、設計、設定方針
- `imp`: 作業中の実装・検証メモ
- `source`: 参照情報の要約
- `decision`: 判断済みの決定
- `wait`: ユーザ判断待ち

## Naming

- Markdown file は lowercase-kebab-case を基本にする。
- 日本語タイトルは本文の `title` に書く。
- ファイル名は短く、検索しやすくする。
- 日付が主役の作業ログだけ `YYYY-MM-DD-*` を許可する。

## Writing Rules

1. 1ファイル1目的にする。
2. 公式情報と推論を混ぜない。
3. 古くなりやすい情報には `review_after` を付ける。
4. API key、token、private URL、個人情報は書かない。
5. AI会話は全文保存せず、決定、根拠、未決、次アクションへ圧縮する。

## Initial Workflow

1. 調査する。
2. `docs/imp/imp-plan.md` に作業案を追加する。
3. 判断が必要なものは `docs/imp/imp-wait.md` に移す。
4. 判断不要な運用ルールは `docs/guide/` に、条件付き参考資料は `docs/condi-ref/` にドラフトを書く。
5. 実装対象として確定した仕様だけ `docs/spec/` に移す。
6. Git commit 前に `git status --short --branch` と `git diff --stat` を確認する。

## Query Workflow

「このカテゴリを今どう把握しているか」と聞く場合:

1. `PROJECT.md` を読む。
2. 関連する `docs/guide/` と `docs/spec/` を読む。
3. 関連する `docs/condi-ref/` を読む。
4. `docs/imp/imp-wait.md` を見て未決を確認する。
5. 回答を `sourced fact`, `inference`, `recommendation`, `open questions` に分ける。
