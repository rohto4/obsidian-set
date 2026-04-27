# Task A: Vault Structure and Implementation Priority

作成日: 2026-04-17
更新日: 2026-04-18

## 目的

本運用 knowledge vault の最終構成と初期導入順を決める。

この文書は `obsidian-set` 自体を本運用 vault にするためではなく、`G:\knowledge-vault` を横断ナレッジ + LLM 長期記憶の本運用 vault として使うための作業メモ。

## 現在の結論

旧案の `knowledge/index` 中心構成は採用しない。

新方針:

```text
G:\knowledge-vault\
  AGENTS.md
  PROJECT.md
  README.md
  memory/
    l1-triggers.md
    l2-models/
    l3-summaries/
    l4-records/
  knowledge/
    dev/
    ai/
    decisions/
  tasks/
    active/
    done/
    handoff/
  sources/
  prompts/
  inbox/
  templates/
  attachments/
```

## 前提

- `obsidian-set` は設計、検証、運用ルール、AI効率化の拠点。
- 本運用 vault は `G:\knowledge-vault`。
- `G:\knowledge-vault` は初期 GitHub repo 化しない。
- vault 正本はローカル Markdown。
- backup は別ドライブ日付付き snapshot を優先する。
- `G:\devwork` 配下の各開発PJは、必要に応じて個別に GitHub repo 化する。
- LLM記憶は `memory/` に置くが、詳細正本にはしない。

## ディレクトリ役割

| Path | 役割 | 初期導入 |
|---|---|---|
| `memory/` | LLM 用の想起・圧縮レイヤー | yes |
| `memory/l1-triggers.md` | 常時読む短いキーワードとリンク | yes |
| `memory/l2-models/` | 未確定の理解モデル、仮説、違和感 | yes |
| `memory/l3-summaries/` | 実施したことの概略 | yes |
| `memory/l4-records/` | 詳細記録、または詳細正本への入口 | yes |
| `knowledge/dev/` | 開発ノウハウ | yes |
| `knowledge/ai/` | AI、LLM、agent、MCP、RAG、eval | yes |
| `knowledge/decisions/` | 判断済み事項と理由 | yes |
| `tasks/active/` | 実行中タスク | yes |
| `tasks/done/` | 完了タスク要約 | yes |
| `tasks/handoff/` | セッション引き継ぎ | yes |
| `sources/` | 根拠資料、source-backed note | yes |
| `prompts/` | ユーザプロンプト全文、AI回答要約 | yes |
| `inbox/` | 未整理情報の一時置き場 | yes |
| `templates/` | note template | yes |
| `attachments/` | 画像、PDF、添付 | yes |

## 重複回避ルール

- 同じ事実セットの正本は1つ。
- `memory/` に詳細本文を重複保存しない。
- `memory/` は `knowledge/`, `tasks/`, `sources/`, `prompts/` への入口。
- `sources/` は根拠の正本。
- `tasks/` は実施履歴の正本。
- `knowledge/` は再利用知識の正本。
- `prompts/` は会話入力とAI出力要約の正本。
- `inbox/` は未整理であり正本ではない。

## LLM記憶階層

| 層 | 内容 | 正本性 |
|---|---|---|
| L1 | 常時読むトリガー、キーワード、リンク | 正本ではない |
| L2 | 未確定モデル、仮説、違和感 | 仮置き |
| L3 | 実施概要、作業要約 | 要約 |
| L4 | 詳細記録、または詳細正本への入口 | 内容次第 |

運用:

- L1 は短く保つ。
- L2 は決定事項を書かない。
- L3 は詳細を書かずリンクする。
- L4 は必要時だけ詳しくする。

## P0

| Rank | 候補 | 元番号 | 判定 | 反映先 |
|---:|---|---:|---|---|
| 1 | vault operation を新構成で定義 | 01 | P0 | `AGENTS.md`, `PROJECT.md`, `memory/README.md` |
| 2 | frontmatter schema を template へ反映 | 05 | P0 | `templates/*.md` |
| 3 | source-backed note を採用 | 06 | P0 | `sources/`, `templates/source-note.md` |
| 4 | inbox 運用を採用 | 18 | P0 | `inbox/`, `templates/inbox-note.md` |
| 5 | AI session summary を採用 | 19 | P0 | `prompts/`, `templates/ai-session-summary.md` |
| 6 | GitHub / vault 境界を定義 | 20 | P0 | `PROJECT.md`, `tasks/README.md` |
| 7 | knowledge index を memory 階層へ再設計 | 17 | P0 | `memory/l1-l3` |
| 8 | query protocol は可変ルール化 | 04 | P0 | 後で `memory` 読込手順へ接続 |

