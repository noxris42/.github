# Canonical Primary Language Support Architecture（正規主要言語補助アーキテクチャ）

## Purpose（目的）

本文書は、`noxris42` において**Repository Documentation（Repository文書）で使用されるEnglish Representation（英語表現）について、そのEnglish Representation（英語表現）の理解をPrimary Languageで補助するためにRepositoryが一貫して再利用するPrimary Language Representation（主要言語表現）** との対応を定義するArchitecture Asset（アーキテクチャ資産）である。

本文書が扱う問いは次の4点である。

1. English Representation（英語表現）と、その理解補助としてRepositoryが一貫して再利用するPrimary Language Representation（主要言語表現）との対応は、何によって成立するのか。
2. その対応は、English Representation1つに対していくつ成立するのか。
3. その対応を成立させることは、English Representation（英語表現）そのものの意味、およびEnglish Representation（英語表現）が指すUnderlying Meaning（対象の意味）を定めることとどこで分かれるのか。
4. その対応が成立していることと、Concrete Usage OccurrenceでPrimary Language Representation（主要言語表現）が表示されることは、どこで分かれるのか。

本文書が定義するのは、この対応を成立させるArchitecture-level Semantic Modelである。個々のEnglish Representation（英語表現）に対する具体的なPrimary Language Representation（主要言語表現）の値は、本文書が定義しない。

本文書におけるPrimary Languageは、Repository Documentation（Repository文書）のHuman-readable Natural Language Representation（人間可読な自然言語表現）がMeaning（意味）を伝える基準言語である。Primary Language Representation（主要言語表現）は、そのPrimary Languageによって記述されたRepresentation（表現）である。どの言語がPrimary LanguageであるかというConcrete Assignment（具体割当）は、本文書が定義しない。

本文書は、Formal Terminology Management、 Translation Management、 Naming Managementを責務としない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)が定義するArchitecture Area（アーキテクチャ領域）に属する通常のDocumentation Asset（文書資産）である。同AreaのArea Responsibility（領域責務）であるSemantic / Structural Modelの定義として、本文書はCanonical Primary Language Support Association（正規主要言語補助対応）を成立させるConcept（概念）・Relationship・ Boundary（境界）・Definition Authority（定義権限）を定義する。Areaを代表・集約するAssetではない。

```text
Repository Governance Documentation Framework
        ▲
        │ belongs to
Canonical Primary Language Support Architecture
```

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は上位設計にある。本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）とDocument Responsibility（文書責務）
- Definition Authority（定義権限）
- Documentation Area（文書責務領域）とArea Responsibility（領域責務）

### Position（設計上の位置づけ）

