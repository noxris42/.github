# Canonical Japanese Support Architecture（正規日本語補助のArchitecture）

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
2. その対応は、English Representation（英語表現）1つに対して
   いくつ成立するのか。
3. その対応を成立させることは、
   English Representation（英語表現）そのものの意味、および
   English Representation（英語表現）が指す
   Underlying Meaning（対象の意味）を
   定めることとどこで分かれるのか。
4. その対応が成立していることと、
   Concrete Usage Occurrence（具体使用箇所）で
   Japanese Representation（日本語表現）が
   表示されることは、どこで分かれるのか。

本文書が定義するのは、この対応を成立させる
Architecture-level Semantic Model（アーキテクチャレベル意味モデル）である。
個々のEnglish Representation（英語表現）に対する
具体的なJapanese Representation（日本語表現）の値は、
本文書が定義しない。

本文書は、Formal Terminology Management（正式用語管理）、
Translation Management（翻訳管理）、
Naming Management（名称管理）を責務としない。

## Position（上位Architectureとの関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Documentation Structure Architecture](documentation-structure.md)
- [Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture（文書構造の一般意味モデル）
        ▲
        │ presupposes（前提として使用する）
Canonical Japanese Support Architecture（本文書）

Repository Governance Documentation Framework Architecture
（文書体系と領域責務）
        ▲
        │ belongs to（Architecture Areaに属する）
Canonical Japanese Support Architecture（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)
が定義するArchitecture Area（アーキテクチャ領域）に属する
通常のDocumentation Asset（文書資産）である。
同Area（領域）のArea Responsibility（領域責務）である
Semantic / Structural Model（意味・構造モデル）の定義として、
本文書はCanonical Japanese Support Association（正規日本語補助対応）を
成立させるConcept（概念）・Relationship（関係）・
Boundary（境界）・Definition Authority（定義権限）を定義する。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Definition Authority（定義権限）
- Documentation Area（文書責務領域）と
  Area Responsibility（領域責務）

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
  Definition Authority Boundary（定義権限境界）
- Canonical Japanese Support Representation（正規日本語補助表現）と、
  Underlying Meaning（対象の意味）との
  Definition Authority Boundary（定義権限境界）
- Canonical Japanese Support Representation（正規日本語補助表現）と、
  別のSubject（別対象）についての
  Definition Responsibility（定義責務）が定義する
  Human-readable Representation（人間可読表現）との
  Definition Authority Boundary（定義権限境界）
- Architecture-level Semantic Model（アーキテクチャレベル意味モデル）と
  Individual Canonical Value（個別正規値）との
  Definition Authority Boundary（定義権限境界）
- Canonical Japanese Support Association（正規日本語補助対応）の成立と、
  Documentation Presentation（文書上の表示）との
  Boundary（境界）

### Out of Scope（本文書が定義しない範囲）

- English Representation（英語表現）のIdentity（同一性）、
  Meaning（意味）、Formal Status（正式地位）、
  Category（分類）、およびName（名称）としての地位
- English Representation（英語表現）が指す
  Underlying Meaning（対象の意味）そのもの
- 個々のEnglish Representation（英語表現）と
  個々のCanonical Japanese Support Representation（正規日本語補助表現）との
  具体的な対応の値
- 別のSubject（別対象）についての
  Definition Responsibility（定義責務）が定義する
  Human-readable Representation（人間可読表現）そのもの、および
  そのLanguage-specific Representation（言語固有表現）
- Subject-specific Representation（対象固有表現）または
  Local Presentation（局所表示）の詳細Model（詳細モデル）
- Japanese Representation（日本語表現）側から見た
  逆方向のMultiplicity（多重度）
- Title（題名）・Heading（見出し）・Body（本文）、初出、常時表示等の
  Presentation Rule（表示規則）
- Registry（登録簿）・Schema（スキーマ）・Field（フィールド）・
  Stable Identifier（安定識別子）等の管理機構
- Workflow（作業手順）、Actor Model（主体モデル）、
  Candidate Detection（候補検出）、Occurrence Count（出現回数）