P0意図:

```text
1. vaultの正本とbackup方針を決める
2. note metadataを揃える
3. 根拠資料の保存形式を決める
4. 未整理情報の逃げ場を作る
5. AI会話保存形式を作る
6. GitHubとvaultの責務を分ける
7. LLM記憶階層を作る
8. 問い合わせ形式は運用で調整する
```

## P1

| Rank | 候補 | 元番号 | 判定 | 反映先 |
|---:|---|---:|---|---|
| 9 | dev taxonomy を反映 | 02 | P1 | `knowledge/dev/` |
| 10 | ai taxonomy を反映 | 03 | P1 | `knowledge/ai/` |
| 11 | backup / sync 方針を更新 | 10 | P1 | `PROJECT.md`, backup script候補 |
| 12 | Web Clipper 保存先を決める | 11 | P1 | `sources/`, `attachments/` |

## P2以降

| Rank | 候補 | 元番号 | 判定 | 理由 |
|---:|---|---:|---|---|
| 13 | SQL queryable vault | 22 | P2 | frontmatter と正本配置後 |
| 14 | Local REST API plugin | 12 | P2 | 検証用vaultで試す |
| 15 | Obsidian MCP server | 13 | P2 | 12の上位層として一体検討 |
| 16 | markdownlint | 09 | P2 | 品質補助 |
| 17 | Foam | 08 | P3 | VS CodeをObsidian風に使う補助 |
| 18 | 実運用パターン追加 | 21 | P3 | 継続取り込み |

## Rejected / 保留

| 元番号 | 候補 | 扱い |
|---:|---|---|
| 07 | VS Code Markdown extension比較 | rejected |
| 14 | VS Code MCP workspace設定案 | rejected |
| 15 | Claude Code MCP project scope案 | rejected |
| 16 | Gemini CLI MCP案 | rejected |

## 最大構成

```text
G:\knowledge-vault\
  AGENTS.md
  PROJECT.md
  README.md
  memory/
    l1-triggers.md
    l2-models/
      *.md
    l3-summaries/
      weekly/
      task/
    l4-records/
      decisions/
      operational-knowledge/
  knowledge/
    dev/
      git/
      testing/
      debugging/
      windows/
      vscode/
      ai-coding/
      mcp/
    ai/
      models/
      agents/
      prompting/
      tool-use/
      mcp/
      rag/
      eval/
      security/
    decisions/
      active/
      superseded/
  tasks/
    active/
    done/
    handoff/
  sources/
    official/
    primary/
    secondary/
    local/
    experiment-result/
  prompts/
    codex/
    claude-code/
    gemini-cli/
  inbox/
  templates/
  attachments/
    images/
    pdf/
    web-clipper/
  scripts/
    backup/
    index-vault/
    query-vault/
  data/
    vault.sqlite
    vault.duckdb
```

## 既に作成済み

`G:\knowledge-vault` に初期構成を作成済み。

作成済み入口:

- `G:\knowledge-vault\AGENTS.md`
- `G:\knowledge-vault\PROJECT.md`
- `G:\knowledge-vault\README.md`
- `G:\knowledge-vault\memory\README.md`
- `G:\knowledge-vault\memory\l1-triggers.md`
- `G:\knowledge-vault\tasks\active\2026-04-18-vault-bootstrap.md`
- `G:\knowledge-vault\tasks\handoff\2026-04-18-vault-bootstrap-handoff.md`

## 次の作業

判断不要:

1. `docs/guide/vault-operation.md` を新方針へ更新。
2. `docs/guide/source-backed-notes.md` を `sources/` 前提へ更新。
3. `docs/guide/ai-session-summary.md` を `prompts/` + `tasks/` 前提へ更新。
4. `docs/condi-ref/github-vault-boundary.md` を `G:\devwork` 各PJ GitHub + `G:\knowledge-vault` 分離へ更新。
5. backup script案を作る。

判断待ち:

1. backup 先。採用: `H:\bk\knowledge-vault-snapshots\YYYY-MM-DD_HHmmss\`
2. `memory/l2`, `memory/l3`, `memory/l4` の粒度。
3. Web Clipper は見送り。
4. P1で Dataview と SQLite を入れる。DuckDB は後段。

## PRP command試用メモ

`commands/prp-plan.md` は本来 `.claude/PRPs/plans/` 出力前提。
このPJでは `AGENTS.md` / `PROJECT.md` の情報配置を優先し、成果物は `docs/imp/task-a-vault-structure-plan.md` に置く。