本文書は[Documentation Structure Architecture](documentation-structure.md)を上位Sourceとして参照する。

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ presupposes
Canonical Primary Language Support Architecture
```

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 本文書が対応元として扱うEnglish Representation（英語表現）の局所的な意味
- Canonical Primary Language Support Representation（正規主要言語補助表現）が何によって成立するか
- Canonical Primary Language Support Association（正規主要言語補助対応）が何を表す関係であるか
- 同Association（対応）について現在必要なMultiplicity（多重度）
- Canonical Primary Language Support Representation（正規主要言語補助表現）と、English Representation（英語表現）そのものとのDefinition Authority Boundary
- Canonical Primary Language Support Representation（正規主要言語補助表現）と、Underlying Meaning（対象の意味）とのDefinition Authority Boundary
- Canonical Primary Language Support Representation（正規主要言語補助表現）と、別のSubjectについてのDefinition Responsibility（定義責務）が定義するHuman-readable Representation（人間可読表現）とのDefinition Authority Boundary
- Architecture-level Semantic ModelとIndividual Canonical ValueとのDefinition Authority Boundary
- Canonical Primary Language Support Association（正規主要言語補助対応）の成立と、Documentation Presentation（文書上の表示）とのBoundary（境界）

### Out of Scope（本文書が定義しない範囲）

- English Representation（英語表現）のIdentity（同一性）、Meaning（意味）、Formal Status（正式地位）、Category（分類）、およびNameとしての地位
- English Representation（英語表現）が指すUnderlying Meaning（対象の意味）そのもの
- 個々のEnglish Representation（英語表現）と個々のCanonical Primary Language Support Representation（正規主要言語補助表現）との具体的な対応の値
- 別のSubjectについてのDefinition Responsibility（定義責務）が定義するHuman-readable Representation（人間可読表現）そのもの、およびそのLanguage-specific Representation
- Subject-specific RepresentationまたはLocal Presentationの詳細Model
- Primary Language Representation（主要言語表現）側から見た逆方向のMultiplicity（多重度）
- Title・Heading（見出し）・Body、初出、常時表示等のPresentation Rule
- Registry・Schema・Field・ Stable Identifier等の管理機構
- Workflow、Actor Model、 Candidate Detection、Occurrence Count（出現回数）
- Alias・Synonym、Lifecycle、 Versioning（版管理）
- どの言語がPrimary LanguageであるかというConcrete Assignment（具体割当）、およびその保持先
- English Representation（英語表現）とPrimary Language Representation（主要言語表現）とのSupport Association以外の言語間対応を扱うGeneric Translation Model、 Generic Language Map、 Localization Model
- Validator・Linter・CLI・CI等のTool要求

本節が示すのは、本文書がDefinition Authority（定義権限）を持たない範囲である。本節は、ここに挙げた事項の存在または導入を禁止するものではない。

## Concept Model（概念モデル）

### Model Overview（Model全体像）

本文書が成立させるModelは次である。

```text
English Representation
        │
        │ 0..1
        │ is canonically supported by
        │
        ▼
Canonical Primary Language Support Representation
```

この矢印が表すRelationshipをCanonical Primary Language Support Association（正規主要言語補助対応）と呼ぶ。

本Modelが保持するConcept（概念）は次の3つのみである。

- English Representation（英語表現）
- Canonical Primary Language Support Representation（正規主要言語補助表現）
- Canonical Primary Language Support Association（正規主要言語補助対応）

### English Representation（英語表現）

English Representation（英語表現）は、Repository Documentation（Repository文書）で意図的に使用され、本ModelにおいてCanonical Primary Language Support Association（正規主要言語補助対応）の対応元として扱われ得る英語によるRepresentation（表現）である。

本文書はEnglish Representation（英語表現）を、本Modelが対応元を指し示すために必要な範囲のLocal Input Conceptとして扱う。

したがって本文書は、English Representation（英語表現）について次を定義しない。

- Identity（同一性）
- Meaning（意味）
- Formal Status（正式地位）
- Category（分類）
- Nameとしての地位

本文書は、これらを担う独立したConcept（概念）を本Modelへ導入しない。

### Canonical Primary Language Support Representation（正規主要言語補助表現）

Canonical Primary Language Support Representation（正規主要言語補助表現）は、特定のEnglish Representation（英語表現）の理解をPrimary Languageで補助するため、そのEnglish Representation（英語表現）とのCanonical Primary Language Support Association（正規主要言語補助対応）においてRepositoryが一貫して再利用するPrimary Language Representation（主要言語表現）である。

Canonicalityは、Primary Language Representation（主要言語表現）単体に対して成立しない。成立するのは、特定のEnglish Representation（英語表現）とのAssociation（対応）に対してである。同じ語形のPrimary Language Representation（主要言語表現）が別のEnglish Representation（英語表現）とのAssociation（対応）においてCanonicalであるかどうかは、そのAssociation（対応）ごとに定まる。

本文書は、次の境界を保持する。

```text
Canonical Primary Language Support Representation
≠ English RepresentationのIdentity
≠ Underlying MeaningのDefinition
≠ Translationとして唯一正しい表現
```

Canonical Primary Language Support Representation（正規主要言語補助表現）が成立していることは、そのPrimary Language Representation（主要言語表現）がTranslationとして唯一正しいことを意味しない。成立しているのは、Repositoryが理解補助として一貫して再利用するという対応のみである。

### Canonical Primary Language Support Association（正規主要言語補助対応）

Canonical Primary Language Support Association（正規主要言語補助対応）は、English Representation（英語表現）と、その理解補助としてRepositoryが一貫して再利用すると決定したCanonical Primary Language Support Representation（正規主要言語補助表現）とのRelationshipである。

### Association Establishment（対応の成立）

Canonical Primary Language Support Association（正規主要言語補助対応）は、Repositoryが、特定のEnglish Representation（英語表現）に対して一貫して再利用するPrimary Language Representation（主要言語表現）をCanonicalとして決定したときに成立する。

本文書は、この成立を上記Relationshipの意味として扱い、成立可否を判定する独立したConcept（概念）を導入しない。Occurrence Count（出現回数）、Candidate Detection、 Formal Status（正式地位）等の付随的な性質から成立を導出しない。

### Multiplicity（多重度）

本文書が定義するMultiplicity（多重度）は、現在必要な方向のみである。

```text
1 English Representation
    → 0..1 Canonical Primary Language Support Representation
