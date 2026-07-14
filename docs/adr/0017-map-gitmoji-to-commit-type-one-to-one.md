# 0017. GitmojiとCommit Typeを1対1で対応させる

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

Gitmojiの使用を必須とする運用（ADR 0016参照）のもとで、GitmojiとCommit Typeの対応関係をどう扱うかが論点になった。

GitmojiとTypeの組み合わせが自由になっていると、同じTypeに複数のGitmojiが使われたり、同じGitmojiが複数のTypeに使われたりする状況が生じうる。

---

## Decision（決定）

GitmojiとCommit Typeは、定義された対応表に基づいて1対1で対応させる。対応表にない組み合わせは使用しない。

---

## Rationale（理由）

GitmojiとTypeが1対1に対応することで、どちらか一方を見ただけでもう一方を判断できる。対応がずれると、視覚的な識別（Gitmoji）と機械的な分類（Type）が矛盾し、Git履歴の信頼性を損なう。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| GitmojiとTypeの組み合わせを自由にする | 同じTypeに複数のGitmojiが使われる、あるいは同じGitmojiが複数のTypeに使われる状況が生じ、視覚的な識別とTypeによる分類が一致しなくなる |

---

## Consequences（影響・注意点）

- コミット作成時は、定義された対応表からTypeとGitmojiの組み合わせを選択する
- 対応表にない新しいTypeが必要な場合は、対応するGitmojiも合わせて定義する
- 具体的な対応表の内容は、本ADRの対象外とし、`docs/conventions/commit.md`が定義する

---

## Related Documents（関連文書）

- ADR 0016（Commit MessageでGitmojiの使用を必須とする）
- `docs/conventions/commit.md`