- Alias（別名）・Synonym（同義語）、Lifecycle（生存期間）、
  Versioning（版管理）
- English Representation（英語表現）以外の言語、または
  Japanese Representation（日本語表現）以外の言語を対象とする
  Generic Translation Model（汎用翻訳モデル）、
  Generic Language Map（汎用言語対応表）、
  Localization Model（地域化モデル）
- Validator（検証器）・Linter・CLI・CI等のTool（ツール）要求

本節が示すのは、本文書がDefinition Authority（定義権限）を
持たない範囲である。
本節は、ここに挙げた事項の存在または導入を
禁止するものではない。

## Concept Model（概念モデル）

### Model全体像

本文書が成立させるModel（モデル）は次である。

```text
English Representation（英語表現）
        │
        │ 0..1
        │ is canonically supported by
        │ （正規日本語補助対応を持つ）
        ▼
Canonical Japanese Support Representation（正規日本語補助表現）
```

この矢印が表すRelationship（関係）を
Canonical Japanese Support Association（正規日本語補助対応）と呼ぶ。

本Model（モデル）が保持するConcept（概念）は
次の3つのみである。

- English Representation（英語表現）
- Canonical Japanese Support Representation（正規日本語補助表現）
- Canonical Japanese Support Association（正規日本語補助対応）

### English Representation（英語表現）

English Representation（英語表現）は、
Repository Documentation（Repository文書）で意図的に使用され、
本Model（モデル）において
Canonical Japanese Support Association（正規日本語補助対応）の
対応元として扱われ得る英語によるRepresentation（表現）である。

本文書はEnglish Representation（英語表現）を、
本Model（モデル）が対応元を指し示すために必要な範囲の
Local Input Concept（局所的入力概念）として扱う。

したがって本文書は、
English Representation（英語表現）について次を定義しない。

- Identity（同一性）
- Meaning（意味）
- Formal Status（正式地位）
- Category（分類）
- Name（名称）としての地位

本文書は、これらを担う独立したConcept（概念）を
本Model（モデル）へ導入しない。

### Canonical Japanese Support Representation（正規日本語補助表現）

Canonical Japanese Support Representation（正規日本語補助表現）は、
特定のEnglish Representation（英語表現）の理解を日本語で補助するため、
そのEnglish Representation（英語表現）との
Canonical Japanese Support Association（正規日本語補助対応）において
Repositoryが一貫して再利用する
Japanese Representation（日本語表現）である。

Canonicality（正規性）は、
Japanese Representation（日本語表現）単体に対して成立しない。
成立するのは、特定のEnglish Representation（英語表現）との
Association（対応）に対してである。
同じ語形のJapanese Representation（日本語表現）が
別のEnglish Representation（英語表現）との
Association（対応）においてCanonical（正規）であるかどうかは、
そのAssociation（対応）ごとに定まる。

本文書は、次の境界を保持する。

```text
Canonical Japanese Support Representation（正規日本語補助表現）
≠ English Representation（英語表現）のIdentity（同一性）
≠ Underlying Meaning（対象の意味）のDefinition（定義）
≠ Translation（翻訳）として唯一正しい表現
```

Canonical Japanese Support Representation（正規日本語補助表現）が
成立していることは、
そのJapanese Representation（日本語表現）が
Translation（翻訳）として唯一正しいことを意味しない。
成立しているのは、Repositoryが理解補助として
一貫して再利用するという対応のみである。

### Canonical Japanese Support Association（正規日本語補助対応）

Canonical Japanese Support Association（正規日本語補助対応）は、
English Representation（英語表現）と、
その理解補助としてRepositoryが一貫して再利用すると決定した
Canonical Japanese Support Representation（正規日本語補助表現）との
Relationship（関係）である。

### Association Establishment（対応の成立）

Canonical Japanese Support Association（正規日本語補助対応）は、
Repositoryが、特定のEnglish Representation（英語表現）に対して
一貫して再利用するJapanese Representation（日本語表現）を
Canonical（正規）として決定したときに成立する。

