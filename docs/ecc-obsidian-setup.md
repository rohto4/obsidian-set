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
- `commands/`: 旧 slash command 互換面。Codex PJ では優先度を下げる。ただし 2026-04-17 に必要な command だけ試用導入した。
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
- `tdd-workflow`
- `verification-loop`

コピー済みの skill 本体は `obsidian-set` 配下にあり、実運用時に外部の ECC clone を参照する構成ではない。

選定理由:

- `knowledge-ops`: Obsidian / KB / local docs の整理、保存、重複排除、検索方針に合う。
- `research-ops`, `deep-research`, `exa-search`, `market-research`: 現在情報の調査、比較、根拠付き整理に使う。
- `article-writing`, `brand-voice`, `content-engine`: Obsidian 内のメモや調査結果を記事、投稿、長文メモへ展開する用途に使う。
- `tdd-workflow`, `verification-loop`: 実装候補の詳細化や実装検証 workflow を試すために追加導入した。ECC の PRP command 系とは別で、skill として存在する範囲を先に使う。

## 今回コピーしなかったもの

以下はあえて入れていない。

- ECC repo 全体
  - Obsidian PJ には過剰。テスト、installer、CI、複数 harness 用 surface まで混ざる。
- `.codex/config.toml`
  - Windows では `terminal-notifier` がそのまま使えない。
  - `npx` 起動の MCP が複数入るため、必要なタイミングで個別に設計した方がよい。
- `commands/` 全体
  - ECC では legacy slash-entry 互換面。Codex では skill 優先。2026-04-17 時点では全体ではなく `expand-answer`, `prp-plan`, `prp-implement`, `prp-prd` だけを試用導入した。
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
- command は必要なものだけ `commands/` に取り込む。
- 調査結果や運用メモは `docs/` 配下に UTF-8 Markdown で残す。
- ECC 元 repository を更新したら、必要な skill だけ再コピーする。

必要になったら追加候補:

- `strategic-compact`: 長い調査や会話の圧縮方針が必要になった場合。
- `verification-loop`: Obsidian vault 内で scripts や tooling を追加し、検証ループが必要になった場合。
- `document-processing`: PDF / DOCX などの変換や抽出ワークフローが必要になった場合。ただし現状の ECC 側 skill は用途特化が強いので、追加前に中身を確認する。

## 未導入 ECC 要素の意図とできること

この PJ では、ECC の便利な要素を全部入れるのではなく、Obsidian vault / knowledge base として実際に使うものだけを薄く取り込む方針にしている。

現状は `AGENTS.md` と `PROJECT.md` を正本にし、ECC からは `.agents/skills/` だけを作業別 workflow として使う。つまり、この PJ は「ECC 由来の作業手順を使う」が、「ECC の実行基盤を丸ごと常駐させる」状態ではない。

### ECC repo 全体を入れない意図

ECC repo 全体には、複数 agent harness 向けの設定、installer、tests、rules、commands、hooks、MCP 設定、Claude / Codex / Gemini / Cursor / OpenCode 向けの面がまとめて入っている。

この PJ は Obsidian vault / knowledge base 用なので、全部入れると次の問題が出る。

- Obsidian 運用に不要なファイルが大量に増える。
- Claude Code 前提、macOS 前提、Node/npm 前提の仕組みが混ざる。
- どのルールが正本か分かりにくくなる。
- `AGENTS.md` / `PROJECT.md` / `docs/guide/` の運用と、ECC 側 rules が二重管理になる。
- Codex / Claude / Gemini を併用する前提なのに、特定 harness 向け設定が強く出る。

そのため、現時点では「必要な skill だけコピー」が合理的。

### `commands/` があるとできること

ECC の `commands/` は、主に slash command 的な作業入口。

ECC clone には、例えば次のような command がある。

- `/plan`: 要件整理、リスク確認、実装計画を作って、確認を待つ。
- `/tdd`: TDD 的に進める。
- `/code-review`: レビュー観点で確認する。
- `/build-fix`: build エラー修正に寄せて動く。
- `/verify`: 検証ループを回す。
- `/update-docs`: docs 更新を促す。
- `/hookify`: 会話や操作から hook ルールを作る。
- `/save-session` / `/resume-session`: セッション保存・再開系。
- 言語別の `go-test`、`rust-review`、`python-review` など。

`commands/` があると、毎回プロンプトで細かく頼まなくても、定型作業をコマンド名で起動できる。

ただし、これは Claude Code 系の slash command 互換面が中心。Codex では `AGENTS.md` と skill の方が自然に効くため、この PJ では優先度を下げている。

### `hooks/` があるとできること

ECC の `hooks/` は、Claude Code の tool 実行前後に自動で走るイベント処理。

主なイベントは次の通り。

