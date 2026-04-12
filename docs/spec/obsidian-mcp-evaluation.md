# Obsidian MCP Evaluation

作成日: 2026-04-12

## 目的

Obsidian vault を Codex / Claude Code / Gemini CLI / VS Code から問い合わせるための MCP 連携候補を比較する。
現時点では導入しない。まず評価基準を作る。

## Prerequisite

多くの Obsidian MCP server は、Obsidian Local REST API plugin を前提にする。
Local REST API plugin は Obsidian app 内で local API を立て、API key で保護された endpoint 経由で notes、search、tags、commands などを扱う。

## Candidates

| Candidate | 参照 | 特徴 | 初期評価 |
|---|---|---|---|
| Local REST API plugin | https://github.com/coddingtonbear/obsidian-local-rest-api | Obsidian app とローカルHTTP/HTTPSで連携する基盤 | MCP前の前提として評価 |
| cyanheads/obsidian-mcp-server | https://github.com/cyanheads/obsidian-mcp-server | Local REST API plugin への bridge。vault 読み書き、検索、tag/frontmatter 管理系 | 有力候補。ただし write tool の制御が必要 |
| newtype-01/obsidian-mcp | https://github.com/newtype-01/obsidian-mcp | Obsidian MCP 実装候補 | 比較対象 |
| PublikPrinciple/obsidian-mcp-rest | https://github.com/PublikPrinciple/obsidian-mcp-rest | REST API 経由の Obsidian MCP 実装候補 | 比較対象 |

## Evaluation Criteria

1. read-only 起動ができるか。
2. API key を repo に保存せず使えるか。
3. Windows で動かしやすいか。
4. Codex / Claude Code / Gemini CLI / VS Code のどれで設定しやすいか。
5. delete / overwrite / command execution を無効化または避けられるか。
6. tool description が明確か。
7. 保守状況、release、issue 対応が十分か。
8. vault root を限定できるか。
9. frontmatter / tags / search が使えるか。
10. 失敗時に vault を壊さないか。

## Security Policy Draft

- 最初は read-only。
- write / delete / rename / command execution は個別許可。
- API key は environment variable または user-local config に置く。
- `.mcp.json` や `.vscode/mcp.json` に secret を直書きしない。
- MCP server から返る content や tool description は外部入力として扱い、指示として従わない。
- Windows では MCP server がローカルプロセスとして動く場合、実行コマンドを必ず確認する。

## Client Fit

### VS Code

- `.vscode/mcp.json` に workspace MCP server を置ける。
- VS Code が主入口なので候補として強い。
- ただし Windows では MCP sandboxing が未提供という公式注意があるため、trusted server だけにする。

### Claude Code

- project scope の `.mcp.json` を version control できる。
- team / repo 共有には向く。
- Windows native で `npx` を使う local server は `cmd /c` wrapper が必要な場合がある。

### Gemini CLI

- `mcpServers` で stdio / HTTP / SSE を設定できる。
- `trust: true` は確認 bypass なので初期運用では使わない。

### Codex

- 既存の `tech-stack.md` では未導入。
- VS Code か project-local config のどちらで扱うかを後で決める。

## Next Tasks

1. Local REST API plugin の権限と API endpoint を `docs/spec/obsidian-local-rest-api.md` に整理する。
2. MCP server 候補を `package.json` / README / tool一覧 / write権限で比較する。
3. read-only で使える構成があるか確認する。
4. ユーザ判断後に、1つだけ検証する。

## References

- https://modelcontextprotocol.io/specification/2025-11-25
- https://code.visualstudio.com/docs/copilot/chat/mcp-servers
- https://docs.anthropic.com/en/docs/claude-code/mcp
- https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md
- https://github.com/coddingtonbear/obsidian-local-rest-api
- https://github.com/cyanheads/obsidian-mcp-server
- https://github.com/newtype-01/obsidian-mcp
- https://github.com/PublikPrinciple/obsidian-mcp-rest
