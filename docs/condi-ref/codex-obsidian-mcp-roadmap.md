# Codex Obsidian MCP Roadmap

作成日: 2026-04-14

## ユーザ回答の反映

- 最初に試す MCP client: Codex
- MCP 権限: ユーザ回答は「全部許可」
- community plugin: 必要になったら入れる
- Sync: 一旦PCのみGit運用

## 実務上の解釈

「全部許可」は最終的に write / delete / command execution まで許可し得る、という方針として扱う。
ただし、初回検証では vault破壊を避けるため、段階的に許可する。

段階:

1. read/search/list
2. create/append
3. update frontmatter/tags
4. overwrite
5. delete / command execution

## なぜ段階化するか

- Obsidian vault はMarkdownファイル群なので、MCPのwrite/deleteは直接知識資産を変更する。
- Local REST API plugin の API key が漏れると vault 操作権限になる。
- MCP server はローカルプロセスとして実行されるため、実行元の信頼性確認が必要。
- 「全部許可」の方針でも、検証手順は段階化した方が切り戻しやすい。

## 候補比較の現時点評価

| Candidate | 良いところ | 悪いところ | うれしいこと |
|---|---|---|---|
| cyanheads/obsidian-mcp-server | tool が豊富。read/write/search/frontmatter/tags/delete などを広く扱える。npm package利用しやすい | 権限が広い。Local REST API plugin とAPI keyが必要 | CodexからObsidianを実用的に操作できる可能性が高い |
| newtype-01/obsidian-mcp | DXT / npm など利用導線がある。note/folder管理やsearchを扱う | 削除やfolder操作まで含むため検証時の権限管理が重要 | GUI寄りの導入体験が合えば簡単に試せる可能性 |
| PublikPrinciple/obsidian-mcp-rest | 機能が比較的シンプル。read/write/list/search/metadata | npm install -g やconfig file運用が必要。候補としては小さめ | シンプルな比較対象として使える |

## 初期推奨

最初に評価するなら `cyanheads/obsidian-mcp-server`。

理由:

- Obsidian Local REST API plugin との接続を明確に前提化している。
- tool が多く、将来の「全部許可」方針にも対応しやすい。
- 逆に権限が広いので、最初は実運用 vault ではなく検証用 vault で試す。

## 必要な準備

1. 検証用 Obsidian vault を作る。
2. Local REST API plugin を検証用 vault にだけ入れる。
3. API key を repo に保存しない運用を決める。
4. Codex 側の MCP 設定方法を確認する。
5. read/search/list だけで疎通確認する。
6. create/append を検証する。
7. overwrite/delete は最後に試す。

## まだ実施しないこと

- 本番 vault への Local REST API plugin 導入。
- `.mcp.json` への secret 直書き。
- delete tool の自動承認。
- Obsidian command execution の自動承認。

## References

- https://modelcontextprotocol.io/specification/2025-11-25
- https://github.com/coddingtonbear/obsidian-local-rest-api
- https://github.com/cyanheads/obsidian-mcp-server
- https://github.com/newtype-01/obsidian-mcp
- https://github.com/PublikPrinciple/obsidian-mcp-rest

