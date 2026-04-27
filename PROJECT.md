# obsidian-set Project Context

## 目的

この PJ は Obsidian vault / knowledge base 的に扱う。
主な用途は、調査、知識整理、文章化、運用メモの蓄積。

## 優先度モデル

1. `AGENTS.md`
   - 全 tool 共通の最上位ルール。
2. `PROJECT.md`
   - この PJ の目的、情報配置、運用方針。
3. `docs/guide/`
   - 恒久的な運用ガイド、判断基準、ルール補足。
4. `docs/spec/`
   - 実装対象として確定した仕様、要件、設計前提。
5. `docs/condi-ref/`
   - 条件付き参考資料、実現可能性確認、候補比較、未採用の選択肢。
6. `docs/imp/`
   - 実装メモ、作業記録、進捗。
7. `.agents/skills/`
   - ECC 由来の作業別 workflow。該当作業の時だけ読む。
8. `commands/`
   - ECC / ecc-expand 由来の試用 command。該当 command を使う時だけ読む。
9. `docs/memo.md`
   - 初回依頼などの生メモ。恒久ルールの正本にはしない。

## ECC から取り込んだ skill

`G:\devwork\obsidian-set\.agents\skills` に実体をコピー済み。
外部の ECC clone を実運用で参照する構成ではない。

- `knowledge-ops`: Obsidian / KB / local docs の整理、保存、検索、重複排除。
- `research-ops`: 調査タスクの入口。証拠、推論、提案を分ける。
- `deep-research`: 複数ソースの深い調査。
- `exa-search`: Web / code / company などの探索補助。
- `market-research`: 比較、評価、推薦。
- `article-writing`: メモや調査結果から長文を書く。
- `brand-voice`: 文体や声の抽出。
- `content-engine`: 複数媒体向けの文章展開。
- `tdd-workflow`: 実装タスクをテスト先行で進める workflow。試用導入。
- `verification-loop`: 実装後の検証ループ。試用導入。
- `genshijin`: 短文圧縮回答モード。ユーザ指定時だけ使う。

## 試用導入した command

`commands/` に ECC / ecc-expand 由来の command を必要分だけ置く。

- `expand-answer`: 短い一次回答を必要時だけ詳しく展開する。
- `prp-plan`: 実装候補を詳細な計画ファイルに落とす。
- `prp-implement`: 計画ファイルを段階的に実行する。
- `prp-prd`: 大きめの要望を PRD / phase に分解する。

## 運用ルール

- ルールを増やす時は `AGENTS.md` に詰め込まず、原則 `PROJECT.md` か `docs/guide/` に分ける。
- 作業の一次記録は `docs/imp/` に置く。
- 実装対象として確定した仕様は `docs/spec/` に置く。
- まだ採用未確定の調査、候補比較、実現可能性確認は `docs/condi-ref/` に置く。
- 一時メモを恒久ルールに昇格する時は、`docs/memo.txt` から該当箇所を整理して移す。
- `docs/` 配下の構成を変更した時は、`docs/README.md` を更新する。
- `docs/condi-ref/` のファイルを追加・削除・大きく変更した時は、`docs/condi-ref/condi-ref-summary.md` を更新する。
- `docs/guide/` のファイルを追加・削除・大きく変更した時は、`docs/guide/guide-summary.md` を更新する。
- `docs/spec/` のファイルを追加・削除・大きく変更した時は、`docs/spec/spec-summary.md` を更新する。
- ECC skill を追加する時は、必要な skill だけ `.agents/skills/` にコピーし、`docs/ecc-obsidian-setup.md` とこの `PROJECT.md` を更新する。
- command を追加する時は、必要な command だけ `commands/` にコピーし、`docs/ecc-obsidian-setup.md` とこの `PROJECT.md` を更新する。
