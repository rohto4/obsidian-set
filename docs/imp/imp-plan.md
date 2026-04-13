# Obsidian Operation Implementation Plan

作成日: 2026-04-12

## 前提

ユーザは普段 VS Code から Codex / Claude Code / Gemini CLI を使うことが多い。
したがって、最初の運用単位は「Obsidian アプリ」ではなく「VS Code で開ける Markdown vault + Git repo」とする。
Obsidian Windows 版、スマホ版、Obsidian Sync、MCP 連携は段階的に検証する。

## Research Summary

根拠:

- Obsidian Sync は複数デバイス同期、選択同期、version history、security/privacy、headless sync などを扱う有料 add-on。Obsidian 公式 Help は、Dropbox / Google Drive / OneDrive など他の cloud storage と併用する場合は sync conflict 防止のため完全移行を強く推奨している。
- Obsidian Web Clipper は公式の無料 browser extension。ページの highlight と web content の vault 保存、template、variables、filters、logic があり、privacy 説明では content はローカル vault に保存される。
- Local REST API plugin は community plugin だが、notes CRUD、active file、periodic notes、search、commands、tags、open file を HTTPS + API key で扱える。Obsidian と MCP をつなぐ場合の現実的な土台。
- VS Code は workspace の `.vscode/mcp.json` に MCP server を設定できる。公式 docs は local MCP server が任意コードを実行し得るため trusted source と secret 管理を強調している。Windows では VS Code の MCP sandboxing が未提供。
- Claude Code は project scope の `.mcp.json` を version control 可能な MCP 設定として扱う。local / project / user の precedence がある。
- Gemini CLI は `mcpServers` 設定で stdio / HTTP / SSE の MCP server を扱える。`trust` を true にすると確認を bypass するため、この PJ では初期設定で使わない。
- Foam は VS Code + Markdown + wikilinks の PKM として成熟しており、graph、backlinks、tag explorer、daily note などがある。ただし Obsidian と二重の PKM 体験になるため、まずは VS Code 標準 Markdown + 必要最小 extension から始める方が安全。
- Markdown All in One と markdownlint は Markdown 編集・整形・lint の候補。markdownlint は project-local config を推奨しており、チーム / repo 運用に合う。
- 公式情報だけでは実運用の型が薄いため、個人ブログ・実践記事も別枠で参照した。日次ノートをintake layerにして週次レビューで永久noteへ昇格する運用、Inbox / Literature / Permanent / Templates の最小Zettelkasten構成、MOCを後から自然発生させる運用、AIで孤立note・重複・古いMOCを点検する運用がこのPJに合う。
- 個人ブログ系の情報は公式情報ではないため、採用判断の根拠ではなく「試す案」として扱う。詳細は `docs/condi-ref/practical-obsidian-workflows.md` に分離した。

参照:

- https://help.obsidian.md/sync
- https://help.obsidian.md/web-clipper
- https://docs.obsidian.md/
- https://git-scm.com/docs
- https://modelcontextprotocol.io/specification/2025-11-25
- https://code.visualstudio.com/docs/copilot/chat/mcp-servers
- https://docs.anthropic.com/en/docs/claude-code/mcp
- https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md
- https://github.com/coddingtonbear/obsidian-local-rest-api
- https://github.com/cyanheads/obsidian-mcp-server
- https://github.com/newtype-01/obsidian-mcp
- https://github.com/PublikPrinciple/obsidian-mcp-rest
- https://github.com/foambubble/foam
- https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
- https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint
- https://parazettel.com/articles/obsidian-daily-workflows/
- https://aiproductivity.ai/guides/obsidian-daily-notes-workflow/
- https://desktopcommander.app/blog/zettelkasten-obsidian/
- https://www.xda-developers.com/tried-using-vs-code-obsidian-notes/

## Current Recommendation

Phase 1 は「Obsidian を使う前に repo と Markdown の知識運用を固める」。

1. `docs/guide/` に運用ルールを作る。
2. `docs/condi-ref/` に技術・構成・採用判断の候補を書く。
3. 実装対象として確定したものだけ `docs/spec/` に移す。
4. `docs/imp/` に作業計画、判断待ち、AI作業状況を書く。
5. notes は小さく始め、必要になったカテゴリだけ追加する。
6. MCP / Local REST API / Sync / VS Code extension は検証候補として保持し、いきなり導入しない。

## Task Candidates

### 01. Vault 情報設計の最小ルールを作る

- 出力先: `docs/guide/vault-operation.md`
- 状態: done
- 内容: note の粒度、frontmatter、タグ、リンク、カテゴリの最低ルール。
- 理由: 最初に細かく分類しすぎると破綻する。まず「どこに何を書くか」だけ決める。
- 完了内容: `docs/guide/vault-operation.md` にドラフトを作成。

