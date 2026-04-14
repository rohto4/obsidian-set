# Foam Evaluation

作成日: 2026-04-14

## 目的

VS Code中心の運用で、FoamをObsidianと併用する価値があるかを評価する。
現時点では導入しない。Obsidianと役割が重複しやすいため、条件付き参考資料として保持する。

## 何ができるか

- VS Code上でwikilink、backlink、graph、daily noteに近いPKM体験を作れる。
- Markdown repoをVS Code中心に扱いやすくできる。
- Obsidianを開かなくてもリンク中心のnote編集を進められる可能性がある。

## できない・弱い可能性

- Obsidian Sync、Obsidian plugin、mobile UIの代替にはならない。
- ObsidianとFoamの両方でgraph / backlinks / daily notesを使うと役割が重複する。
- このPJではまだObsidian側の保存体系が確定していないため、先にFoamを入れると分類設計がぶれやすい。

## 評価観点

1. Obsidianのwikilinkと衝突しないか。
2. VS Code上のbacklink / graphが実用に足るか。
3. daily note運用を始める場合、Obsidian側と重複しないか。
4. 拡張機能なしでも今のMarkdown運用で足りるか。
5. AI agentが作業する時に、Foam固有の補助が本当に必要か。

## 暫定判断

導入は待ち。
VS Code中心の運用という前提には合うが、Obsidianの役割とぶつかる可能性が高い。
最初はMarkdown + Git + Obsidian UIで進め、リンク数が増えてVS Code側のbacklink体験が不足したら再評価する。

## References

- https://github.com/foambubble/foam
