# 0024. Task Issue作成とGitHub Project登録を分離し、厳格な1対1経路はProject管理作業に限定する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-24 |

<!-- Supersedes ADR 0014（Branch運用を採用する場合、Issue・Branch・PRを一対一で対応させる） -->

---

## Context（背景）

ADR 0014は、「Branch運用を採用する場合、1 Issue = 1 Work = 1 Branch = 1 Pull Request」という単一の対応関係を定義していた。この決定は、main-only運用にはこの対応関係が適用されないという例外を含んでいたが、「Branch運用を採用するかどうか」という単一の分岐だけを前提としていた。

Base Branch ConventionをBranching Modelへ分離する作業（ADR 0023）の過程で、Branching Model自体がIssueとの対応関係・Pull Requestの要否を個別に定義できるようになり、Branch運用の採否という単一分岐では実際の運用を表現しきれないことが分かった。特に、Task Issueを作成することと、それをGitHub Projectで管理することが暗黙に同一視されており、GitHub Projectを使わない軽量な運用でもTask Issueテンプレートを使って作業内容を記録したい、という需要と、GitHub Projectで管理する作業には厳格な経路を適用したいという需要の両方があることが明らかになった。

---

## Decision（決定）

次の3つの軸を独立した判断として分離する。

1. **Task Issueの作成とGitHub Project登録は独立である。** Task Issueは、GitHub Projectで管理しない場合でも、Task Issueテンプレートを使って作業内容・背景・完了条件を記録するために作成できる。
2. **GitHub Projectで管理する作業には、厳格な変更経路を適用する。** Task IssueをGitHub Projectへ登録した場合、対応するWork Branchを作成し、そのWork Branchの変更を1つのPull Requestとして統合する（Task Issue・Work Branch・Pull Requestを1対1で対応させる）。Project Statusの遷移・Review／Done条件は、GitHub Project Conventionが定義する。
3. **GitHub Projectで管理しない作業の変更経路は、Branching Modelが定義する。** GitHub Projectへ登録しないTask Issue、Issueなし作業、IssueなしWork Branchの可否・変更経路は、Base Branch Conventionでは決定せず、各Branching Modelが定義する。ただし、Task IssueとWork Branchを対応させる場合は、GitHub Project登録の有無によらず、常に1対1（1つのWork Branchを複数のTask Issueに対応させない）とする。

Epic・Feature・Taskという型の意味・階層は、GitHub Project Setupを正本とし、Branch Conventionはこれを再定義しない。Work Branchと対応できるIssue種別は、GitHub Project Setupが定義するTask Issueとする。

---

## Rationale（理由）

「Branch運用を採用するかどうか」という単一の分岐だけでは、GitHub Projectで管理する作業と管理しない作業とで、必要な厳格さの水準が異なるという実態を表現できない。GitHub Projectで管理する作業は、Project上の作業単位・Branch上の変更範囲・レビュー対象を一致させる必要があり、Task Issue・Work Branch・Pull Requestの対応を厳格にする価値が高い。一方、GitHub Projectで管理しない軽量な作業にまで同じ厳格さを要求すると、Main Branch Flowのような`main`を通常の作業場所とするModelが成立しなくなる。

Task Issue作成をGitHub Project登録から切り離すことで、Task Issueテンプレートによる作業記録の価値（背景・完了条件の明文化）と、GitHub Projectによる管理コストを別々に選択できるようになる。Task IssueとWork Branchの1対1原則自体は、対応させると決めた場合に一貫性を保つための最低限の契約として、GitHub Project登録の有無によらず維持する。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| すべてのTask IssueをGitHub Project管理対象にする | 軽量なドキュメント管理や`main`直接作業が中心のリポジトリで、Task Issue作成のたびにProject登録を強制することになり、運用負荷が実態に合わない |
| すべてのTask IssueにWork Branchを必須化する | Main Branch Flowのように`main`を通常の作業場所とするModelと矛盾する |
| すべてのWork BranchにTask Issueを必須化する | IssueなしWork Branch（軽微な変更の隔離目的）を許可する余地がなくなる |
| Base Branch ConventionでIssueなし作業・BranchなしTask Issueを一律禁止する | Branching Modelごとに異なる運用（Project管理外では柔軟にする等）を表現できなくなる |

---

## Consequences（影響・注意点）

- ADR 0014（Branch運用を採用する場合、Issue・Branch・PRを一対一で対応させる）は、本ADRにより置換される。ADR 0014のStatusをSupersededとし、Superseded byに本ADRの番号を記載する
- Base Branch Conventionは、Task IssueとWork Branchを対応させる場合の1対1原則（双方向）のみを共通契約として定義し、Task Issue・Work Branch双方の作成義務は定義しない
- GitHub Project Convention（`docs/conventions/github-project.md`）は、Managed Work Ruleとして、GitHub Project管理作業のTask Issue・Work Branch・Pull Request対応を定義する
- 各Branching Modelは、GitHub Project管理外の作業について、Issueなし作業・IssueなしWork Branch・Project未登録Task Issueの完了条件・Pull Requestの要否を個別に定義する
- Epic・Feature・Taskの意味・階層はGitHub Project Setupが正本のまま維持され、Branch ConventionおよびBranching Modelはこれを再定義しない

---

## Related Documents（関連文書）

- ADR 0012（Issueを作業の起点とする）
- ADR 0013（1つのIssueは1つのWorkを表す）
- ADR 0014（Branch運用を採用する場合、Issue・Branch・PRを一対一で対応させる）※本ADRにより置換
- ADR 0023（Branch ConventionをBase Branch ConventionとBranching Modelへ分離する）
- `docs/conventions/branch.md`
- `docs/conventions/github-project.md`
- `docs/specifications/github-project-setup.md`
- design-notes 0006（Branch Convention再設計とBranching Model確立）