### 02. 開発ノウハウ用カテゴリを作る

- 出力先: `docs/guide/dev-knowledge-taxonomy.md`
- 状態: done
- 内容: Git、設計、テスト、デバッグ、Windows、VS Code、AI coding、MCP の分類。
- 理由: ユーザの主目的が開発ノウハウ蓄積だから。
- 完了内容: 初期カテゴリと note type mapping を作成。

### 03. AI知識用カテゴリを作る

- 出力先: `docs/guide/ai-knowledge-taxonomy.md`
- 状態: done
- 内容: model、agent、prompting、tool use、MCP、RAG、eval、security の分類。
- 理由: AI知識は変化が速いので、日付、根拠、古くなる条件を持たせる必要がある。
- 完了内容: 初期カテゴリ、freshness policy、query example を作成。

### 04. 「今このカテゴリをどう把握しているか」問い合わせフォーマットを作る

- 出力先: `docs/guide/query-protocol.md`
- 状態: done
- 内容: LLM へ聞く時の質問テンプレート、根拠・推論・未確定を分ける出力形式。
- 理由: Obsidian を通して LLM に聞く用途の中核。
- 完了内容: `research-ops` と `knowledge-ops` に合わせてテンプレートを作成。

### 05. note frontmatter schema を作る

- 出力先: `docs/spec/note-frontmatter.md`
- 状態: done
- 候補 fields: `title`, `type`, `status`, `topic`, `source`, `created`, `updated`, `confidence`, `review_after`, `tags`
- 理由: 後から検索・MCP・LLM要約へつなげやすい。
- 完了内容: schema とサンプル note を作成。

### 06. source-backed note ルールを作る

- 出力先: `docs/guide/source-backed-notes.md`
- 状態: done
- 内容: 公式情報、一次情報、二次情報、推論、個人メモの分離。
- 理由: AI / 開発情報は誤情報が混ざりやすい。
- 完了内容: source class と note structure を作成。

### 07. VS Code Markdown extension 候補を評価する

- 出力先: `docs/condi-ref/vscode-extensions.md`
- 候補: Markdown All in One、markdownlint、Foam、MLink。
- 理由: 普段の入口が VS Code のため。
- 今できること: いきなり install せず、候補と採用条件をまとめる。

### 08. Foam 導入の可否を評価する

- 出力先: `docs/spec/foam-evaluation.md`
- 内容: Obsidian と Foam の役割重複、wikilink 互換、backlinks、graph、daily note。
- 理由: Foam は VS Code で強いが、Obsidian と二重運用になる可能性がある。
- 今できること: 評価観点を書く。導入は判断待ち。

### 09. markdownlint 設定を検討する

- 出力先: `.markdownlint.json` または `docs/condi-ref/markdownlint.md`
- 状態: done
- 理由: Markdown repo として品質を保つ。VS Code extension と CLI の両方に効く。
- 完了内容: `docs/condi-ref/markdownlint.md` にルール案を作成。設定ファイルの追加は判断待ち。

### 10. Obsidian Sync / Git 併用方針を整理する

- 出力先: `docs/condi-ref/sync-strategy.md`
- 状態: done
- 内容: Windows中心、スマホ利用、有料 Sync、GitHub repo、conflict 方針。
- 理由: 公式 Help は Obsidian Sync と他 cloud storage 併用に注意を促している。
- 完了内容: 選択肢とリスクを整理。課金や実導入は判断待ち。

### 11. Obsidian Web Clipper 運用を検討する

- 出力先: `docs/condi-ref/web-clipper.md`
- 内容: 公式 Web Clipper、template、保存先、source URL、引用量、著作権配慮。
- 理由: 開発・AI情報の収集で有用。
- 今できること: 取り込みルールを作る。extension install は判断待ち。

### 12. Local REST API plugin 検証計画を作る

- 出力先: `docs/condi-ref/obsidian-local-rest-api.md`
- 状態: done
- 内容: API key 管理、read-only から始める方針、curl 疎通確認、search / active file / tags。
- 理由: MCP 連携の現実的な土台。
- 完了内容: 検証用 vault、API key policy、検証順を作成。Obsidian plugin install は判断待ち。

### 13. Obsidian MCP server 候補を比較する

- 出力先: `docs/condi-ref/obsidian-mcp-evaluation.md`
- 状態: done
- 候補: `cyanheads/obsidian-mcp-server`, `newtype-01/obsidian-mcp`, `PublikPrinciple/obsidian-mcp-rest`
- 理由: Codex / Claude / Gemini から vault を問合せる将来構成の候補。
- 完了内容: 初期比較表と評価基準、セキュリティ方針を作成。