- `PreToolUse`: tool 実行前に動く。危険ならブロックできる。
- `PostToolUse`: tool 実行後に動く。結果を見て警告や分析ができる。
- `Stop`: agent の応答後に動く。
- `SessionStart` / `SessionEnd`: セッション開始・終了時に動く。
- `PreCompact`: context 圧縮前に状態保存する。

導入すると、例えば次ができる。

- `git commit --no-verify` をブロックする。
- 長時間コマンドは tmux で動かすよう促す。
- `git push` 前に確認を促す。
- commit 前に lint、commit message、secret、`console.log` などを検査する。
- Markdown / txt の作成場所がルール外なら警告する。
- 編集後に品質チェック、format、TypeScript check を走らせる。
- セッション終了時に作業状態を保存する。
- 応答後にデスクトップ通知を出す。
- context 圧縮前に状態を退避する。

これは強力だが、この PJ では未導入でよい理由がある。

- Claude Code の hook system 前提が強い。
- `CLAUDE_PLUGIN_ROOT` など Claude plugin 前提の環境変数が出てくる。
- Node script と一部 Bash wrapper が必要。
- macOS / WSL 通知や tmux 前提の hook が含まれる。
- Windows + Codex + Obsidian vault では、そのまま動かすより選別が必要。
- 自動ブロック系は便利だが、知識整理 PJ では過剰になりやすい。

この PJ で採用するなら、丸ごとではなく「Markdown 配置警告」「セッション要約保存」「secret 検出」など、Obsidian 運用に合うものだけを個別移植するのが現実的。

### `.codex/config.toml` があるとできること

ECC clone の `.codex/config.toml` は、Codex 用の参考設定。

主に次を設定できる。

- `approval_policy`
- `sandbox_mode`
- `web_search`
- `notify`
- `persistent_instructions`
- MCP server 設定
- Codex multi-agent 設定
- profile 切り替え
- agent role 定義

導入すると、例えば次ができる。

- この PJ 用に Codex の sandbox / approval / web search の既定値を設定する。
- GitHub、Context7、Exa、Memory、Playwright、Sequential Thinking などの MCP server を Codex から使えるようにする。
- `strict` / `yolo` のような profile を切り替えられる。
- explorer / reviewer / docs researcher のような sub-agent 設定を定義できる。
- タスク完了時に通知を出す。
- 毎回の prompt に persistent instruction を追加できる。

ただし、ECC の設定をそのまま入れない判断には理由がある。

- `notify` が `terminal-notifier` で、これは macOS 前提。
- MCP が `npx` 起動中心で、初回起動や更新時にネットワーク・Node 環境へ依存する。
- GitHub / Exa などは credentials の扱いを別途決める必要がある。
- Obsidian PJ に最初から多数の MCP を入れると、何が必要で何が不要か分かりにくくなる。
- Codex の実行設定はセッション側からも制御されるため、PJ-local config を置けば必ず現在の実行条件が変わる、とは限らない。

### 現時点の判断

現状の未導入方針は、「ECC の知識・作業手順は使うが、自動実行・強制・外部連携の層はまだ入れない」という判断。

導入するとできることは増える。

- `commands/`: 定型作業を slash command 化できる。
- `hooks/`: tool 実行前後に品質チェック、警告、ブロック、状態保存を自動化できる。
- `.codex/config.toml`: Codex の project-local 設定、MCP、profile、multi-agent を定義できる。

ただし、この PJ ではまず `.agents/skills/` と `docs/` 運用を正本にして、必要性が出たものだけ追加する。

特に最初に検討価値があるのは、次の方向。

- `commands/` 丸ごとではなく、Obsidian 運用向け command 相当の手順を `docs/guide/` か skill に落とす。
- `hooks/` 丸ごとではなく、Markdown 配置・セッション要約・secret 検出だけを選ぶ。
- `.codex/config.toml` 丸ごとではなく、必要な MCP だけ個別に設計する。

commands 化する場合の追加候補:

- `detail-answer`: 通常は短く回答し、ユーザが詳しい説明・比較・追記を求めた時だけ長めに展開するための入口。

## 2026-04-17 command 試用導入

`ecc-expand` 経由で次の command をこの PJ の `commands/` に導入した。

- `expand-answer`
- `prp-plan`
- `prp-implement`
- `prp-prd`

目的:

- `expand-answer`: 通常回答を短く保ち、必要時だけ詳細化する。
- `prp-plan`: 実装候補や運用候補を、調査済みの計画ファイルへ落とす。
- `prp-implement`: 計画ファイルを順に実行し、検証結果を残す。
- `prp-prd`: 大きいテーマを PRD / phase に分解する。

注意:

- ECC の command は `.claude/PRPs/` 前提を含むため、この PJ ではまず試用扱いにする。
- Obsidian 運用に合うことが分かったら、`ecc-expand` 側で docs / vault 向けに調整する。