```

これが意味するのは次の2点である。

- あるEnglish Representation（英語表現）についてPrimary Language Supportが必要でない場合、Canonical Primary Language Support Association（正規主要言語補助対応）は存在しなくてよい。
- Canonical Primary Language Support Association（正規主要言語補助対応）が成立する場合、そのEnglish Representation（英語表現）に対するCanonical Primary Language Support Representation（正規主要言語補助表現）は1つである。

Primary Language Representation（主要言語表現）側から見た逆方向のMultiplicity（多重度）は、現在のNeedから導出されないため、本文書は定義しない。定義しないことは、逆方向に制約が存在しないことを意味しない。

## Responsibility Boundary（責務境界）

### Boundary with English Representation and Underlying Meaning（英語表現および対象の意味との境界）

本文書がDefinition Responsibility（定義責務）を持つのは、Canonical Primary Language Support Association（正規主要言語補助対応）を成立させるConcept（概念）・Relationship・ Boundary（境界）のみである。

```text
English Representationそのもの
Underlying Meaning
        ↓
それぞれの対象を所有する既存のDefinition Authority

Canonical Primary Language Support Associationの
Concept・Relationship・Boundary
        ↓
本文書のDefinition Responsibility
```

したがって、あるEnglish Representation（英語表現）がCanonical Primary Language Support Representation（正規主要言語補助表現）を伴っていることは、そのPrimary Language Representation（主要言語表現）がEnglish Representation（英語表現）そのもの、またはUnderlying Meaning（対象の意味）を確定させていることを意味しない。意味の確定は、常にその対象を所有するDefinition Authority（定義権限）側にある。

本文書は、English Representation（英語表現）およびUnderlying Meaning（対象の意味）に関するDefinition Authority（定義権限）の一般Modelを新たに設計しない。

### Boundary with Human-readable Representation Defined by Another Subject（別のSubjectが定義するHuman-readable Representationとの境界）

Canonical Primary Language Support（正規主要言語補助）が扱うのは、Repository Documentation（Repository文書）で使用されるEnglish Representation（英語表現）の理解を補助するためにRepository横断で再利用されるPrimary Language Reading Supportである。

Human-readable Representation（人間可読表現）そのものが、別のSubjectについてのDefinition Responsibility（定義責務）の一部として定義されている場合がある。この場合、そのRepresentation（表現）のLanguage-specific Representationを定めるのは、そのSubjectを所有するDefinition Authority（定義権限）側である。

```text
別のSubjectについての
Definition Responsibilityが定義する
Human-readable Representation
        ↓
そのSubjectを所有するDefinition Authority

English Representationの理解補助として
Repository横断で再利用される
Primary Language Reading Support
        ↓