### 14. VS Code MCP workspace 設定案を作る

- 出力先: `docs/condi-ref/vscode-mcp.md`
- 内容: `.vscode/mcp.json` の使い方、secret を直書きしない、Windows sandbox 不可の注意。
- 理由: VS Code が主入口で、workspace-local MCP は共有しやすい。
- 今できること: 設定サンプルを docs に書く。実ファイル追加は判断待ち。

### 15. Claude Code MCP project scope 案を作る

- 出力先: `docs/condi-ref/claude-mcp.md`
- 内容: `.mcp.json` の project scope、local/project/user precedence、API key を含めない方針。
- 理由: Claude Code を使う前提がある。
- 今できること: docs のみ。`.mcp.json` 実作成は判断待ち。

### 16. Gemini CLI MCP 案を作る

- 出力先: `docs/condi-ref/gemini-mcp.md`
- 内容: `mcpServers`、stdio / HTTP、`trust` は初期 true にしない。
- 理由: Gemini CLI を使う前提がある。
- 今できること: docs のみ。user config 変更は判断待ち。

### 17. knowledge index を作る

- 出力先: `docs/guide/index-policy.md` と将来の `docs/index.md`
- 内容: カテゴリ別 index、last reviewed、重要 topic、未整理 inbox。
- 理由: LLM に現在把握を聞くには index がある方が安定する。
- 今できること: index policy を書く。

### 18. inbox 運用を作る

- 出力先: `docs/guide/inbox-policy.md`
- 内容: すぐ整理できない情報の一時置き場、週次処理、恒久情報への昇格条件。
- 理由: 最初から完全分類しようとすると蓄積が止まる。
- 今できること: policy を作る。実フォルダ作成は判断待ち。

### 19. AI session summary 運用を作る

- 出力先: `docs/guide/ai-session-summary.md`
- 内容: Codex / Claude Code / Gemini CLI の会話から、決定、根拠、未決、次アクションだけ保存する。
- 理由: AIとの会話ログをそのまま保存すると検索ノイズが増える。
- 今できること: summary template を作る。

### 20. GitHub Issue / PR と vault の棲み分けを決める

- 出力先: `docs/guide/github-vault-boundary.md`
- 内容: active execution truth は GitHub、長期知識は vault、作業ログは `docs/imp/`。
- 理由: knowledge-ops の方針と合う。事実の二重管理を避ける。
- 今できること: boundary doc を作る。

### 21. 実運用ブログ由来のObsidianパターンを整理する

- 出力先: `docs/condi-ref/practical-obsidian-workflows.md`
- 状態: done
- 内容: daily notes、weekly review、Zettelkasten、MOC、AI maintenance、VS Code/Obsidian分業。
- 理由: 公式docsだけでは応用的な運用方法が薄かったため。
- 完了内容: 公式情報とは別枠で、試す案として整理。

### 22. SQLで再現可能にvaultを検索する方式を検討する

- 出力先: `docs/condi-ref/sql-queryable-vault.md`
- 状態: done
- 内容: Dataview、Query All The Things、SQLite FTS5、DuckDB FTSの比較。
- 理由: ユーザが「再現性のある検索結果の閲覧」と「SQLで内容を引く」可能性を確認したため。
- 完了内容: 初期推奨を外部SQLite/DuckDB index方式として整理。

## Suggested Next Execution Order

1. `docs/guide/vault-operation.md`
2. `docs/spec/note-frontmatter.md`
3. `docs/guide/query-protocol.md`
4. `docs/condi-ref/sync-strategy.md`
5. `docs/condi-ref/obsidian-mcp-evaluation.md`

この順番なら、Obsidian アプリや MCP をまだ入れなくても PJ 上で前進できる。

上記5件は 2026-04-12 に初回ドラフト作成済み。
## 2026-04-14 Update

`docs/imp/imp-wait.md` のユーザ回答を反映した。

新規作成済み:

- `docs/condi-ref/vscode-extensions.md`
- `docs/condi-ref/web-clipper.md`
- `docs/condi-ref/knowledge-category-options.md`
- `docs/guide/ai-session-summary.md`
- `docs/condi-ref/codex-obsidian-mcp-roadmap.md`

上記5件は 2026-04-14 に初回ドラフト作成済み。
次はカテゴリ体系のユーザ選択後に `knowledge/` などのObsidian側directoryを作るか、Codex + Obsidian MCP 検証用 vault の準備に進む。
