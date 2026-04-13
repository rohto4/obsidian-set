# obsidian-set Agent Instructions

## 最優先ルール

1. 日本語で対応する。
2. UTF-8 で読み書きする。
3. 質問と回答は連番を振り、ユーザとのやり取りを確実にする。
4. この PJ は ECC 導入前提で扱う。
5. ただし、この `AGENTS.md` と `PROJECT.md` は ECC 由来の一般ルールより優先する。

## 読み込み順

1. `AGENTS.md`
   - 全 agent / tool 共通の最上位ルール。
2. `PROJECT.md`
   - PJ 固有の目的、情報配置、運用方針。
3. `docs/ecc-obsidian-setup.md`
   - ECC をこの PJ にどう取り込んだかの運用メモ。
4. 必要な `.agents/skills/*/SKILL.md`
   - 作業内容に応じて読む。常時すべてを読まない。

## 恒久情報の置き場所

- ECC や `AGENTS.md` 以外の恒久ルール: `docs/guide/`
- 実装対象として確定した仕様: `docs/spec/`
- 条件付き参考資料、実現可能性確認、候補比較: `docs/condi-ref/`
- 実装内容: `docs/imp/imp-*`
- 進捗状況: `docs/imp/*-status.md`

## ECC の扱い

- ECC は `.agents/skills/` にコピー済みの skill を優先して使う。
- ECC repo 全体、`commands/`、`hooks/`、`.codex/config.toml` はこの PJ には未導入。
- Claude / Gemini / Codex などツール別ファイルは、共通ルールを複製せず、このファイルと `PROJECT.md` へ誘導する。