本文書は、この成立を上記Relationship（関係）の意味として扱い、
成立可否を判定する独立したConcept（概念）を導入しない。
Occurrence Count（出現回数）、Candidate Detection（候補検出）、
Formal Status（正式地位）等の付随的な性質から
成立を導出しない。

### Multiplicity（多重度）

本文書が定義するMultiplicity（多重度）は、
現在必要な方向のみである。

```text
1 English Representation（英語表現）
    → 0..1 Canonical Japanese Support Representation（正規日本語補助表現）
```

これが意味するのは次の2点である。

- あるEnglish Representation（英語表現）について
  Japanese Support（日本語補助）が必要でない場合、
  Canonical Japanese Support Association（正規日本語補助対応）は
  存在しなくてよい。
- Canonical Japanese Support Association（正規日本語補助対応）が
  成立する場合、そのEnglish Representation（英語表現）に対する
  Canonical Japanese Support Representation（正規日本語補助表現）は
  1つである。

Japanese Representation（日本語表現）側から見た
逆方向のMultiplicity（多重度）は、
現在のNeed（必要性）から導出されないため、
本文書は定義しない。
定義しないことは、
逆方向に制約が存在しないことを意味しない。

## Definition Authority Boundary（定義権限境界）

### English Representation（英語表現）およびUnderlying Meaning（対象の意味）との境界

本文書がDefinition Responsibility（定義責務）を持つのは、
Canonical Japanese Support Association（正規日本語補助対応）を
成立させるConcept（概念）・Relationship（関係）・
Boundary（境界）のみである。

```text
English Representation（英語表現）そのもの
Underlying Meaning（対象の意味）
        ↓
それぞれの対象を所有する既存のDefinition Authority（定義権限）

Canonical Japanese Support Association（正規日本語補助対応）の
Concept（概念）・Relationship（関係）・Boundary（境界）
        ↓
本文書のDefinition Responsibility（定義責務）
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
Definition Authority（定義権限）の一般Model（一般モデル）を
新たに設計しない。

### 別のSubject（別対象）が定義するHuman-readable Representation（人間可読表現）との境界

Canonical Japanese Support（正規日本語補助）が扱うのは、
Repository Documentation（Repository文書）で使用される
English Representation（英語表現）の理解を補助するために
Repository横断で再利用される
Japanese Reading Support（日本語読解補助）である。

Human-readable Representation（人間可読表現）そのものが、
別のSubject（別対象）についての
Definition Responsibility（定義責務）の一部として
定義されている場合がある。
この場合、そのRepresentation（表現）の
Language-specific Representation（言語固有表現）を定めるのは、
そのSubject（対象）を所有する
Definition Authority（定義権限）側である。

```text
別のSubject（別対象）についての
Definition Responsibility（定義責務）が定義する
Human-readable Representation（人間可読表現）
        ↓
そのSubject（対象）を所有するDefinition Authority（定義権限）

English Representation（英語表現）の理解補助として
Repository横断で再利用される
Japanese Reading Support（日本語読解補助）
        ↓
本文書が成立させる
Canonical Japanese Support Association（正規日本語補助対応）
```

したがって、そのようなRepresentation（表現）は
本文書のDefinition Authority（定義権限）の外にある。
本文書は、それを定義・置換・上書きしない。

また、あるRepresentation（表現）が
English Representation（英語表現）と
同じSurface Form（表層形式）であること、または
あるJapanese Representation（日本語表現）が
Canonical Japanese Support Representation（正規日本語補助表現）と
同じJapanese Value（日本語値）であることは、
それだけでは同じSemantic Responsibility（意味上の責務）を意味しない。
本文書は、Surface Form（表層形式）の一致、または
Japanese Value（日本語値）の一致のみから
Canonical Japanese Support Association（正規日本語補助対応）の成立を
推論しない。

本文書は、そのようなRepresentation（表現）が
どのように定義または表示されるかについての
Model（モデル）を新たに設計しない。

### Architecture-level Semantic Model（アーキテクチャレベル意味モデル）とIndividual Canonical Value（個別正規値）との境界

本文書は、Architecture-level Definition（アーキテクチャレベル定義）と
Individual Canonical Value（個別正規値）を分離する。

```text
Canonical Japanese Support（正規日本語補助）の
Concept（概念）・Relationship（関係）・Boundary（境界）
    → 本文書

