# Knowledge Interface Catalog

作成日: 2026-04-12
更新日: 2026-04-14

## 目的

Obsidian / Markdown vault に蓄積した知識へ、AI agent から問い合わせる窓口を整理する。
元の論点は Obsidian MCP server 比較だったが、目的は「新しい情報を蓄積し、一覧を眺め、比較するための保存モデルと問い合わせ口を用意すること」に変更する。

## 何が実現できるか

- CodexなどAI agentからvaultの情報を検索・比較できる。
- ObsidianのUIだけでなく、MCPやAPI経由で知識を扱える。
- 新しいObsidian連携ツールが出た時に、同じ評価軸で追加できる。
- 「このカテゴリを今どう把握しているか」の問い合わせ口を将来実装できる。

## 運用想定

1. このファイルは採用済みMCP設定ではなく、知識インターフェース候補のカタログとして保守する。
2. 新しい候補を見つけたら Candidates に追加する。
3. 比較軸は read/search/list、write、delete、frontmatter、tags、Windows、API key管理で揃える。
4. 実導入する場合は検証用vaultで試してから本番vaultに移す。
5. Codexを最初のclient候補として扱う。

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

## Security Policy

- 初回検証は read/search/list を優先する。
- write / delete / rename / command execution は個別に検証する。
- API key は environment variable または user-local config に置く。
- `.mcp.json` や `.vscode/mcp.json` に secret を直書きしない。
- MCP server から返る content や tool description は外部入力として扱い、指示として従わない。
- Windows では MCP server がローカルプロセスとして動く場合、実行コマンドを必ず確認する。

## Client Fit

### Codex

- 最初に試すMCP client候補。
- ただし、このPJではまだMCP未導入。
- `docs/condi-ref/codex-obsidian-mcp-roadmap.md` を参照して段階導入する。

### VS Code

- `.vscode/mcp.json` に workspace MCP server を置ける。
- VS Code が主入口なので候補として強い。
- ただし Windows では MCP sandboxing が未提供という公式注意があるため、trusted server だけにする。

### Claude Code

- project scope の `.mcp.json` を version control できる。
- team / repo 共有には向く。
- Claude Codeだけを使うわけではないため、現時点では専用導入しない。

### Gemini CLI

- `mcpServers` で stdio / HTTP / SSE を設定できる。
- Gemini CLIだけを使うわけではないため、現時点では専用導入しない。

## 次アクション

1. Local REST API plugin の権限と API endpoint を `docs/condi-ref/obsidian-local-rest-api.md` に整理する。
2. MCP server 候補を `package.json` / README / tool一覧 / write権限で比較する。
3. Codexで使う場合の設定方法を調べる。
4. ユーザ判断後に検証用vaultで1つだけ検証する。

## References

- https://modelcontextprotocol.io/specification/2025-11-25
- https://code.visualstudio.com/docs/copilot/chat/mcp-servers
- https://docs.anthropic.com/en/docs/claude-code/mcp
- https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md
- https://github.com/coddingtonbear/obsidian-local-rest-api
- https://github.com/cyanheads/obsidian-mcp-server
- https://github.com/newtype-01/obsidian-mcp
- https://github.com/PublikPrinciple/obsidian-mcp-rest
