# Canonical Japanese Support Architecture（正規日本語補助アーキテクチャ）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Documentation（Repository文書）で使用される
English Representation（英語表現）について、
そのEnglish Representation（英語表現）の理解を日本語で補助するために
Repositoryが一貫して再利用する
Japanese Representation（日本語表現）** との対応を定義する
Architecture Asset（アーキテクチャ資産）である。

本文書が扱う問いは次の4点である。

1. English Representation（英語表現）と、その理解補助として
   Repositoryが一貫して再利用する
   Japanese Representation（日本語表現）との対応は、
   何によって成立するのか。
2. その対応は、English Representation1つに対して
   いくつ成立するのか。
3. その対応を成立させることは、
   English Representation（英語表現）そのものの意味、および
   English Representation（英語表現）が指す
   Underlying Meaning（対象の意味）を
   定めることとどこで分かれるのか。
4. その対応が成立していることと、
   Concrete Usage Occurrenceで
   Japanese Representation（日本語表現）が
   表示されることは、どこで分かれるのか。

本文書が定義するのは、この対応を成立させる
Architecture-level Semantic Modelである。
個々のEnglish Representation（英語表現）に対する
具体的なJapanese Representation（日本語表現）の値は、
本文書が定義しない。

本文書は、Formal Terminology Management、
Translation Management、
Naming Managementを責務としない。

## Relationships（関係）

本文書は
[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)
が定義するArchitecture Area（アーキテクチャ領域）に属する
通常のDocumentation Asset（文書資産）である。
同AreaのArea Responsibility（領域責務）である
Semantic / Structural Modelの定義として、
本文書はCanonical Japanese Support Association（正規日本語補助対応）を
成立させるConcept（概念）・Relationship・
Boundary（境界）・Definition Authority（定義権限）を定義する。
Areaを代表・集約するAssetではない。

```text
Repository Governance Documentation Framework
        ▲
        │ belongs to
Canonical Japanese Support Architecture
```

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Definition Authority（定義権限）
- Documentation Area（文書責務領域）と
  Area Responsibility（領域責務）

### Position（設計上の位置づけ）

本文書は
[Documentation Structure Architecture](documentation-structure.md)
を上位Sourceとして参照する。

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ presupposes
Canonical Japanese Support Architecture
```

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 本文書が対応元として扱う
  English Representation（英語表現）の局所的な意味
- Canonical Japanese Support Representation（正規日本語補助表現）が
  何によって成立するか
- Canonical Japanese Support Association（正規日本語補助対応）が
  何を表す関係であるか
- 同Association（対応）について現在必要な
  Multiplicity（多重度）
- Canonical Japanese Support Representation（正規日本語補助表現）と、
  English Representation（英語表現）そのものとの
  Definition Authority Boundary
- Canonical Japanese Support Representation（正規日本語補助表現）と、
  Underlying Meaning（対象の意味）との
  Definition Authority Boundary
- Canonical Japanese Support Representation（正規日本語補助表現）と、
  別のSubjectについての
  Definition Responsibility（定義責務）が定義する
  Human-readable Representation（人間可読表現）との
  Definition Authority Boundary
- Architecture-level Semantic Modelと
  Individual Canonical Valueとの
  Definition Authority Boundary
- Canonical Japanese Support Association（正規日本語補助対応）の成立と、
  Documentation Presentation（文書上の表示）との
  Boundary（境界）

### Out of Scope（本文書が定義しない範囲）

- English Representation（英語表現）のIdentity（同一性）、
  Meaning（意味）、Formal Status（正式地位）、
  Category（分類）、およびNameとしての地位
- English Representation（英語表現）が指す
  Underlying Meaning（対象の意味）そのもの
- 個々のEnglish Representation（英語表現）と
  個々のCanonical Japanese Support Representation（正規日本語補助表現）との
  具体的な対応の値
- 別のSubjectについての
  Definition Responsibility（定義責務）が定義する
  Human-readable Representation（人間可読表現）そのもの、および
  そのLanguage-specific Representation
- Subject-specific Representationまたは
  Local Presentationの詳細Model
- Japanese Representation（日本語表現）側から見た
  逆方向のMultiplicity（多重度）
- Title・Heading（見出し）・Body、初出、常時表示等の
  Presentation Rule
- Registry・Schema・Field・
  Stable Identifier等の管理機構
- Workflow、Actor Model、
  Candidate Detection、Occurrence Count（出現回数）
- Alias・Synonym、Lifecycle、
  Versioning（版管理）
- English Representation（英語表現）以外の言語、または
  Japanese Representation（日本語表現）以外の言語を対象とする
  Generic Translation Model、
  Generic Language Map、
  Localization Model
- Validator・Linter・CLI・CI等のTool要求

本節が示すのは、本文書がDefinition Authority（定義権限）を
持たない範囲である。
本節は、ここに挙げた事項の存在または導入を
禁止するものではない。

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
Canonical Japanese Support Representation
```

この矢印が表すRelationshipを
Canonical Japanese Support Association（正規日本語補助対応）と呼ぶ。

