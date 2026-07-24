# 0025. Main Branch Flowを最初のBranching Modelとして採用する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-24 |

---

## Context（背景）

Base Branch ConventionをBranching Modelへ分離する方針（ADR 0023）を受け、最初に実装するBranching Modelとして`.github`リポジトリ向けのModelを設計することにした。`.github`リポジトリの実際の運用は、Issue登録を伴わない直接編集を含む、比較的軽量なドキュメント・Workflow管理であり、既存の（当時の）Issue駆動を前提としたBranch Conventionとは実態が乖離していた。

設計の過程で、Pattern名から「Flow」という語を避ける方針が一度検討されたが（Git Flow・GitHub Flow・LTS Release Branch Flowとの混同を避けるため）、Branching Model概念の確立（ADR 0023）により、Branchのライフサイクル全体を定めるという意味では「Flow」という語がむしろ適合することが分かり、この制約は解消された。

---

## Decision（決定）

`.github`リポジトリ向けの最初のBranching Modelとして、Main Branch Flowを採用する。Main Branch Flowは次を骨子とする。

- `main`を唯一の永続Branchとし、正本かつ通常の作業場所とする（分岐元・統合先を持たず、終了条件を持たない）
- `main`への直接Commit／Pushを許可する。Pull Requestを必須とするBranch Protectionは標準設定として要求しない
- Work Branchは一時Branchとして任意に使用できる（`main`から分岐し`main`へ統合する）
- GitHub Projectで管理する作業には、Task Issue・Work Branch・Pull Requestを必須とする厳格な変更経路を適用する（GitHub Project Convention・Base Branch Conventionに従う）
- GitHub Projectで管理しない作業のWork Branchを`main`へ統合する場合、Pull RequestはSHOULD（基本経路だが必須ではない）とする
- `develop`・release・hotfix・保守Branchなど、`main`以外の永続Branchは標準構造に含めない

`docs/repository-manifest.md`において、`.github`リポジトリ自身がBranching ModelとしてMain Branch Flowを選択する。

---

## Rationale（理由）

`.github`リポジトリの実態（軽量なドキュメント・Workflow管理、Issueなしの直接編集を含む）には、`main`を通常の作業場所とし直接変更を許可するModelが適合する。一方で、GitHub Projectで管理する作業（Task・Feature・Epicとして追跡する作業）については、Project上の状態とBranch上の変更を一致させる価値があるため、その場合に限り厳格な経路を要求する。

`main`以外の永続Branchを持たないシンプルな構造にすることで、`.github`のような軽量運用のリポジトリが、不要な永続Branchやリリース管理の概念を持ち込まずに済む。Project管理外のWork BranchでPull RequestをSHOULDに留めるのは、差分確認・CI検証の価値を認めつつ、軽量運用の柔軟性を損なわないためである。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| すべての変更にBranch＋Pull Requestを要求する（Issue駆動のGitHub Flow型を標準採用） | `.github`の実態（Issueなしの直接編集を含む軽量運用）と乖離し、運用負荷が実態に合わない |
| すべての変更を`main`直接で行うモデルとする | GitHub Projectで管理する作業についても差分確認・レビューの機会が失われる |
| Issueの有無だけで変更経路を固定的に決める | GitHub Project登録の有無という別の軸が存在し、Issueの有無だけでは実際に必要な厳格さの水準を表現できない（ADR 0024参照） |
| `develop`などの永続Branchを標準構造へ追加する | `.github`の実態には、リリース管理や次期バージョン開発のための永続Branchを必要とする根拠がなく、構造を不必要に複雑化する |
| `.github`専用の名称・専用の狭い適用範囲として設計する | 同種の軽量運用は他のリポジトリにも起こりうるため、`.github`固有ではなく再利用可能なBranching Modelとして一般化する方が、Convention Extension Architectureの意図（Pattern Conventionは再利用可能な標準拡張）に合う |

---

## Consequences（影響・注意点）

- Main Branch Flowは`docs/conventions/patterns/branch/main-branch-flow.md`として実装され、`.github`リポジトリ自身がRepository ManifestでこのModelを選択する
- `main`以外の永続Branchや、本Modelで定義していない変更経路が必要になった場合は、Repository Conventionではなく新しいBranching Modelとして扱う（Modelの中心的構造を変えるため）
- 他のリポジトリも、実態が`.github`と同様に軽量な運用であれば、Main Branch Flowを選択できる
- 本ADRはMain Branch Flowという1つのBranching Modelの採用を記録するものであり、Symnous向け専用Modelの要否・LTS Release Branch Flowの扱いは別途判断する（ADR 0026参照）

---

## Related Documents（関連文書）

- ADR 0023（Branch ConventionをBase Branch ConventionとBranching Modelへ分離する）
- ADR 0024（Task Issue作成とGitHub Project登録を分離し、厳格な1対1経路はProject管理作業に限定する）
- ADR 0020（`.github`リポジトリ自身も共通標準の適用対象とする）
- `docs/conventions/patterns/branch/main-branch-flow.md`
- `docs/repository-manifest.md`
- design-notes 0006（Branch Convention再設計とBranching Model確立）
