# 0015. GitHub ProjectにArea/Scopeを紐づけたフィールドを初期標準として採用しない

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

GitHub Projectsの標準フィールドを設計する過程で、Issueや作業項目を技術領域・対象範囲によって分類するAreaフィールドが、明確な活用方法を検討しないまま採用されかけていた。

改めて検討したところ、AreaはコミットメッセージやProjectで使用するScope（Commit ConventionのScope等）と同種の概念として扱おうとしていたことが分かった。しかしAreaとScopeは責務が異なり、連携させるべきではないという判断に至った。

---

## Decision（決定）

GitHub Projectの標準フィールドとして、AreaフィールドおよびScopeと紐づけた分類軸は、初期標準には採用しない。

---

## Rationale（理由）

明確な活用方法・どの判断に寄与するかが定まらないまま分類軸を追加すると、後から見て何のためのフィールドかが分からなくなる。AreaとScopeは責務が異なる概念であり、これらを連携・混同させると、どちらの分類軸としての判断にも寄与しない曖昧なフィールドになる。

必要性が明確になった時点で、Scopeとは独立した責務を持つ分類軸として改めて設計する方が、既存のDesign When Neededの原則に沿う。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| Areaフィールドを、Commit・ProjectのScopeと連携する形で追加する | AreaとScopeは責務が異なる概念であり、連携させると両者の責務が混同され、フィールドの活用目的が曖昧になる |

---

## Consequences（影響・注意点）

- GitHub Project Setup仕様には、Area・Scopeに関する標準フィールドの記述を持たない
- 将来Areaに相当する分類軸が必要になった場合は、Scopeとは独立した責務を持つ概念として改めて設計する
- 未設計の概念について「将来検討する」という記述を現行文書に残さない

---

## Related Documents（関連文書）

- `docs/specifications/github-project-setup.md`
- `docs/conventions/github-project.md`
