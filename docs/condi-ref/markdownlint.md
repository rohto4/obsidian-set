# Markdownlint Policy

作成日: 2026-04-14

## 目的

Markdown knowledge base として、最低限の読みやすさと差分の安定性を保つ。
ただし、Obsidian のメモ速度を落とすほど厳しくしない。

## 入れると何がうれしいか

- 見出し、リスト、空行、リンクなどの崩れを早く見つけられる。
- VS Codeで編集しながらMarkdownの警告を見られる。
- AIが生成したMarkdownの体裁崩れを発見しやすい。
- 将来CLI/CIでドキュメント品質チェックへ拡張できる。

## 入れない方がよい可能性

- メモ速度を落とすほど警告が多い場合。
- Obsidian独自記法と衝突する場合。
- 長いURLや日本語文でline length警告が邪魔になる場合。

このため、最初はextension導入候補に留め、設定ファイル追加は別判断にする。

## 初期方針

- VS Code extension: markdownlint は導入候補。
- project config: `.markdownlint.json` は次の段階で追加候補。
- CI: まだ導入しない。

## 初期ルール案

厳しくしすぎない。

```json
{
  "default": true,
  "MD013": false,
  "MD033": false,
  "MD041": false
}
```

理由:

- `MD013` line length は日本語・URL・表で邪魔になりやすい。
- `MD033` inline HTML はObsidianやdocsで必要になる可能性がある。
- `MD041` first line heading はfrontmatter付きnoteやテンプレートで邪魔になる可能性がある。

## 導入手順案

1. VS Code に markdownlint extension を入れる。
2. 1週間ほど警告の出方を見る。
3. `.markdownlint.json` を追加する。
4. 必要なら CLI lint を追加する。

## References

- https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint
- https://github.com/DavidAnson/markdownlint
