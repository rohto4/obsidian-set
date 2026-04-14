# Obsidian Local REST API Evaluation

作成日: 2026-04-14

## 目的

Obsidian と Codex / MCP を接続する前提候補として、Local REST API plugin の検証計画を定義する。

## 位置づけ

Local REST API plugin は Obsidian community plugin。
Obsidian app 内で local REST API を立て、API key で保護された endpoint 経由で vault を操作する。

## 何がうれしいか

- AI agent から note を検索できる。
- active file や periodic note など、Obsidianアプリ側の状態にアクセスできる可能性がある。
- MCP server の土台として使える。
- 将来的に「このカテゴリを今どう把握しているか」をObsidian経由で問い合わせやすくなる。

## 何をするものか

Obsidianアプリ内にローカルREST APIを立て、外部プロセスからvaultを読んだり書いたりできるようにするcommunity plugin。
Codexから直接使うというより、Obsidian MCP serverの裏側の接続口として使う想定。

## 何が良くなるか

- Obsidianアプリが持つactive fileやvault状態を外部から扱える。
- MCP serverがObsidian vaultへアクセスする土台になる。
- 将来、AI agentがnote作成、検索、frontmatter更新を行う道が開ける。

## どう管理するか

- 本番vaultにはまだ入れない。
- 検証用vaultにだけ入れる。
- API key はrepoに保存しない。
- `read/search/list` から検証し、write/deleteは最後に回す。

## 懸念

- API key 管理が必要。
- write / delete / command execution を許可すると vault を壊せる。
- Obsidian app が起動している必要がある構成になりやすい。
- community plugin なので、公式機能ではない。

## 検証手順案

1. 本番 `obsidian-set` ではなく検証用 vault を作る。
2. 検証用 vault に Local REST API plugin を入れる。
3. API key を repo に保存しない。
4. read/search/list のみ疎通する。
5. create/append を検証する。
6. update / overwrite を検証する。
7. delete / command execution は最後に検証する。
8. 検証結果を `docs/imp/` に保存する。

## API Key Policy

- `.env` をGit管理しない。
- `.mcp.json` や `.vscode/mcp.json` に key を直書きしない。
- 必要なら user-local config または環境変数を使う。

## Codex MCP との関係

`docs/condi-ref/codex-obsidian-mcp-roadmap.md` の前段として使う。
MCP server を入れる前に、Local REST API plugin 単体で何ができるか確認する。

## References

- https://github.com/coddingtonbear/obsidian-local-rest-api
- https://coddingtonbear.github.io/obsidian-local-rest-api/
