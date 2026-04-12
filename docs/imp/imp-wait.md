# Decision Wait List

作成日: 2026-04-12

## 判断待ち

1. Obsidian Sync に課金する可能性を前提に、GitHub repo とどう併用するか。
   - 選択肢: Gitを正、Syncは端末同期 / Syncを正、Gitはバックアップ / 当面WindowsのみでGit運用。

2. VS Code extension を入れるか。
   - 候補: Markdown All in One、markdownlint、Foam、MLink。
   - 初期推奨: Markdown All in One と markdownlint は採用候補。Foam / MLink は評価後。

3. Obsidian Web Clipper を使うか。
   - 使う場合、保存先、template、source URL、引用量ルールを決める。

4. Obsidian community plugin を許可するか。
   - 特に Local REST API plugin は API key と write 権限を伴うため、導入前に範囲を決める。

5. MCP をどの client で最初に試すか。
   - 候補: VS Code workspace MCP、Claude Code project scope、Gemini CLI user config、Codex config。

6. MCP の初期権限を read-only に固定するか。
   - 初期推奨: read-only。write / delete / command execution は後で個別許可。

7. Obsidian MCP server 候補のどれを評価対象にするか。
   - 候補: `cyanheads/obsidian-mcp-server`, `newtype-01/obsidian-mcp`, `PublikPrinciple/obsidian-mcp-rest`。

8. notes のカテゴリをどこまで最初に作るか。
   - 初期推奨: `dev`, `ai`, `ops`, `sources`, `inbox` 程度に絞る。

9. `docs/` 以外に Obsidian vault 用の top-level note directory を作るか。
   - 候補: `notes/`, `knowledge/`, `vault/`。
   - 初期推奨: まだ作らず `docs/guide`, `docs/spec`, `docs/imp` を運用してから判断。

10. AI会話ログを保存するか、要約だけ保存するか。
    - 初期推奨: 要約だけ保存。全文ログはノイズと秘匿情報のリスクが大きい。

## 判断不要で先に進めること

1. `docs/guide/vault-operation.md` のドラフト作成。
2. `docs/spec/note-frontmatter.md` のドラフト作成。
3. `docs/guide/query-protocol.md` のドラフト作成。
4. `docs/spec/obsidian-mcp-evaluation.md` の比較表作成。
5. `docs/spec/sync-strategy.md` の選択肢整理。

