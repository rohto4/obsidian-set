# ECC 導入メモ for obsidian-set

作成日: 2026-04-12

## PJ 前提

`AGENTS.md` を先に確認した結果、この PJ では次を優先する。

- 日本語で対応する
- UTF-8 で読み書きする
- ECC 導入前提で対応する
- ただし、この PJ の `AGENTS.md` は ECC 側の一般ルールより優先する

現在の正本構成:

- `AGENTS.md`: 全 agent / tool 共通の最上位ルール
- `PROJECT.md`: PJ 固有の目的、情報配置、運用方針
- `CLAUDE.md`: Claude Code 用の薄い入口。共通ルールは複製しない
- `GEMINI.md`: Gemini 用の薄い入口。共通ルールは複製しない
- `.agents/skills/`: ECC 由来の作業別 workflow。該当作業の時だけ読む

## 読んだ ECC 情報

確認元:

- GitHub: `https://github.com/affaan-m/everything-claude-code`
- ローカル clone。コピー元としてだけ利用し、実運用では参照しない。

ECC は Claude Code 専用の設定集ではなく、Codex / Cursor / OpenCode / Gemini など複数の AI agent harness 向けの performance / workflow system として構成されている。

重要な構成:

- `skills/`: 現行の主導線。再利用できる作業手順、判断基準、ドメイン知識。
- `.agents/skills/`: Codex など agent harness 向けに使いやすく整えられた skill 面。
- `commands/`: 旧 slash command 互換面。Codex PJ では優先度を下げる。
- `hooks/`: Claude / Cursor / OpenCode など向けの hook 実行面。Codex ではそのまま使う前提にしない。
- `.codex/`: Codex 用の参考設定。ただし clone 側の `config.toml` は MCP を `npx` で起動し、macOS の `terminal-notifier` も含むため、この Windows の Obsidian PJ にはそのままコピーしない。

## 今回コピーしたもの

Obsidian vault 的な用途を想定し、知識管理、調査、文章化に関係する skill だけをコピーした。

コピー先:

`G:\devwork\obsidian-set\.agents\skills`

コピーした skill:

- `article-writing`
- `brand-voice`
- `content-engine`
- `deep-research`
- `exa-search`
- `knowledge-ops`
- `market-research`
- `research-ops`

コピー済みの skill 本体は `obsidian-set` 配下にあり、実運用時に外部の ECC clone を参照する構成ではない。

選定理由:

- `knowledge-ops`: Obsidian / KB / local docs の整理、保存、重複排除、検索方針に合う。
- `research-ops`, `deep-research`, `exa-search`, `market-research`: 現在情報の調査、比較、根拠付き整理に使う。
- `article-writing`, `brand-voice`, `content-engine`: Obsidian 内のメモや調査結果を記事、投稿、長文メモへ展開する用途に使う。

## 今回コピーしなかったもの

以下はあえて入れていない。

- ECC repo 全体
  - Obsidian PJ には過剰。テスト、installer、CI、複数 harness 用 surface まで混ざる。
- `.codex/config.toml`
  - Windows では `terminal-notifier` がそのまま使えない。
  - `npx` 起動の MCP が複数入るため、必要なタイミングで個別に設計した方がよい。
- `commands/`
  - ECC では legacy slash-entry 互換面。Codex では skill 優先。
- `hooks/`
  - Codex は Claude Code と同じ hook 前提ではないため、この PJ に直接入れない。
- `rules/`
  - clone 側 manifest では `rules-core` が Codex target に含まれていない。Codex では `AGENTS.md` と skill の方を優先する。
- `mcp-configs/`
  - 使う MCP が決まってから個別導入する。Obsidian PJ では最初から全部は不要。

## フル導入を検討する場合

ECC の installer は Codex target の場合、project root ではなく原則 `%USERPROFILE%\.codex` を対象にする。
この PJ 配下へ直接すべてを入れる用途ではない。

dry run で確認するなら、ECC の元 repository 側で依存を入れてから実行する。

```powershell
cd <ECC の clone 先>
npm install --no-audit --no-fund
.\install.ps1 --target codex --profile research --dry-run
```

注意:

- `npm install` はネットワークアクセスを使う。
- 実インストール前に `--dry-run` のコピー先を確認する。
- `%USERPROFILE%\.codex` に入れるのか、この Obsidian PJ だけに限定するのかを分けて判断する。

## 今後の運用

基本方針:

- この PJ では `AGENTS.md` を最上位ルールにする。
- PJ 固有の階層や情報配置は `PROJECT.md` に置く。
- Claude / Gemini など tool 別入口には共通ルールを複製せず、`AGENTS.md` と `PROJECT.md` へ誘導する。
- ECC は必要 skill だけをローカル PJ に取り込む。
- 調査結果や運用メモは `docs/` 配下に UTF-8 Markdown で残す。
- ECC 元 repository を更新したら、必要な skill だけ再コピーする。

必要になったら追加候補:

- `strategic-compact`: 長い調査や会話の圧縮方針が必要になった場合。
- `verification-loop`: Obsidian vault 内で scripts や tooling を追加し、検証ループが必要になった場合。
- `document-processing`: PDF / DOCX などの変換や抽出ワークフローが必要になった場合。ただし現状の ECC 側 skill は用途特化が強いので、追加前に中身を確認する。