本Modelが保持するConcept（概念）は
次の3つのみである。

- English Representation（英語表現）
- Canonical Japanese Support Representation（正規日本語補助表現）
- Canonical Japanese Support Association（正規日本語補助対応）

### English Representation（英語表現）

English Representation（英語表現）は、
Repository Documentation（Repository文書）で意図的に使用され、
本Modelにおいて
Canonical Japanese Support Association（正規日本語補助対応）の
対応元として扱われ得る英語によるRepresentation（表現）である。

本文書はEnglish Representation（英語表現）を、
本Modelが対応元を指し示すために必要な範囲の
Local Input Conceptとして扱う。

したがって本文書は、
English Representation（英語表現）について次を定義しない。

- Identity（同一性）
- Meaning（意味）
- Formal Status（正式地位）
- Category（分類）
- Nameとしての地位

本文書は、これらを担う独立したConcept（概念）を
本Modelへ導入しない。

### Canonical Japanese Support Representation（正規日本語補助表現）

Canonical Japanese Support Representation（正規日本語補助表現）は、
特定のEnglish Representation（英語表現）の理解を日本語で補助するため、
そのEnglish Representation（英語表現）との
Canonical Japanese Support Association（正規日本語補助対応）において
Repositoryが一貫して再利用する
Japanese Representation（日本語表現）である。

Canonicalityは、
Japanese Representation（日本語表現）単体に対して成立しない。
成立するのは、特定のEnglish Representation（英語表現）との
Association（対応）に対してである。
同じ語形のJapanese Representation（日本語表現）が
別のEnglish Representation（英語表現）との
Association（対応）においてCanonicalであるかどうかは、
そのAssociation（対応）ごとに定まる。

本文書は、次の境界を保持する。

```text
Canonical Japanese Support Representation
≠ English RepresentationのIdentity
≠ Underlying MeaningのDefinition
≠ Translationとして唯一正しい表現
```

Canonical Japanese Support Representation（正規日本語補助表現）が
成立していることは、
そのJapanese Representation（日本語表現）が
Translationとして唯一正しいことを意味しない。
成立しているのは、Repositoryが理解補助として
一貫して再利用するという対応のみである。

### Canonical Japanese Support Association（正規日本語補助対応）

Canonical Japanese Support Association（正規日本語補助対応）は、
English Representation（英語表現）と、
その理解補助としてRepositoryが一貫して再利用すると決定した
Canonical Japanese Support Representation（正規日本語補助表現）との
Relationshipである。

### Association Establishment（対応の成立）

Canonical Japanese Support Association（正規日本語補助対応）は、
Repositoryが、特定のEnglish Representation（英語表現）に対して
一貫して再利用するJapanese Representation（日本語表現）を
Canonicalとして決定したときに成立する。

本文書は、この成立を上記Relationshipの意味として扱い、
成立可否を判定する独立したConcept（概念）を導入しない。
Occurrence Count（出現回数）、Candidate Detection、
Formal Status（正式地位）等の付随的な性質から
成立を導出しない。

### Multiplicity（多重度）

本文書が定義するMultiplicity（多重度）は、
現在必要な方向のみである。

```text
1 English Representation
    → 0..1 Canonical Japanese Support Representation
```

これが意味するのは次の2点である。

- あるEnglish Representation（英語表現）について
  Japanese Supportが必要でない場合、
  Canonical Japanese Support Association（正規日本語補助対応）は
  存在しなくてよい。
- Canonical Japanese Support Association（正規日本語補助対応）が
  成立する場合、そのEnglish Representation（英語表現）に対する
  Canonical Japanese Support Representation（正規日本語補助表現）は
  1つである。

Japanese Representation（日本語表現）側から見た
逆方向のMultiplicity（多重度）は、
現在のNeedから導出されないため、
本文書は定義しない。
定義しないことは、
逆方向に制約が存在しないことを意味しない。

## Responsibility Boundary（責務境界）

### Boundary with English Representation and Underlying Meaning（English RepresentationおよびUnderlying Meaningとの境界）

本文書がDefinition Responsibility（定義責務）を持つのは、
Canonical Japanese Support Association（正規日本語補助対応）を
成立させるConcept（概念）・Relationship・
Boundary（境界）のみである。

```text
English Representationそのもの
Underlying Meaning
        ↓
それぞれの対象を所有する既存のDefinition Authority

Canonical Japanese Support Associationの
Concept・Relationship・Boundary
        ↓
本文書のDefinition Responsibility
```

したがって、あるEnglish Representation（英語表現）が
Canonical Japanese Support Representation（正規日本語補助表現）を
伴っていることは、
そのJapanese Representation（日本語表現）が
English Representation（英語表現）そのもの、または
Underlying Meaning（対象の意味）を
確定させていることを意味しない。
意味の確定は、常にその対象を所有する
Definition Authority（定義権限）側にある。

本文書は、English Representation（英語表現）および
Underlying Meaning（対象の意味）に関する
Definition Authority（定義権限）の一般Modelを
新たに設計しない。

### Boundary with Human-readable Representation Defined by Another Subject（別のSubjectが定義するHuman-readable Representationとの境界）

