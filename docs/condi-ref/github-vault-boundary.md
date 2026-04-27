# GitHub Vault Boundary

作成日: 2026-04-14
更新日: 2026-04-19

## 目的

`G:\devwork` 配下の各開発PJ GitHub と、`G:\knowledge-vault` の責務を分ける。

## 結論

- 各開発PJ: GitHub repo 化してよい。
- `G:\knowledge-vault`: 初期 GitHub repo 化しない。
- vault backup: `H:\bk\knowledge-vault-snapshots\` へ日付付き snapshot。

## 正本

| 情報 | 正本 |
|---|---|
| 実装状態、Issue、PR | 各開発PJ GitHub |
| 横断ナレッジ | `G:\knowledge-vault\knowledge\` |
| LLM記憶 | `G:\knowledge-vault\memory\` |
| 作業記録、引き継ぎ | `G:\knowledge-vault\tasks\` |
| 根拠資料 | `G:\knowledge-vault\sources\` |
| AI会話要約 | `G:\knowledge-vault\prompts\` |

## 重複回避

- GitHubとvaultに同じ本文を持たない。
- GitHub側が正本なら、vaultにはリンクと短い要約だけ。
- vault側が正本なら、GitHubには実行に必要な範囲だけ。
- `memory/` はどちらの正本にもせず、想起入口にする。

