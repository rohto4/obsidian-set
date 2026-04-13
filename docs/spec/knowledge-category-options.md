# Knowledge Category Options

作成日: 2026-04-14

## 目的

Obsidian側の保存体系候補を整理する。
`docs/guide`, `docs/spec`, `docs/imp` はPJ設計書類の分類であり、Obsidianの知識カテゴリとは別に考える。

## Option 1: 用途別

```text
knowledge/
  dev/
  ai/
  tools/
  sources/
  inbox/
```

向いている場合:

- 最初に小さく始めたい。
- AIと開発ノウハウが主目的。

欠点:

- 後からカテゴリが肥大化しやすい。

## Option 2: 信頼度・状態別

```text
knowledge/
  inbox/
  sources/
  synthesized/
  decided/
  deprecated/
```

向いている場合:

- source-backed noteを重視したい。
- LLM回答で根拠と推論を分けたい。

欠点:

- 人間が探す時にtopic別ではないため慣れが必要。

## Option 3: PARA寄り

```text
knowledge/
  projects/
  areas/
  resources/
  archives/
  inbox/
```

向いている場合:

- Obsidianを長期の個人知識管理に広げたい。

欠点:

- 開発PJと混ざると「どれが実行中か」が曖昧になりやすい。

## Option 4: AI問い合わせ最適化

```text
knowledge/
  index/
  dev/
  ai/
  source-notes/
  summaries/
  prompts/
  decisions/
```

向いている場合:

- 「このカテゴリを今どう把握しているか」をLLMに聞く用途を重視する。
- ユーザプロンプト全文保存、AI出力要約保存と相性がよい。

欠点:

- 最初から少し構造が多い。

## Option 5: 時系列 + topic

```text
knowledge/
  daily/
  weekly/
  topics/
  sources/
  decisions/
```

向いている場合:

- 日々の作業ログから知識を抽出する運用。

欠点:

- 整理をサボるとdailyに情報が埋もれる。

## 初期おすすめ

Option 4 の縮小版。

```text
knowledge/
  index/
  dev/
  ai/
  sources/
  prompts/
  decisions/
  inbox/
```

理由:

- 開発ノウハウとAI知識の両方に対応できる。
- ユーザプロンプト全文保存の方針を `prompts/` に分離できる。
- LLM問い合わせ時に `index/` と `decisions/` が効く。
- `sources/` で根拠を分けられる。

## 次アクション

1. ユーザにOption 1-5から選んでもらう。
2. 選定後、directoryを作る。
3. `docs/spec/note-frontmatter.md` と整合させる。