Canonical Japanese Support（正規日本語補助）が扱うのは、
Repository Documentation（Repository文書）で使用される
English Representation（英語表現）の理解を補助するために
Repository横断で再利用される
Japanese Reading Supportである。

Human-readable Representation（人間可読表現）そのものが、
別のSubjectについての
Definition Responsibility（定義責務）の一部として
定義されている場合がある。
この場合、そのRepresentation（表現）の
Language-specific Representationを定めるのは、
そのSubjectを所有する
Definition Authority（定義権限）側である。

```text
別のSubjectについての
Definition Responsibilityが定義する
Human-readable Representation
        ↓
そのSubjectを所有するDefinition Authority

English Representationの理解補助として
Repository横断で再利用される
Japanese Reading Support
        ↓
本文書が成立させる
Canonical Japanese Support Association
```

したがって、そのようなRepresentation（表現）は
本文書のDefinition Authority（定義権限）の外にある。
本文書は、それを定義・置換・上書きしない。

また、あるRepresentation（表現）が
English Representation（英語表現）と
同じSurface Formであること、または
あるJapanese Representation（日本語表現）が
Canonical Japanese Support Representation（正規日本語補助表現）と
同じJapanese Valueであることは、
それだけでは同じSemantic Responsibility（意味上の責務）を意味しない。
本文書は、Surface Formの一致、または
Japanese Valueの一致のみから
Canonical Japanese Support Association（正規日本語補助対応）の成立を
推論しない。

本文書は、そのようなRepresentation（表現）が
どのように定義または表示されるかについての
Modelを新たに設計しない。

### Boundary between Architecture-level Semantic Model and Individual Canonical Value（Architecture-level Semantic ModelとIndividual Canonical Valueとの境界）

本文書は、Architecture-level Definitionと
Individual Canonical Valueを分離する。

```text
Canonical Japanese Supportの
Concept・Relationship・Boundary
    → 本文書

個々のEnglish Representation
    ↔
個々のCanonical Japanese Support Representation
という具体的なCanonical Associationとその値
    → 下位のDefinition-holding Asset
```

本文書は、

```text
Design Dependency → 設計依存
```

のような個別のPairを定義しない。
本文書が成立させるのは、そのようなPairが
何であるかを説明するModelである。

## Availability / Presentation Boundary（利用可能性と表示の境界）

Documentation Presentation（文書上の表示）は、
Canonical Japanese Support Representation（正規日本語補助表現）が
Concrete Usage Occurrenceへ
実際に現れることである。

本文書は、次を境界として成立させる。

```text
Canonical Japanese Support Association exists
≠
Documentation Presentation
```

すなわち、あるEnglish Representation（英語表現）について
Canonical Japanese Support Association（正規日本語補助対応）が
成立していることは、
Canonical Japanese Support Representation（正規日本語補助表現）が
すべてのConcrete Usage Occurrenceへ
表示されることを意味しない。
逆に、ある使用箇所へ表示されていないことは、
そのAssociation（対応）が成立していないことを意味しない。

どの箇所で表示するかを定めるPresentation Ruleは、
本文書が定義しない。
本文書が保持するのは、この境界のみである。

## Design Principles（設計原則）

本節が示すのは、本文書が定義する
Semantic Model（意味モデル）の内部で成立する
Local Design Principle（局所設計原則）である。
Philosophy Area（思想領域）が所有する
Fundamental Principle（根本原則）ではない。

### Association over Classification（分類ではなく対応）

Canonical Japanese Support（正規日本語補助）は、
English Representation（英語表現）に対する
Semantic Classificationを成立させない。
成立させるのは、対応元と対応先の
Association（対応）のみである。

### Support without Redefinition（補助は再定義しない）

Canonical Japanese Support Representation（正規日本語補助表現）は、
English Representation（英語表現）そのもの、および
Underlying Meaning（対象の意味）を再定義しない。
担うのは日本語による理解補助のみである。

### Current Need Only（現在必要な範囲だけを定義する）

本Modelは、English Representation（英語表現）から
Japanese Representation（日本語表現）への
Support Associationのみを扱う。
Translation一般、
Localization一般へ拡張しない。

### Availability and Presentation Separation（利用可能性と表示の分離）

Canonical Japanese Support Association（正規日本語補助対応）が
成立していることと、
Concrete Documentation Presentationとを
分離して扱う。

## Usage by Downstream Design（下位設計からの参照）

本文書を上位Sourceとする下位設計は、
次を本文書側の定義として参照する。

- Canonical Japanese Support Association（正規日本語補助対応）が
  何を表す関係であるか
- 同Association（対応）のMultiplicity（多重度）
- 本文書が保持するDefinition Authority Boundaryおよび
  Availability / Presentation Boundary

次は本文書から判断できない。
下位設計が自身の責務として決定する。

- 個々のEnglish Representation（英語表現）に対する
  Canonical Japanese Support Representation（正規日本語補助表現）の値
- Canonical Japanese Support Representation（正規日本語補助表現）を
  どの箇所で表示するか
