# Practical Obsidian Workflow Patterns

作成日: 2026-04-14

## 目的

公式docsだけでは分からない、個人・実運用ブログ由来のObsidian運用パターンを整理する。
公式情報は機能確認の正本、個人ブログは運用案の材料として扱う。

## 追加調査した応用パターン

### 1. Daily notes as intake layer

日次ノートを単なる日記ではなく、アイデア、会議、タスク、観察の入口にする運用。

うれしいこと:

- 最初に分類しなくてよい。
- 今日の作業・発見・未決が1箇所に集まる。
- 週次レビューで恒久noteへ昇格できる。

このPJへの適用:

- AI会話のユーザプロンプト全文保存と相性がよい。
- ただし、最初からdaily directoryを作るかは未決。`docs/imp/` とObsidian側分類を分ける。

### 2. Weekly review as knowledge distillation

日次ノートを貯めっぱなしにせず、週次で見直して永久note、decision、source-backed noteへ変換する運用。

うれしいこと:

- AI会話ログや調査メモが書き捨てにならない。
- 未完了タスク、未決、再調査点を拾える。
- LLMに「今どう把握しているか」を聞く時の材料が整理される。

このPJへの適用:

- `docs/imp/agents-tasks-status.md` と `docs/imp/imp-wait.md` を週次レビュー対象にする。

### 3. Zettelkasten minimal folders

Zettelkasten系の記事では、最初のフォルダを少なくし、Inbox / Literature Notes / Permanent Notes / Templates などの最小構成から始める案がある。

うれしいこと:

- 分類の迷いが少ない。
- source note と permanent note を分けやすい。
- リンク中心で知識を育てられる。

このPJへの適用:

- `knowledge/` を作るなら、`inbox`, `sources`, `permanent`, `templates` のような最小構成が候補。
- ただしユーザ要望ではカテゴリ候補を比較したいので、現時点では `docs/spec/knowledge-category-options.md` の判断待ち。

### 4. Claim-style permanent notes

永久noteのタイトルを単なるラベルではなく、主張や1アイデアとして書く運用。

例:

- 悪い: `MCP`
- 良い: `MCP write tools should be tested in a disposable vault first`

うれしいこと:

- LLMがnoteの意味を把握しやすい。
- リンクした時に文脈が残る。
- あとからMOCを作りやすい。

このPJへの適用:

- `docs/spec/note-frontmatter.md` のnoteルールに追加候補。

### 5. MOC should emerge later

Map of Content は最初から作りすぎず、関連noteが増えて探しにくくなった時に作るという運用。

うれしいこと:

- 構造の作りすぎを避けられる。
- 実際に増えた知識クラスタからindexを作れる。

このPJへの適用:

- `knowledge/index/` を最初から大量に作らない。
- 最初は `docs/spec/knowledge-category-options.md` の候補だけに留める。

### 6. AI maintenance prompts

AIに vault を読ませ、孤立note、古いMOC、未処理Inbox、重複アイデアを発見させる運用。

うれしいこと:

- 人間が見落としやすい構造劣化を検出できる。
- MCP / Local REST API / Codex と相性がよい。
- 「全部許可」のMCP方針を使うなら、最終的にリンク追加や整理も自動化できる。

このPJへの適用:

- 最初は read/search/list で監査だけ。
- その後 create/append、最後に update/delete。

### 7. VS Code as Markdown editor, Obsidian as knowledge UI

VS CodeでMarkdownを編集し、Obsidianでリンク、グラフ、閲覧、モバイル連携を使う分業。

うれしいこと:

- 普段のCodex / Claude Code / Gemini CLI作業と同じ場所で編集できる。
- Git差分を見やすい。
- Obsidian固有UIへの依存を減らせる。

このPJへの適用:

- 現在の方針と一致。`docs/spec/vscode-extensions.md` で Markdown All in One と markdownlint を初期候補にしている。

## このPJへの追加候補タスク

1. `docs/guide/weekly-review.md` を作る。
2. `docs/guide/daily-capture.md` を作る。
3. `docs/spec/knowledge-category-options.md` に Zettelkasten minimal folders 案を統合する。
4. `docs/spec/note-frontmatter.md` に claim-style permanent note のルールを追加する。
5. `docs/guide/ai-maintenance-prompts.md` を作る。

## References

- PARAZETTEL daily workflows: https://parazettel.com/articles/obsidian-daily-workflows/
- Daily notes workflow: https://aiproductivity.ai/guides/obsidian-daily-notes-workflow/
- Zettelkasten in Obsidian with AI maintenance: https://desktopcommander.app/blog/zettelkasten-obsidian/
- VS Code as Obsidian-like notes editor: https://www.xda-developers.com/tried-using-vs-code-obsidian-notes/

