# Task A Session Handoff

作成日: 2026-04-17

## 目的

このファイルは、セッション切り替え、`/clear`、または context compaction 後に、AI がタスクAを安全に再開するための引き継ぎメモ。

タスクA:

> 実装候補を制限なく挙げた時の最終フォルダ構造の検討 + 実装候補の優先順位付け

最終成果物:

- 最終フォルダ構造の検討
- 実装候補の優先順位付け
- 次の実装に向けた `imp-wait` 系の整理
- 上記を 1 ファイルにまとめた出力

## 初期読み込み

セッション再開時は、最低限次を読む。

1. `AGENTS.md`
2. `PROJECT.md`
3. `docs/ecc-obsidian-setup.md`
4. `docs/guide/vault-operation.md`
5. `docs/imp/imp-plan.md`
6. `docs/imp/imp-wait.md`
7. `commands/prp-plan.md`
8. 必要に応じて `commands/prp-implement.md`

## 現在の前提

- `obsidian-set` は本運用の vault 本体ではない。
- `obsidian-set` は Obsidian 運用ルール、仕組み、AI 効率化の拠点として扱う。
- 本運用の知識ベース vault は別ディレクトリに作る方針。
- 候補名は未確定だが、例として `G:\devwork\knowledge-vault` のような別 repo / vault を想定する。
- `docs/guide/` と `docs/spec/` は、仕組み化が進んだ結果の置き場。
- `docs/condi-ref/` は採用未確定の調査、比較、候補。
- `docs/imp/` は作業計画、進捗、判断待ち、作業ログ。
- `docs/Z_trash/` は使わないと判断した候補の退避場所。vault の一般的なゴミ箱とは別。

## 直近で導入したもの

試用 command:

- `commands/expand-answer.md`
- `commands/prp-plan.md`
- `commands/prp-implement.md`
- `commands/prp-prd.md`

試用 skill:

- `.agents/skills/tdd-workflow/`
- `.agents/skills/verification-loop/`

作成済み guide:

- `docs/guide/inbox-policy.md`

整理済み trash:

```text
docs/Z_trash/
  vault/
  spec/
  tools/
    vscode-extensions.md
  old-memo/
```

## タスクAチェックリスト

### 1. prp-plan の準備

- [ ] `commands/prp-plan.md` を読む。
- [ ] PRP の出力先が `.claude/PRPs/` 前提である点を確認する。
- [ ] この PJ では必要に応じて `docs/imp/` または `docs/condi-ref/` に成果物を置くと判断する。
- [ ] ただし今回は「ECC のやつをそのまま使う」試行なので、可能な限り `prp-plan` の流れを尊重する。

### 2. タスクAの入力を明確化

- [ ] 本運用 vault と `obsidian-set` を分ける前提を書く。
- [ ] 本運用 vault の目的を書く。
- [ ] 実装候補を数量制限なしで洗い出す。
- [ ] 候補ごとに、採用時のディレクトリ影響を整理する。
- [ ] 候補をすべて採用した場合の最大構成を出す。
- [ ] 初期導入に絞った最小構成を出す。
- [ ] 中期構成、将来構成も必要なら分ける。

### 3. 検討対象に含める候補

最低限、`docs/imp/imp-plan.md` の 01-22 を見る。

特に含める:

- 18. inbox 運用
- 11. Obsidian Web Clipper
- 04. 問い合わせフォーマット
- 17. knowledge index
- 12. Local REST API plugin
- 05. note frontmatter schema
- 06. source-backed note
- 19. AI session summary
- 20. GitHub Issue / PR と vault の棲み分け
- 22. SQLで再現可能にvaultを検索する方式

### 4. フォルダ構造の検討

- [ ] `obsidian-set` 側に残すものを定義する。
- [ ] 本運用 vault 側に置くものを定義する。
- [ ] `docs/` 系と `knowledge/` 系を混ぜない。
- [ ] `inbox`, `sources`, `permanent`, `index`, `daily`, `templates`, `attachments` の要否を検討する。
- [ ] `Z_trash` 相当を本運用 vault に置くか検討する。
- [ ] LLM がたどりやすい構成か確認する。
- [ ] Git 管理と Obsidian Sync の併用可能性を考慮する。

### 5. 優先順位付け

- [ ] すぐ実用化できる候補を上位にする。
- [ ] 外部 plugin / MCP / API key が必要な候補は後ろにする。
- [ ] 構造の土台になる候補を先にする。
- [ ] 後から移動コストが高いものを早めに検討する。
- [ ] 根拠が薄いものは `condi-ref` 扱いにする。

### 6. 成果物作成

- [ ] 1ファイルにまとめる。
- [ ] 候補ファイル名は `docs/condi-ref/vault-final-structure-options.md` または `docs/imp/task-a-vault-structure-plan.md`。
- [ ] 最終ファイルには、目的、前提、最大構成、推奨初期構成、優先順位、判断待ちを入れる。
- [ ] `docs/imp/imp-wait.md` に次の実装判断を整理する。
- [ ] `docs/imp/agents-tasks-status.md` に作業記録を追加する。

## タスクAで避けること

- `obsidian-set` を本運用 vault として扱わない。
- 本運用 vault の実フォルダを勝手に作らない。
- Obsidian plugin や MCP を本番 vault 前提で導入しない。
- `docs/guide/` と `docs/spec/` に未確定案を入れない。
- 公式情報、個人ブログ、推論、ユーザ判断を混ぜて正本化しない。

## 期待する最終出力

完了時には、ユーザへ短く次を報告する。

- 作成した 1 ファイルのパス
- 推奨する本運用 vault の初期フォルダ構造
- 優先順位トップ 5
- 次にユーザ判断が必要なこと
- commit / push した場合は commit hash

## `/clear` について

この環境の assistant は UI の `/clear` を発行できない可能性がある。
その場合は、このファイル作成と push まで完了した上でユーザに返す。

ユーザが `/clear` した後、再開する AI はこのファイルを最初に読む。
