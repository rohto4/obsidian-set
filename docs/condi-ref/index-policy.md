# Index Policy Evaluation

作成日: 2026-04-14

## 目的

knowledge indexを作るべきか、`source-backed-notes` と役割がぶつからないかを評価する。
現時点ではguideへ昇格しない。

## 何が実現できるか

- LLMに「このカテゴリを今どう把握しているか」と聞く時の入口を作れる。
- カテゴリごとの主要note、last reviewed、未整理noteを一覧できる。
- vault全体を毎回読ませずに、確認対象を絞れる。

## source-backed-notes との違い

`source-backed-notes` は根拠資料noteの形式を定義する。
`index-policy` は根拠本文や要約を書かず、関連noteへのリンクとレビュー状態だけを扱う。

同じ情報を重複して書くと更新漏れが起きるため、indexは目次として使い、事実や解釈の正本にはしない。

## 運用想定

1. 最初はカテゴリindexを作りすぎない。
2. noteが増えて探しにくくなったカテゴリだけindexを作る。
3. indexにはリンク、短い説明、last reviewed、open questionsだけを書く。
4. source factsやlocal interpretationは元noteに置く。

## 暫定判断

採用候補。
ただし、`source-backed-notes` と重複しない目次専用ルールとして設計できる場合に限る。
