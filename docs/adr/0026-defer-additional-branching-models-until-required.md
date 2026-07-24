# 0026. 追加のBranching Modelは実要件が確定するまで作成しない

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-24 |

---

## Context（背景）

Main Branch Flow（ADR 0025）に続き、当初はSymnous向け専用Branching Model（仮称：Selective Branching Model／dual-track）と、Nexnos向けLTS Release Branch Flowの計3つのBranching Modelを実装対象としていた。

Symnous向けModelは、「定型的な知識運用は`main`直接、設計・開発変更はBranch＋PR」という2経路併用モデルとして具体的な設計を進めていた。しかし、Main Branch Flowが固まった段階で比較したところ、Symnous向け案は実質的に「Main Branch Flowを少し厳格にしたもの」であり、モデルとして分ける明確な境界（例えばWork Branchを通常経路に固定するなど）を持たせない限り、Main Branch Flowとの違いが薄いことが分かった。Symnousが抱える複雑さ（Raw Dataの日常追加、Knowledge／Valuesの実質変更、ツール開発、スキーマ変更、GitHub Project管理作業が同居するモノレポであること）を再整理すると、これはBranching Modelの選択の問題ではなく、変更の性質ごとにどの経路を使うかという、Repository Convention・リポジトリ固有運用の問題であった。

LTS Release Branch Flowについては、既存のNexnos向けBranch Convention資料を土台に設計へ進もうとしたが、着手直前に、リリース頻度・セマンティックバージョニングの運用・複数バージョンの並行保守期間・LTS対象バージョン・hotfixの扱い・backport方針・release candidateの有無・CI/CDと配布方法・EOL後のBranch管理といった具体要件が、実際のOSSプロジェクトが存在しない現時点では確定できないことが認識された。

---

## Decision（決定）

Branching Modelは、既存のBranching Modelでは表現できない実際のBranch構造または変更経路が確認された場合にのみ追加する。リポジトリ種別、モノレポ構成、将来想定、参考資料の存在だけを理由に追加しない。

この原則の適用結果として、次を決定する。

1. **Symnous専用のBranching Modelは作成しない。** Symnousの変更種別ごとの経路（日常的なデータ追加、人間による意味変更、ツール・スキーマの変更、GitHub Project管理作業など）は、Main Branch FlowとRepository固有運用で表現する。
2. **LTS Release Branch Flow（Nexnos向け）の設計は、実際のOSSプロジェクトでリリース・保守要件が具体化するまで着手しない。**

---

## Rationale（理由）

Branching Modelは、`main`の扱い・Branchの要否・PRの要否・Issueとの対応・永続Branchの構成までを一体として定義する、設計・レビューの負荷が大きい単位である（ADR 0023参照）。リポジトリ種別・モノレポ構成・将来の想定・既存の参考資料の存在といった、実際のBranch運用の確認を伴わない理由でBranching Modelを増やすと、実態に合わない構造を固定したり、既存Modelとの違いが曖昧な重複Modelを生んだりする可能性がある。Branching Modelの追加は、既存Modelでは表現できない実際の構造・変更経路が確認された時点に限ることで、この種の先回り設計を避ける。

この原則をSymnousへ適用すると、モノレポであることや、性質の異なる変更が同居することは、それ自体がBranching Modelを分ける理由にはならない。重要なのは変更の性質であり、リポジトリの構成そのものではない。Main Branch Flowは「`main`直接変更とWork Branchによる変更を、作業の管理方法に応じて選択できるModel」であるため、変更種別ごとの経路の使い分けは、Branching Modelそのものではなく、Repository Convention・リポジトリ固有運用の層で十分に表現できる。

LTS Release Branch Flowについても、リリース・保守に関する要件を確定しないまま先に設計すると、既存資料（Nexnos向け）の想定を過度に一般化したり、実運用に合わない永続Branchを固定したりする可能性がある。実際の要件が明らかになってから設計する方が、再利用可能で実態に合ったBranching Modelになる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| Symnous向け専用Branching Model（2経路併用モデル）を実装する | Main Branch Flowとの実質的な差が、Work Branchを通常経路へ固定するなどの明確な境界を持たせない限り薄く、専用Modelとして独立させる根拠が乏しい |
| モノレポ全般に適用する共通Branching Modelを新設する | モノレポであること自体は変更経路選択の決定要因ではなく、変更の性質で決まるため、リポジトリ構成を基準にしたModelは実態に合わない |
| 既存のNexnos向けBranch Convention資料をそのまま一般化してLTS Release Branch Flowを先行設計する | リリース頻度・LTS期間・backport方針などの具体要件が未確定であり、先行設計するとNexnos固有の想定を過度に一般化したり、実運用に合わない永続Branchを固定したりする可能性がある |
| 想定される全Branching Modelを事前にすべて作成する | 実際の要件が確定していないモデルを先に作ると、後から実態に合わせた手戻りが生じる可能性が高い（Design When Needed） |

---

## Consequences（影響・注意点）

- 今後、新しいBranching Modelを提案する場合は、既存Modelでは表現できない実際のBranch構造・変更経路が確認されていることを示す必要がある。リポジトリ種別・モノレポ構成・将来想定・参考資料の存在だけでは、提案の根拠として十分ではない
- Symnousの変更経路方針は、Repository ConventionまたはSymnous固有運用の文書として別途整理する必要がある。本ADR作成時点では、その具体的な文書化は行っていない
- LTS Release Branch Flowは未設計のまま保留される。実際のOSSプロジェクトが開始され、リリース・保守要件が具体化した時点で、改めてBranching Modelとして設計する
- 将来、Symnousの変更経路の使い分けだけではMain Branch Flowで表現しきれない事情が判明した場合は、Repository Conventionでの調整では対応せず、新しいBranching Modelの作成を検討する
- 本ADRは「作らない・保留する」という判断を記録するものであり、将来Symnous向けModelやLTS Release Branch Flowを作成すること自体を妨げない

---

## Related Documents（関連文書）

- ADR 0023（Branch ConventionをBase Branch ConventionとBranching Modelへ分離する）
- ADR 0025（Main Branch Flowを最初のBranching Modelとして採用する）
- `docs/conventions/patterns/branch/main-branch-flow.md`
- design-notes 0006（Branch Convention再設計とBranching Model確立）