個々のEnglish Representation（英語表現）
    ↔
個々のCanonical Japanese Support Representation（正規日本語補助表現）
という具体的なCanonical Association（正規対応）とその値
    → 下位のDefinition-holding Asset（定義保持資産）
```

本文書は、

```text
Design Dependency → 設計依存
```

のような個別のPair（個別対応）を定義しない。
本文書が成立させるのは、そのようなPair（個別対応）が
何であるかを説明するModel（モデル）である。

## Availability / Presentation Boundary（利用可能性と表示の境界）

Documentation Presentation（文書上の表示）は、
Canonical Japanese Support Representation（正規日本語補助表現）が
Concrete Usage Occurrence（具体使用箇所）へ
実際に現れることである。

本文書は、次を境界として成立させる。

```text
Canonical Japanese Support Association exists
（Canonical Japanese Support Association（正規日本語補助対応）が
成立している）
≠
Documentation Presentation
（Concrete Usage Occurrence（具体使用箇所）で表示される）
```

すなわち、あるEnglish Representation（英語表現）について
Canonical Japanese Support Association（正規日本語補助対応）が
成立していることは、
Canonical Japanese Support Representation（正規日本語補助表現）が
すべてのConcrete Usage Occurrence（具体使用箇所）へ
表示されることを意味しない。
逆に、ある使用箇所へ表示されていないことは、
そのAssociation（対応）が成立していないことを意味しない。

どの箇所で表示するかを定めるPresentation Rule（表示規則）は、
本文書が定義しない。
本文書が保持するのは、この境界のみである。

## Design Principles（設計原則）

本節が示すのは、本文書が定義する
Semantic Model（意味モデル）の内部で成立する
Local Design Principle（局所設計原則）である。
Philosophy Area（思想領域）が所有する
Fundamental Principle（根本原則）ではない。

### 1. Association over Classification（分類ではなく対応）

Canonical Japanese Support（正規日本語補助）は、
English Representation（英語表現）に対する
Semantic Classification（意味上の分類）を成立させない。
成立させるのは、対応元と対応先の
Association（対応）のみである。

### 2. Support without Redefinition（補助は再定義しない）

Canonical Japanese Support Representation（正規日本語補助表現）は、
English Representation（英語表現）そのもの、および
Underlying Meaning（対象の意味）を再定義しない。
担うのは日本語による理解補助のみである。

### 3. Current Need Only（現在必要な範囲だけを定義する）

本Model（モデル）は、English Representation（英語表現）から
Japanese Representation（日本語表現）への
Support Association（補助対応）のみを扱う。
Translation（翻訳）一般、
Localization（地域化）一般へ拡張しない。

### 4. Availability and Presentation Separation（利用可能性と表示の分離）

Canonical Japanese Support Association（正規日本語補助対応）が
成立していることと、
Concrete Documentation Presentation（具体的な文書上の表示）とを
分離して扱う。

## Usage by Downstream Design（下位設計からの参照）

本文書を上位Source（上位の情報源）とする下位設計は、
次を本文書側の定義として参照する。

- Canonical Japanese Support Association（正規日本語補助対応）が
  何を表す関係であるか
- 同Association（対応）のMultiplicity（多重度）
- 本文書が保持するDefinition Authority Boundary（定義権限境界）および
  Availability / Presentation Boundary（利用可能性と表示の境界）

次は本文書から判断できない。
下位設計が自身の責務として決定する。

- 個々のEnglish Representation（英語表現）に対する
  Canonical Japanese Support Representation（正規日本語補助表現）の値
- Canonical Japanese Support Representation（正規日本語補助表現）を
  どの箇所で表示するか
