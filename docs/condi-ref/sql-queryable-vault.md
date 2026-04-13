# SQL Queryable Vault

作成日: 2026-04-14

## 質問

Obsidianで保存したものに対して、SQLで内容を引っ張ってくるようなことは可能か。

## 短い回答

可能。
ただしObsidian標準機能としてSQLを直接提供するというより、次の3ルートになる。

1. Obsidian plugin の Dataview / Query All The Things を使う。
2. Markdown vault を外部の SQLite / DuckDB にindexしてSQLで問い合わせる。
3. Obsidian Local REST API / MCP で読み出し、別プロセスでindexを作る。

このPJで再現性を重視するなら、初期推奨は 2 の外部index方式。

## Option A: Dataview

Dataview はObsidian vault内のMarkdown metadataやinline fieldsを問い合わせる定番community plugin。
SQLではないが、table/list/taskなどのqueryで再現性のあるビューを作れる。

うれしいこと:

- Obsidian内で完結する。
- noteのfrontmatter、tag、taskを扱いやすい。
- Obsidian UIで閲覧しやすい。

弱いところ:

- SQLそのものではない。
- Obsidian plugin依存。
- 再現性はvault + plugin + query blockに依存する。

使いどころ:

- Obsidian上のダッシュボード。
- task一覧、source note一覧、review_after一覧。

## Option B: Query All The Things

Query All The Things は、Obsidian APIやDataview由来のdata collectionに対してSQL-based queryを実行できるcommunity plugin。

うれしいこと:

- Obsidian内でSQL風に問い合わせられる。
- Dataviewと連携した高度な抽出に向く。

弱いところ:

- plugin依存が強い。
- このPJの初期段階では過剰。
- 保守状況とplugin権限を確認してから採用したい。

使いどころ:

- Obsidian UI内でSQL的な表を出したい場合。

## Option C: SQLite FTS5 external index

Markdown filesをスクリプトで読み、frontmatterと本文をSQLiteへ入れ、FTS5で全文検索する方式。

うれしいこと:

- SQLで問い合わせられる。
- 再現性が高い。index生成スクリプトとDB schemaをGit管理できる。
- Obsidian pluginに依存しない。
- Codex / Claude Code / Gemini CLI からCLIで使いやすい。

弱いところ:

- index生成スクリプトが必要。
- Obsidian UI内で直接動くわけではない。
- 日本語全文検索のtokenize方針を別途検討する必要がある。

使いどころ:

- 「このvaultをSQLで検索する」再現性重視の運用。
- AI agentに同じSQLを再実行させたい場合。

## Option D: DuckDB external index

DuckDB にMarkdown metadata / bodyを入れ、DuckDBのSQLで問い合わせる方式。
DuckDBにはfull-text search extensionもある。

うれしいこと:

- 単体ファイルDBで扱いやすい。
- CSV / Parquet / JSONなどとの連携が強い。
- 分析クエリが書きやすい。

弱いところ:

- FTS extensionの扱い、導入方法、環境差を確認する必要がある。
- SQLiteより標準搭載感は弱い場合がある。

使いどころ:

- noteだけでなく、ログ、CSV、export、metadataをまとめて分析する場合。

## 初期推奨

このPJでは次の順で検証する。

1. まず frontmatter schema を安定させる。
2. `docs/condi-ref/sql-queryable-vault.md` でDB schema案を書く。
3. SQLite FTS5 indexerを検討する。
4. 必要ならDuckDB版も比較する。
5. Obsidian UI内で必要になったらDataviewを検討する。

## Schema案

```sql
CREATE TABLE notes (
  path TEXT PRIMARY KEY,
  title TEXT,
  type TEXT,
  status TEXT,
  topic TEXT,
  tags TEXT,
  source TEXT,
  created TEXT,
  updated TEXT,
  confidence TEXT,
  review_after TEXT,
  body TEXT,
  mtime TEXT
);

CREATE VIRTUAL TABLE notes_fts
USING fts5(path UNINDEXED, title, body, topic, tags, content='notes', content_rowid='rowid');
```

注意:

- 上記は案。SQLite FTS5 のcontent table連携は実装時に検証する。
- `topic`, `tags`, `source` はJSON textとして保存するか、別tableに正規化するかを後で決める。

## Example Queries

```sql
-- AI関連のactive note
SELECT path, title, updated
FROM notes
WHERE status = 'active'
  AND topic LIKE '%ai%'
ORDER BY updated DESC;

-- review期限切れ
SELECT path, title, review_after
FROM notes
WHERE review_after IS NOT NULL
  AND review_after <= date('now')
ORDER BY review_after ASC;

-- 全文検索
SELECT n.path, n.title
FROM notes_fts f
JOIN notes n ON n.path = f.path
WHERE notes_fts MATCH 'MCP';
```

## References

- Obsidian Vault API: https://docs.obsidian.md/Plugins/Vault
- Dataview plugin overview: https://www.obsidianstats.com/plugins/dataview
- Query All The Things plugin overview: https://www.obsidianstats.com/plugins/qatt
- DuckDB full text search: https://duckdb.org/docs/stable/core_extensions/full_text_search.html
- SQLite FTS5: https://www.sqlite.org/fts5.html

