# VS Code Extensions Evaluation

作成日: 2026-04-14

## 結論

初期おすすめは次の2つ。

1. Markdown All in One
2. markdownlint

Foam と MLink は、Obsidian と役割が重なるため、今すぐ導入せず評価対象に残す。

## 採用候補

| Extension | 何がうれしいか | 懸念 | 初期判断 |
|---|---|---|---|
| Markdown All in One | Markdown編集、ショートカット、TOC、list編集、preview補助 | 機能が多く、キーバインド干渉の可能性 | 採用候補 |
| markdownlint | Markdownの一貫性、VS CodeとCLI/CIの両方で使える | ルールが厳しいとメモ書きの速度を落とす | 採用候補 |
| Foam | VS Code上でbacklinks、graph、daily note、tag explorerなどPKM機能 | Obsidianと二重PKMになりやすい | 後で評価 |
| MLink | VS Code上でObsidian風リンク補助ができる可能性 | 役割が限定的。保守状況とObsidian互換を確認したい | 後で評価 |

## 推奨設定方針

- まず VS Code 拡張は Markdown All in One と markdownlint に絞る。
- markdownlint の設定は `.markdownlint.json` を追加する前に `docs/spec/markdownlint.md` で方針を決める。
- Foam は Obsidian の graph / backlinks で不足を感じた時に評価する。

## 次アクション

1. `docs/spec/markdownlint.md` にルール案を書く。
2. ユーザが許可したら VS Code で Markdown All in One と markdownlint を導入する。
3. 1週間程度使って、Foam が必要か判断する。

## References

- https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one
- https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint
- https://github.com/foambubble/foam