本文書が成立させる
Canonical Primary Language Support Association
```

したがって、そのようなRepresentation（表現）は本文書のDefinition Authority（定義権限）の外にある。本文書は、それを定義・置換・上書きしない。

また、あるRepresentation（表現）がEnglish Representation（英語表現）と同じSurface Formであること、またはあるPrimary Language Representation（主要言語表現）がCanonical Primary Language Support Representation（正規主要言語補助表現）と同じPrimary Language Valueであることは、それだけでは同じSemantic Responsibility（意味上の責務）を意味しない。本文書は、Surface Formの一致、またはPrimary Language Valueの一致のみからCanonical Primary Language Support Association（正規主要言語補助対応）の成立を推論しない。

本文書は、そのようなRepresentation（表現）がどのように定義または表示されるかについてのModelを新たに設計しない。

### Boundary between Architecture-level Semantic Model and Individual Canonical Value（Architecture-level Semantic ModelとIndividual Canonical Valueとの境界）

本文書は、Architecture-level DefinitionとIndividual Canonical Valueを分離する。

```text
Canonical Primary Language Supportの
Concept・Relationship・Boundary
    → 本文書

個々のEnglish Representation
    ↔
個々のCanonical Primary Language Support Representation
という具体的なCanonical Associationとその値
    → 下位のDefinition-holding Asset
```

本文書は、

```text
Design Dependency → 設計依存
```

のような個別のPairを定義しない。本文書が成立させるのは、そのようなPairが何であるかを説明するModelである。

## Availability / Presentation Boundary（利用可能性と表示の境界）

Documentation Presentation（文書上の表示）は、Canonical Primary Language Support Representation（正規主要言語補助表現）がConcrete Usage Occurrenceへ実際に現れることである。

本文書は、次を境界として成立させる。

```text
Canonical Primary Language Support Association exists
≠
Documentation Presentation
```

すなわち、あるEnglish Representation（英語表現）についてCanonical Primary Language Support Association（正規主要言語補助対応）が成立していることは、Canonical Primary Language Support Representation（正規主要言語補助表現）がすべてのConcrete Usage Occurrenceへ表示されることを意味しない。逆に、ある使用箇所へ表示されていないことは、そのAssociation（対応）が成立していないことを意味しない。

どの箇所で表示するかを定めるPresentation Ruleは、本文書が定義しない。本文書が保持するのは、この境界のみである。

## Design Principles（設計原則）

本節が示すのは、本文書が定義するSemantic Model（意味モデル）の内部で成立するLocal Design Principle（局所設計原則）である。Philosophy Area（思想領域）が所有するFundamental Principle（根本原則）ではない。

### Association over Classification（分類ではなく対応）

Canonical Primary Language Support（正規主要言語補助）は、English Representation（英語表現）に対するSemantic Classificationを成立させない。成立させるのは、対応元と対応先のAssociation（対応）のみである。

### Support without Redefinition（補助は再定義しない）

Canonical Primary Language Support Representation（正規主要言語補助表現）は、English Representation（英語表現）そのもの、およびUnderlying Meaning（対象の意味）を再定義しない。担うのはPrimary Languageによる理解補助のみである。

### Current Need Only（現在必要な範囲だけを定義する）

本Modelは、English Representation（英語表現）からPrimary Language Representation（主要言語表現）へのSupport Associationのみを扱う。Translation一般、Localization一般へ拡張しない。

### Availability and Presentation Separation（利用可能性と表示の分離）

Canonical Primary Language Support Association（正規主要言語補助対応）が成立していることと、Concrete Documentation Presentationとを分離して扱う。

## Usage by Downstream Design（下位設計からの参照）

本文書を上位Sourceとする下位設計は、次を本文書側の定義として参照する。

- Canonical Primary Language Support Association（正規主要言語補助対応）が何を表す関係であるか
- 同Association（対応）のMultiplicity（多重度）
- 本文書が保持するDefinition Authority BoundaryおよびAvailability / Presentation Boundary

次は本文書から判断できない。下位設計が自身の責務として決定する。

- 個々のEnglish Representation（英語表現）に対するCanonical Primary Language Support Representation（正規主要言語補助表現）の値
- Canonical Primary Language Support Representation（正規主要言語補助表現）をどの箇所で表示するか
