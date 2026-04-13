# Decision Wait List

作成日: 2026-04-12
更新日: 2026-04-14

## 回答済み

1. Obsidian Sync に課金する可能性を前提に、GitHub repo とどう併用するか。
   - 元の選択肢: Gitを正、Syncは端末同期 / Syncを正、Gitはバックアップ / 当面WindowsのみでGit運用。
   - 回答: 一旦PCのみでGit運用。
   - 反映: `docs/spec/sync-strategy.md` の初期推奨と一致。PC + GitHub repo 正本で進める。

2. VS Code extension を入れるか。
   - 元の候補: Markdown All in One、markdownlint、Foam、MLink。
   - 回答: おすすめで。
   - 反映: `docs/spec/vscode-extensions.md` を作成。初期おすすめは Markdown All in One と markdownlint。

3. Obsidian Web Clipper を使うか。
   - 元の論点: 使う場合、保存先、template、source URL、引用量ルールを決める。
   - 回答: 何がうれしいツールか確認したい。
   - 反映: `docs/spec/web-clipper.md` を作成。Web情報をsource note化し、LLM問い合わせ材料にする用途として整理。

4. Obsidian community plugin を許可するか。
   - 元の論点: Local REST API plugin は API key と write 権限を伴う。
   - 回答: 必要になったら入れる。
   - 反映: まだ導入しない。MCP検証前に Local REST API plugin を検証用 vault で検討する。

5. MCP をどの client で最初に試すか。
   - 元の候補: VS Code workspace MCP、Claude Code project scope、Gemini CLI user config、Codex config。
   - 回答: Codex。
   - 反映: `docs/spec/codex-obsidian-mcp-roadmap.md` を作成。

6. MCP の初期権限を read-only に固定するか。
   - 元の推奨: read-only。write / delete / command execution は後で個別許可。
   - 回答: 全部許可。
   - 反映: 最終方針は広い権限を許可し得るものとして扱う。ただし検証は read/search/list -> create/append -> update -> overwrite -> delete/command execution の順で段階化する。

7. Obsidian MCP server 候補のどれを評価対象にするか。
   - 元の候補: `cyanheads/obsidian-mcp-server`, `newtype-01/obsidian-mcp`, `PublikPrinciple/obsidian-mcp-rest`。
   - 回答: 優劣が分からない。いいところ、悪いところ、何がうれしいか解説が必要。
   - 反映: `docs/spec/codex-obsidian-mcp-roadmap.md` に候補比較を追加。初期評価対象は `cyanheads/obsidian-mcp-server`。

8. notes のカテゴリをどこまで最初に作るか。
   - 元の推奨: `dev`, `ai`, `ops`, `sources`, `inbox` 程度。
   - 回答: Obsidianの保存体系ならカテゴリ分け候補を5パターン見たい。
   - 反映: `docs/spec/knowledge-category-options.md` を作成。

9. `docs/` 以外に Obsidian vault 用の top-level note directory を作るか。
   - 元の候補: `notes/`, `knowledge/`, `vault/`。
   - 回答: `docs/guide`, `docs/spec`, `docs/imp` はPJで使用する設計書類の分類で、Obsidianの分け方とは今のところ無関係。
   - 反映: `docs/spec/knowledge-category-options.md` でObsidian側の保存体系を別枠として整理。

10. AI会話ログを保存するか、要約だけ保存するか。
    - 元の推奨: 要約だけ保存。
    - 回答: ユーザプロンプトは全文保存。AIの出力は要約保存。どういうプロセスで回答したかまで保存したい。
    - 反映: `docs/guide/ai-session-summary.md` を作成。

## 新規判断待ち

1. `docs/spec/knowledge-category-options.md` の Option 1-5 のどれを採用するか。
   - 初期おすすめ: Option 4 の縮小版。

2. VS Code拡張として Markdown All in One と markdownlint を実際に導入してよいか。
   - docs上の推奨は作成済み。インストール操作は未実施。

3. Obsidian Web Clipper を実際に使うか。
   - 使う場合は保存先 directory とtemplateを決める。

4. Codex + Obsidian MCP の検証用 vault を作るか。
   - 初期おすすめ: 本番 `obsidian-set` ではなく検証用 vault で試す。

5. MCPの「全部許可」を本番vaultにも適用するか。
   - 初期おすすめ: 最終的には許可してよいが、検証順は段階化する。

## 判断不要で先に進めたこと

1. `docs/spec/markdownlint.md` のドラフト作成。
2. `docs/guide/source-backed-notes.md` のドラフト作成。
3. `docs/guide/dev-knowledge-taxonomy.md` のドラフト作成。
4. `docs/guide/ai-knowledge-taxonomy.md` のドラフト作成。
5. `docs/spec/obsidian-local-rest-api.md` のドラフト作成。

## 次に判断不要で進められること

1. `docs/spec/markdownlint.md` をもとに `.markdownlint.json` の案を作る。
2. `docs/spec/knowledge-category-options.md` の初期おすすめ Option 4 縮小版に沿って、directory作成案だけを書く。
3. `docs/spec/obsidian-local-rest-api.md` をもとに、検証用 vault の作成手順を書く。
