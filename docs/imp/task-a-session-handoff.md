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
8. `docs/imp/task-a-vault-structure-plan.md`
9. `G:\knowledge-vault\AGENTS.md`
10. `G:\knowledge-vault\PROJECT.md`
11. `G:\knowledge-vault\tasks\handoff\2026-04-18-vault-bootstrap-handoff.md`
12. 必要に応じて `commands/prp-implement.md`

## 現在の前提

- `obsidian-set` は本運用の vault 本体ではない。
- `obsidian-set` は Obsidian 運用ルール、仕組み、AI 効率化の拠点として扱う。
- 本運用の知識ベース vault は別ディレクトリに作る方針。
- 2026-04-18 時点では、本運用 vault は `G:\knowledge-vault` に作成する方針。
- 本運用 vault 自体は初期状態では GitHub repo 化しない。ローカル正本 + 別ドライブへの世代 snapshot backup を基本にする。
- `G:\devwork` 配下の各開発PJは必要に応じて GitHub repo 化するが、横断ナレッジ vault とは分ける。
- 本運用 vault には `knowledge/`, `memory/`, `tasks/`, `sources/`, `prompts/`, `inbox/` を分けて作る。
- `memory/` は LLM 用の想起・圧縮レイヤーであり、詳細正本にはしない。
- `docs/guide/` と `docs/spec/` は、仕組み化が進んだ結果の置き場。
- `docs/condi-ref/` は採用未確定の調査、比較、候補。
- `docs/imp/` は作業計画、進捗、判断待ち、作業ログ。
- `docs/Z_trash/` は使わないと判断した候補の退避場所。vault の一般的なゴミ箱とは別。

## 2026-04-18 作業中ステータス

- ユーザ判断により、まず `G:\knowledge-vault` を実作成する。
- P0 は旧案の `knowledge/index` 中心ではなく、`knowledge + memory + tasks + sources + prompts + inbox` の分離で進める。
- `01 vault-operation` は「ローカル正本、GitHub repo 化しない、別ドライブ世代 snapshot backup」を含むメタルールとして作成する。
- `06 source-backed note` は採用。
- `04 query-protocol` は好みが出るため、初期は可変プロトコルとして扱う。
- `17 knowledge index` は LLM 記憶階層の L1-L3 と接続して再設計する。
- `20 GitHub / vault boundary` は、各開発PJ GitHub と横断 vault の分離、vault backup 方針を含めて扱う。
- `G:\knowledge-vault` の初期ディレクトリと基本Markdownを作成済み。
- 作成済み入口: `G:\knowledge-vault\AGENTS.md`, `G:\knowledge-vault\PROJECT.md`, `G:\knowledge-vault\README.md`
- 作成済み引き継ぎ: `G:\knowledge-vault\tasks\handoff\2026-04-18-vault-bootstrap-handoff.md`
- `docs/imp/task-a-vault-structure-plan.md` は新方針へ更新済み。
- `.agents/skills/genshijin/` が追加された。ユーザが `genshijin`、`genshijin 極限` を指定し、以後の会話は短文圧縮モード前提。

## タスクA 方針変更後の構成

旧方針:

```text
knowledge/
  index/
  dev/
  ai/
  sources/
  prompts/
  decisions/
  inbox/
templates/
attachments/
```

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

役割:

- `knowledge/`: 人間向け整理済みナレッジの正本。
- `memory/`: LLM 用の想起・圧縮レイヤー。詳細正本ではない。
- `tasks/`: タスク単位の作業記録、実施概要、引き継ぎ。
- `sources/`: 根拠資料、source-backed note の正本。
- `prompts/`: ユーザプロンプト全文と AI 回答要約。
- `inbox/`: 未整理情報の一時置き場。

記憶階層:

- L1: 常時読む短いトリガーとリンク。
- L2: 未確定の理解モデル、仮説、違和感。
- L3: 実施したことの概略。
- L4: 詳細記録、または詳細正本への入口。

重複回避:

- 同じ事実セットの正本は1つにする。
- `memory/` に詳細本文を重複保存しない。
- `memory/` は `knowledge/`, `tasks/`, `sources/`, `prompts/` への入口として使う。
- `sources/` は根拠、`tasks/` は実施履歴、`knowledge/` は再利用知識。

## タスクA P0/P1 再編成案

P0:

- `01 vault-operation`: 採用。ローカル正本、GitHub repo 化しない、別ドライブ世代 snapshot backup、各ディレクトリ役割のメタルール。
- `05 note frontmatter`: 採用。全 note / template の検索・SQL化前提。
- `06 source-backed note`: 採用。`sources/` の根拠保存ルール。
- `18 inbox`: 採用。`inbox/` の未整理一時保存と昇格ルール。
- `19 ai-session-summary`: 採用。`prompts/` と `tasks/` に接続。
- `20 GitHub / vault boundary`: 採用。`G:\devwork` 配下の各開発PJ GitHub と `G:\knowledge-vault` を分離。
- `17 knowledge index`: 再設計。旧 `knowledge/index` ではなく、`memory/l1-l3` として扱う。
- `04 query-protocol`: 可変ルール。LLM回答フォーマットなので好みで変更余地あり。

P1:

- `02 dev-knowledge-taxonomy`: `knowledge/dev/` に反映。
- `03 ai-knowledge-taxonomy`: `knowledge/ai/` に反映。
- `10 sync-strategy`: GitHub repo 化ではなく、ローカル正本 + 別ドライブ snapshot backup 前提に更新。
- `11 Web Clipper`: `sources/` 保存先で検討継続。

後段:

- `08 Foam`: VS Code を Obsidian 風に使う補助。P0後。
- `09 markdownlint`: Markdown品質補助。P0後。
- `12 Local REST API`: Obsidian外部読み書き入口。P0後、検証用vaultで試す。
- `13 Obsidian MCP`: 12の上位層。AI agent tool化。12と一体構成で検討。
- `21 実運用パターン`: 継続取り込み。
- `22 SQL queryable vault`: frontmatter と正本配置が固まった後。

## タスクA 現在状態

- 方針変更後の構成整理: done
- `G:\knowledge-vault` 初期作成: done
- `docs/imp/task-a-vault-structure-plan.md` 新方針反映: done
- `docs/guide/*` と `docs/condi-ref/github-vault-boundary.md` の新方針同期: done
- Web Clipper 見送り: decided
- backup root: `H:\bk\knowledge-vault-snapshots\`
- P1 Dataview: installed
- P1 SQLite: `G:\knowledge-vault\data\vault.sqlite` 生成済み
- Obsidian registry に `G:\knowledge-vault` 登録済み
- `G:\knowledge-vault\tech-stack.md` 作成済み。参照URL集約先。
- Local REST API plugin 設置済み。API key確認と疎通確認はObsidian有効化後。
- 2026-04-27: Dataview dashboard 調整、backup script 試行、memory L2-L4 README作成、SQLite再indexを実施。
- 2026-04-27: 他PJ向け `G:\knowledge-vault` 参照テンプレートを作成。
- 次: Local REST API疎通確認、backup世代数の決定

## GitHub / Backup 方針

- `G:\devwork` 配下の各PJは、必要に応じて GitHub repo 化する。
- `G:\knowledge-vault` 本体は初期 GitHub repo 化しない。
- vault backup は、別ドライブへの日付付き snapshot を優先する。
- 例: `G:\knowledge-vault` -> `H:\backup\knowledge-vault-snapshots\YYYY-MM-DD\`
- GitHub Private repo で snapshot 運用する案は保留。
- Google Drive 等クラウドへの圧縮断面アップロードも将来候補。

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
