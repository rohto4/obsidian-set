# Decision Wait List

作成日: 2026-04-12
更新日: 2026-04-18

## メモ取り込み（2026-04-14）

`docs/memo.txt` の三分類を取り込み済み。

- 良さそう・やりたい: 02, 03, 05, 10, 11, 13, 19, 22
- 要検討: 01, 04, 06, 08, 09, 12, 17, 18, 20, 21
- 要らない: 07, 14, 15, 16

反映先:
- 実行進捗と判断を分離して `docs/imp/imp-plan.md` に同期
- 要らない項目は `docs/Z_trash/` へ移動済み
- 要検討項目は `docs/condi-ref/` に残して比較・検証を継続

## 回答済み

1. Obsidian Sync に課金する可能性を前提に、GitHub repo とどう併用するか。
   - 元の選択肢: Gitを正、Syncは端末同期 / Syncを正、Gitはバックアップ / 当面WindowsのみでGit運用。
   - 回答: 一旦PCのみでGit運用。
   - 反映: `docs/guide/sync-strategy.md` の初期推奨と一致。PC + GitHub repo 正本で進める。

2. VS Code extension を入れるか。
   - 元の候補: Markdown All in One、markdownlint、Foam、MLink。
   - 回答: おすすめで。
   - 追加判断: VS Code extension 候補比較は不要。installして試して消す運用で十分。
   - 反映: `docs/Z_trash/tools/vscode-extensions.md` へ移動。markdownlint単体は `docs/condi-ref/markdownlint.md` に要検討として残す。

3. Obsidian Web Clipper を使うか。
   - 元の論点: 使う場合、保存先、template、source URL、引用量ルールを決める。
   - 回答: 何がうれしいツールか確認したい。
   - 反映: `docs/guide/web-clipper.md` を作成。Web情報をsource note化し、LLM問い合わせ材料にする用途として整理。

4. Obsidian community plugin を許可するか。
   - 元の論点: Local REST API plugin は API key と write 権限を伴う。
   - 回答: 必要になったら入れる。
   - 反映: まだ導入しない。MCP検証前に Local REST API plugin を検証用 vault で検討する。

5. MCP をどの client で最初に試すか。
   - 元の候補: VS Code workspace MCP、Claude Code project scope、Gemini CLI user config、Codex config。
   - 回答: Codex。
   - 反映: `docs/condi-ref/codex-obsidian-mcp-roadmap.md` を作成。

6. MCP の初期権限を read-only に固定するか。
   - 元の推奨: read-only。write / delete / command execution は後で個別許可。
   - 回答: 全部許可。
   - 反映: 最終方針は広い権限を許可し得るものとして扱う。ただし検証は read/search/list -> create/append -> update -> overwrite -> delete/command execution の順で段階化する。

7. Obsidian MCP server 候補のどれを評価対象にするか。
   - 元の候補: `cyanheads/obsidian-mcp-server`, `newtype-01/obsidian-mcp`, `PublikPrinciple/obsidian-mcp-rest`。
   - 回答: 優劣が分からない。いいところ、悪いところ、何がうれしいか解説が必要。
   - 追加判断: 単なるMCP候補比較ではなく、新しい情報を蓄積して一覧・比較するための保存モデルと問い合わせ口として採用したい。
   - 反映: `docs/guide/knowledge-interface-catalog.md` へ昇格・改題。`docs/condi-ref/codex-obsidian-mcp-roadmap.md` はCodex連携ロードマップとして残す。

8. notes のカテゴリをどこまで最初に作るか。
   - 元の推奨: `dev`, `ai`, `ops`, `sources`, `inbox` 程度。
   - 回答: Obsidianの保存体系ならカテゴリ分け候補を5パターン見たい。
   - 反映: `docs/condi-ref/knowledge-category-options.md` を作成。

9. `docs/` 以外に Obsidian vault 用の top-level note directory を作るか。
   - 元の候補: `notes/`, `knowledge/`, `vault/`。
   - 回答: `docs/guide`, `docs/spec`, `docs/imp` はPJで使用する設計書類の分類で、Obsidianの分け方とは今のところ無関係。
   - 反映: `docs/condi-ref/knowledge-category-options.md` でObsidian側の保存体系を別枠として整理。

