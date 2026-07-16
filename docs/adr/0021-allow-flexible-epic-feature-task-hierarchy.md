# 0021. Epic・Feature・Taskの階層を柔軟な構造とする

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-16 |

---

## Context（背景）

`docs/specifications/github-project-setup.md`では、`Epic → Feature → Task`を標準的な階層構造として定義する一方、EpicやFeatureを使用しないTask-only運用を許容していた。

しかし、親子関係はEpicとFeature、FeatureとTaskに限定して記述されており、中間階層を省略する`Epic → Task`や、上位階層を省略する`Feature → Task`の扱いは体系的に定義されていなかった。

一方、実装済みのEpic Issue Templateは、Epic配下にFeatureまたはTaskを直接紐づける運用を許容していた。標準ラベル定義の説明をSpecificationと照合した際、Specification・Issue Template・想定する運用の間で階層省略の扱いが統一されていないことが明らかになった。

`Epic → Feature → Task`を常に適用すると、Featureを設ける意味が薄い場合にも中間Issueを作成する必要があり、Issue管理自体が過剰になる可能性がある。そのため、標準構造を維持しながら、規模・性質に応じた階層省略を明示的に定義する必要があった。

---

## Decision（決定）

Epic・Feature・Taskの3階層を標準構造として維持しつつ、固定された必須階層とはしない。プロジェクトの規模・性質に応じて、以下の構造を許容する。

```text
Epic → Feature → Task
Epic → Task
Feature → Task
Task only
```

許容する親子関係はEpicとFeature、EpicとTask、FeatureとTaskの3種のみとし、Taskは子Issueを持たない。Epic→Epic・Feature→Feature（同一Type間の階層）、Feature→Epic・Task→Feature・Task→Epic（階層方向の逆転）、Taskが子Issueを持つ構造は許容しない。

---

## Rationale（理由）

階層は、Issue数を増やすための形式要件ではなく、管理対象の規模とまとまりを表現する手段である。大規模なテーマで複数成果物を含む場合はEpic→Feature→Task、複数作業をまとめるテーマだがFeatureへ分ける必要がない場合はEpic→Task、一つの成果物を複数作業へ分解する場合はFeature→Task、単発または小規模な作業はTask onlyというように、規模に応じて必要な階層のみを使う方が、階層維持のためだけに不要なEpicやFeatureを作成する事態を避けられる。

この方針は、すでに実装済みのIssue Templateの実態（Epic直下へのTask紐づけを許容する記述）とも一致しており、SpecificationとTemplateの整合を取る意味も持つ。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| `Epic → Feature → Task`を固定された必須階層として明確化する | Featureを設ける意味が薄い場合にも中間Issueの作成を強制し、Issue管理が過剰になる。既存のEpic Issue Templateが許容していたEpic直下Taskとも整合しない |
| Epic・Feature・Taskという階層概念自体を廃止し、フラットなIssue管理へ変更する | 大規模なテーマを扱う際に、成果物単位・作業単位のまとまりを表現する手段が失われる。標準構造としての階層は、規模が大きい場合の目安として引き続き有用である |

---

## Consequences（影響・注意点）

- `docs/specifications/github-project-setup.md`のProject Structureは、標準構造を維持しつつ階層省略を許容する内容へ改定する
- ラベル定義（`templates/labels/standard/labels.yml`・`.github/labels.yml`）のEpic説明は、Feature・Task双方を束ねる内容のまま維持する
- 既存のIssue Template（`epic.yml`・`feature.yml`・`task.yml`）はすでにこの方針と整合しており、変更を要しない
- 将来、運用実績を踏まえて階層をより厳密化する、または階層概念自体を見直す可能性がある

---

## Related Documents（関連文書）

- `docs/specifications/github-project-setup.md`
- `templates/issue-templates/standard/epic.yml`
- `templates/labels/standard/labels.yml`
