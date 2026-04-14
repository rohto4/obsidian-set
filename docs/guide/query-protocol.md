# Query Protocol

作成日: 2026-04-12

## 目的

Obsidian / Markdown vault を通して LLM に「特定カテゴリを今どう把握しているか」を問い合わせるための回答形式を定義する。

## 使う場面

- 「MCPについて今どう把握しているか」のように、カテゴリ単位でLLMに聞く時。
- 回答に根拠、PJ方針、推論、判断待ち、次アクションを分けたい時。
- `docs/guide/`、`docs/spec/`、`docs/condi-ref/`、`docs/imp/` のどこを読ませるべきか迷う時。

## 重複管理を避ける方針

このファイルは問い合わせ時の出力形式だけを扱う。
source noteの保存形式は `docs/guide/source-backed-notes.md`、全体運用は `docs/guide/vault-operation.md` を正本にする。

## 基本質問テンプレート

```text
この vault を前提に、<カテゴリ> について今どう把握しているか整理してください。
回答は以下に分けてください。

1. 確認済みの事実
2. このPJでの現行方針
3. 推論
4. 判断待ち
5. 次に進められる作業
6. 再調査が必要な点
```

## 読み込み順

1. `AGENTS.md`
2. `PROJECT.md`
3. 関連する `docs/guide/*.md`
4. 関連する `docs/spec/*.md`
5. 関連する `docs/condi-ref/*.md`
6. `docs/imp/imp-wait.md`
7. 必要な `.agents/skills/*/SKILL.md`

## 出力形式

```text
QUESTION
- 対象カテゴリ:

SOURCED FACTS
- 参照元つきの事実:

PROJECT STATE
- このPJで決まっていること:

INFERENCE
- 事実からの推論:

WAITING DECISIONS
- ユーザ判断待ち:

NEXT TASKS
- 今進められること:

RESEARCH NEEDED
- 最新確認が必要なこと:
```

## Evidence Rules

- 公式 docs、repo 内 docs、ユーザ発言、推論を混ぜない。
- 日付に依存する情報は絶対日付を付ける。
- Web 由来の情報は URL を残す。
- source が不明な情報は `推論` か `未確認` として扱う。

## Example Prompt

```text
この vault を前提に、Obsidian MCP 連携について今どう把握しているか整理してください。
公式情報、community plugin情報、このPJでの判断待ち、次に進める作業を分けてください。
```