10. AI会話ログを保存するか、要約だけ保存するか。
    - 元の推奨: 要約だけ保存。
    - 回答: ユーザプロンプトは全文保存。AIの出力は要約保存。どういうプロセスで回答したかまで保存したい。
    - 反映: `docs/guide/ai-session-summary.md` を作成。

## 新規判断待ち

0. タスクA: 方針変更後の本運用 vault 構成を `task-a-vault-structure-plan.md` に反映するか。
   - 参照: `docs/imp/task-a-vault-structure-plan.md`
   - 現在地: `G:\knowledge-vault` は作成済み。
   - 新構成: `knowledge + memory + tasks + sources + prompts + inbox`。
   - 未完了: `task-a-vault-structure-plan.md` は旧 `knowledge/index` 中心案のまま。
   - 判断点: 新構成をタスクA正式成果物として上書き更新するか。

1. `docs/condi-ref/knowledge-category-options.md` の Option 1-5 のどれを採用するか。
   - 現在の扱い: 旧案。新方針では `memory/`, `tasks/`, top-level `sources/`, `prompts/`, `inbox/` を追加した構成へ再設計済み。

2. markdownlintをPJ設定として採用するか。
   - 先に `docs/condi-ref/markdownlint.md` でメリットと邪魔になる可能性を確認する。
   - `.markdownlint.json` 追加は未実施。

3. Obsidian Web Clipper を実際に使うか。
   - `docs/guide/web-clipper.md` へ昇格済み。
   - 回答: 見送り。
   - 反映: P1では導入しない。将来使う場合の保存先は `G:\knowledge-vault\sources\`。

4. Codex + Obsidian MCP の検証用 vault を作るか。
   - 初期おすすめ: 本番 `obsidian-set` ではなく検証用 vault で試す。

5. MCPの「全部許可」を本番vaultにも適用するか。
   - 初期おすすめ: 最終的には許可してよいが、検証順は段階化する。

6. `docs/guide/sql-queryable-vault.md` のどの方式を最初に試すか。
   - 候補: Dataview、Query All The Things、SQLite FTS5、DuckDB。
   - 回答: P1で Dataview と SQLite を入れる。
   - 反映: Dataview dashboard と SQLite indexer を作成。

7. `docs/guide/vault-operation.md` / `docs/guide/query-protocol.md` / `docs/guide/source-backed-notes.md` の役割重複を許容できるか。
   - 現在の方針: `vault-operation` はメタルール、`query-protocol` は可変回答フォーマット、`source-backed-notes` は `sources/` の根拠資料note形式。

8. vault backup 先をどこにするか。
   - 回答: `H:\bk\` 配下。
   - 反映: `H:\bk\knowledge-vault-snapshots\` を初期 backup root にする。

## 判断不要で先に進めたこと

1. `docs/condi-ref/markdownlint.md` のドラフト作成。
2. `docs/guide/source-backed-notes.md` のドラフト作成。
3. `docs/guide/dev-knowledge-taxonomy.md` のドラフト作成。
4. `docs/guide/ai-knowledge-taxonomy.md` のドラフト作成。
5. `docs/condi-ref/obsidian-local-rest-api.md` のドラフト作成。
6. 要らない分類のVS Code extension候補ファイルを `docs/Z_trash/tools/vscode-extensions.md` へ移動。
7. やりたい分類の `sync-strategy`, `web-clipper`, `knowledge-interface-catalog`, `sql-queryable-vault` を `docs/guide/` へ昇格。
8. 要検討分類の `markdownlint`, `obsidian-local-rest-api`, `practical-obsidian-workflows` は `docs/condi-ref/` に残して補足。

## 次に判断不要で進められること

0. `docs/imp/task-a-vault-structure-plan.md` を新構成に更新する。
1. `docs/condi-ref/markdownlint.md` をもとに `.markdownlint.json` の案を作る。
2. `docs/condi-ref/knowledge-category-options.md` は旧候補として扱い、新構成の正式案は `task-a-vault-structure-plan.md` 側へ集約する。
3. `docs/condi-ref/obsidian-local-rest-api.md` をもとに、検証用 vault の作成手順を書く。
4. `docs/condi-ref/foam-evaluation.md` をもとに、導入待ちの判断材料を増やす。
5. `docs/condi-ref/github-vault-boundary.md` をもとに、重複管理しそうなポイントを整理する。
6. `docs/condi-ref/index-policy.md` をもとに、source-backed note と index の役割差を検討する。
