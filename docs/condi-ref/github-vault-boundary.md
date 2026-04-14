# GitHub Vault Boundary Evaluation

作成日: 2026-04-14

## 目的

GitHub Issue / PR、Obsidian vault、`docs/imp/` のどこに何を置くかを整理し、同じ情報の重複管理を避ける。
現時点では要検討のため、guideへ昇格しない。

## 重複しやすいポイント

1. タスク状態
2. 導入判断
3. 調査根拠
4. AI会話要約
5. 設定値
6. 外部URL
7. 実装手順

## 暫定の置き場

| 情報 | 暫定正本 | 理由 |
|---|---|---|
| 実行中タスク | `docs/imp/` | このPJ内でAIがすぐ読める |
| GitHubに紐づく実装状態 | GitHub Issue / PR | active execution truthとして扱いやすい |
| 長期知識 | vault / `docs/guide/` | LLM問い合わせや再利用に向く |
| 条件付き調査 | `docs/condi-ref/` | 採用前の比較・検証を置ける |
| 確定仕様 | `docs/spec/` | 実装対象として扱う |

## 運用想定

- 同じ判断をGitHubとvaultの両方で本文管理しない。
- GitHubに置く場合、vault側にはリンクと短い要約だけ置く。
- vaultに置く場合、GitHub側には実行タスクとして必要な範囲だけ書く。
- AI会話の全文は肥大化しやすいため、ユーザプロンプト全文とAI出力要約の保存ルールに従う。

## 暫定判断

必要。
ただしvaultの特徴とGitHub運用の実態がまだ固まっていないため、先に重複ポイントを洗い出してからguideへ昇格する。
