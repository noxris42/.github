# 0023. Branch ConventionをBase Branch ConventionとBranching Modelへ分離する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-24 |

---

## Context（背景）

Convention Extension Architecture（ADR 0022）の最初の適用対象として、Branch ConventionのPattern Conventionを設計しようとした。当初は、`main-primary`（mainを標準の作業場所とし直接変更を許可）・`dual-track`（定型更新はmain直接、設計・開発変更はBranch＋PR）・`protected-main`（mainへの直接変更を禁止しBranch＋PRのみを経路とする）という3つの「Branch Pattern」を設計する方向で進んでいた。

この過程で、GitHub Flow・Git Flow・添付されたNexnos向けLTS Release Branch Flow資料を比較したところ、これらは`main`保護の有無だけでなく、`maint/vX`・`next`・`release`・`hotfix`・パッチ反映・メジャーバージョン移行・Branch削除までを含む、Branch運用全体のライフサイクルを定義するものであり、検討中の3 Patternより一段具体的であることが分かった。

これにより、「リポジトリ構築時に選択すべきものは、保護レベルのような部分的な差分（Branch Pattern）ではなく、`main`の扱い・Branchの要否・PRの要否・Issueとの対応・永続Branchとhotfix経路などを一体として定義する、Branch運用全体の枠組みである」という認識に至った。

また、現行の（当時の）Branch Conventionは「Base」を名乗りながら、実質的にはIssue駆動の簡易GitHub Flow（`<type>/<issue-number>-<short-description>`という命名、Issue→Branch→Commit→PR→Merge→Deleteという固定ライフサイクル、1 Issue = 1 Branch、Merge後の削除必須）を内包しており、`maint/vX`のような永続Branchを持つModelや、Issueを必須としないModelを表現できないことが判明した。

---

## Decision（決定）

Branch ConventionにおけるPattern Conventionの実体を「Branching Model」と呼ぶ。Branching Modelは、リポジトリにおける各Branchの役割・寿命・作成条件・分岐元・統合先・変更経路・（一時Branchについては）終了条件を一体として定義する。

`docs/conventions/branch.md`をBase Branch Conventionとして再設計し、特定のBranching Modelに依存しない共通原則と、Branching Modelが満たすべき最低限の契約のみを定義する。具体的には次を各Branching Modelへ委譲し、Baseでは決定しない。

- `main`への直接Commit／Pushの可否
- 作業Branch・Pull Requestの要否
- Issueとの対応関係
- 使用するBranch Type、Merge方式
- Branch Protectionの具体的設定
- release・hotfix・保守Branchの構成

各リポジトリは、Branching Modelを正確に1つ選択する。Base Branch Conventionは、Branching Modelが最低限満たすべき定義要件（各Branchの役割・寿命・作成条件・分岐元・統合先・変更経路、一時Branchの終了条件）と、Branch名の共通文字制約、Branch寿命の分類（永続／一時）、一時Branchのライフサイクル完了原則を定義する。

---

## Rationale（理由）

Branch運用は、個々のRuleを独立に組み合わせられるものではなく、`main`の扱い・Branchの要否・PRの要否・Issueとの対応・永続Branchの構成が相互に依存する、一体としての設計判断である。保護レベルのような部分的な差分をPatternとして選ばせる設計では、GitHub Flow・Git Flow・LTS Release Branch Flowのような実際の運用モデルを表現できない。

Branching Modelという単位でPattern Conventionを実装することで、性質の異なるBranch運用を、実際の要件に応じて独立した一貫性のあるModelとして表現できる。また、Base Branch Conventionを「Branching Modelに依存しない共通契約」に限定することで、特定の運用モデル（Issue駆動のGitHub Flow型）が共通規約に紛れ込む状態を解消できる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| `main-primary`・`dual-track`・`protected-main`という保護レベルの違いを3つのPattern Conventionとして実装する | GitHub Flow・Git Flow・LTS Release Branch Flowのような実際の運用モデルより一段抽象的で、`maint/vX`・`next`・hotfix経路などを持つModelを表現できない。保護レベルの組み合わせを増やすたびに複合Patternが増殖する |
| 既存Branch Conventionのルール（Issue駆動命名・固定ライフサイクル・1 Issue = 1 Branch・Merge後削除必須）をBase共通Ruleとして維持する | Issueを必須としないModelや、`maint/vX`のような永続Branchを持つModelを表現できない。特定の運用モデルを前提とした共通規約になってしまう |
| Branching Modelの選択とは別に、Branch Pattern（保護レベル）とGitHub Flow等（詳細フロー）を独立した2つのPattern軸として組み合わせる | 「1 Conventionにつき1 Pattern」という既存アーキテクチャの前提と合わず、組み合わせごとの複合Patternが増殖する |

---

## Consequences（影響・注意点）

- `docs/conventions/branch.md`はBase Branch Conventionとして、Branching Modelに依存しない共通契約のみを定義する
- 個別のBranching Modelは`docs/conventions/patterns/branch/`配下にPattern Conventionとして実装する
- Branching Modelを新設する際は、その運用モデル全体（`main`の扱い・Branch要否・PR要否・Issue対応・永続Branch構成・終了条件）を一体として設計する必要があり、単一Ruleの追加より設計・レビューの負荷が大きい
- 既存Branch Conventionが前提としていたIssue駆動の固定ライフサイクル・1 Issue = 1 Branch・Merge後削除必須は、Base共通Ruleとしては廃止された。Branch運用時のIssue・Branch・PRの対応関係は、本ADRの対象外とし、別途定義する（ADR 0024参照）

---

## Related Documents（関連文書）

- ADR 0022（規約はBase／Pattern／Repositoryの3層とし、Rule ID単位で拡張する）
- ADR 0011（Conventionは採用後の共通ルールのみを定義し、採用の可否は扱わない）
- ADR 0012（Issueを作業の起点とする）
- ADR 0013（1つのIssueは1つのWorkを表す）
- `docs/conventions/branch.md`
- `docs/conventions/patterns/branch/main-branch-flow.md`
- design-notes 0006（Branch Convention再設計とBranching Model確立）
