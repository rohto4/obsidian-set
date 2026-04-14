# Obsidian Sync Strategy

作成日: 2026-04-12

## 目的

Windows 版 Obsidian を中心に、将来のスマホ利用と Obsidian Sync 課金可能性を踏まえて、GitHub repo と同期手段の関係を整理する。

## 現時点の推奨

当面は GitHub repo を正本にする。
Obsidian Sync はスマホ利用や複数端末利用が現実になってから検討する。

理由:

- 現在は Git と PJ ノウハウ以外の知識蓄積がまだ少ない。
- VS Code + Codex / Claude Code / Gemini CLI が主入口。
- GitHub repo なら変更履歴、PR、AI agent 作業と相性がよい。
- Obsidian Sync と他 cloud storage の併用は conflict リスクがあるため、同期設計を決めてから使うべき。

## 何が実現できるか

- AIとユーザが同じGit管理下のMarkdownを見て作業できる。
- 変更履歴をcommit単位で追える。
- VS Code / Codex / Claude Code / Gemini CLI の作業結果を同じ場所に保存できる。
- Obsidian Syncを導入する前でも、PC上の知識ベースとして運用を始められる。

## 運用想定

1. PCでは `obsidian-set` repo を正本にする。
2. CodexなどAI agentはこのrepo内のMarkdownを編集する。
3. Obsidianは同じフォルダをvaultとして開き、閲覧・リンク・検索UIとして使う。
4. スマホ編集が必要になったら、Obsidian Syncの導入を再検討する。
5. Sync導入後もGitHubは履歴・AI作業・バックアップの役割を持つ。

## 導入メリット

- 最初から課金や複数端末同期に依存しない。
- AI作業と人間の作業をGit差分でレビューできる。
- Obsidian特有の設定にロックインしにくい。
- 後からSyncへ移行しやすい。

## Options

### Option A: GitHub repo を正本にする

- Windows / VS Code / AI agent との相性が最もよい。
- Git history で変更追跡できる。
- スマホ編集は弱い。
- 初期推奨。

### Option B: Obsidian Sync を正本にする

- Windows + スマホ + 将来の複数端末に強い。
- version history や selective sync など Obsidian 側の同期機能を使える。
- AI agent / GitHub PR との運用境界を設計する必要がある。
- 課金判断が必要。

### Option C: GitHub + Obsidian Sync 併用

- PCでは Git、スマホでは Sync という運用が可能。
- ただし二重同期・競合・履歴の分裂が起きやすい。
- 使うなら「GitHub はバックアップ」「Sync は端末同期」など役割を明確にする。

## Conflict Policy Draft

- 同じ note を複数端末で同時編集しない。
- AI agent 作業中は Obsidian mobile で同じファイルを編集しない。
- Sync 導入前に vault 全体を backup する。
- Git commit 前に `git status --short --branch` を確認する。
- conflict file が出たら自動解決しない。

## 保留事項

- スマホで実際に編集するか、閲覧だけか。
- Obsidian Sync に課金するか。
- GitHub repo を公開前提にするか、private 運用にするか。
- Obsidian plugin 設定を repo に含めるか。

## References

- https://help.obsidian.md/sync
- https://git-scm.com/docs
