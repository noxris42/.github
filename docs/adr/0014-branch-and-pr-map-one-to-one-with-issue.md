# 0014. Branch運用を採用する場合、Issue・Branch・PRを一対一で対応させる

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

Issueを作業単位として扱う運用（ADR 0013参照）のもとで、Branchを用いて作業する場合に、BranchとPull Requestをどう対応させるかが論点になった。

複数の作業を同一のBranch上に並行させると、そのBranchから作られるPull Requestに複数の目的の異なる変更が混在し、レビューが困難になることが分かった。

---

## Decision（決定）

リポジトリでBranch運用を採用する場合、1つのIssue（Work）に対して1つのBranchを作成し、そのBranchから1つのPull Requestを作成する。1つのIssueに対応する作業を、複数のBranchやPull Requestに分けない。また、1つのBranch上で複数のIssueに対応する作業を並行させない。

この対応関係は、Branch運用を採用しないリポジトリ（main-only運用等）には適用されない。

具体化として、Branch運用を採用する標準Workflowでは以下の対応関係となる。

```text
1 Issue = 1 Work = 1 Branch = 1 Pull Request
```

---

## Rationale（理由）

複数の作業を同一のBranch上に混在させると、そのBranchから作られるPull Requestが複数の目的の異なる変更をまとめて含むことになり、レビュアーが変更の意図を追いにくくなる。

Issue・Branch・PRを一対一に対応させることで、Issueで示された作業目的から、Branchでの変更、Pull Requestでのレビューまでの追跡経路が一貫する。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| 複数の作業を同一Branch上で並行させる | Pull Requestに複数の目的の異なる変更が混在し、レビューが困難になる |
| 1つのIssueを複数のBranch・Pull Requestへ分割する | 1つのWorkの完了状態が複数の統合単位へ分散し、Issueから完了までの対応関係が曖昧になる。ADR 0013で1 Issueを1 Workに限定しているため、大きな作業はIssue自体を分割することで対応する |

---

## Consequences（影響・注意点）

- Branch運用を採用するリポジトリでは、Issueごとに独立したBranchとPull Requestを作成する
- Branch運用を採用しないリポジトリ（main-only運用等）では、本ADRの対応関係は適用されない。この場合の運用は、ADR 0012・0013（Issueを起点とし、1 Issueを1 Workとする運用）のみに従う
- Branch・PRの具体的な命名規則・作成手順は、本ADRの対象外とし、`docs/conventions/branch.md`・`docs/specifications/github-workflow.md`が定義する

---

## Related Documents（関連文書）

- ADR 0012（Issueを作業の起点とする）
- ADR 0013（1つのIssueは1つのWorkを表す）
- `docs/conventions/branch.md`
- `docs/specifications/github-workflow.md`
