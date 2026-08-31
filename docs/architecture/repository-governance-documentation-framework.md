# Repository Governance Documentation Framework（Repository統治文書体系）

## Purpose（目的）

本文書は、`noxris42` が現在採用する具体的な
Documentation Framework（文書体系）である
**Repository Governance Documentation Framework**
を定義する。

本文書が扱う問いは次の3点である。

1. 本Framework（体系）は、Documentation全体として何を成立させるのか
   — Framework Responsibility（体系責務）。
2. その責務は、どのDocumentation Area（文書責務領域）へ分解されるのか
   （Area Composition）。
3. 各Areaは何を所有し、何を所有しないのか
   — Area Responsibility（領域責務）。

本文書は、Areaの責務と構成を定義する。
個々のDocumentation Asset（文書資産）の内容、
記述方法、命名規則は定義しない。

## Relationships（関係）

### Relationship with Documentation Structure Architecture（Documentation Structure Architectureとの関係）

#### Position（設計上の位置づけ）

本文書は
[Documentation Structure Architecture](documentation-structure.md)
を上位Sourceとして参照する。

同Architectureは、
Documentation Framework（文書体系）・
Documentation Area（文書責務領域）・
Documentation Asset（文書資産）と、
それぞれの責務および責務粒度、
ならびにLogical / Physical Boundaryを定義する。
本文書はこれらを再定義せず、前提として使用する。

```text
Documentation Structure Architecture
        ▲
        │ refines
Repository Governance Documentation Framework
```

本文書が具体化するのは、
**一つの具体的なDocumentation Framework（文書体系）** である。
Documentation Structure（文書構造）の一般Modelを拡張・上書きしない。

#### Relationship with Document Responsibility（Document Responsibilityとの関係）

同Architectureにおける
Document Responsibility（文書責務）は、
Documentation Asset（文書資産）が
Documentation上で何を保持・提供する責務を担うかを示す一般Concept（概念）であり、
Definition（定義）を保持する責務に限定されない。

本Framework（体系）は、
そのうち
**正式なDefinition（定義）を保持する責務**
に着目した体系である。
本文書ではこれを
Definition Responsibility（定義責務）と呼ぶ。

```text
Documentation Structure Architecture
    Document Responsibility
    = Documentation Asset一般の責務

Repository Governance Documentation Framework
    Definition Responsibility
    = 正式Definitionを保持する責務
```

Definition Responsibility（定義責務）は、
Document Responsibility（文書責務）の一般Concept（概念）を
本Framework（体系）の範囲において具体化したものである。
一般Concept（概念）を置き換えるものではない。

#### Relationship with Area Responsibility（Area Responsibilityとの関係）

同Architectureにおける
Area Responsibility（領域責務）は、
Documentation Area（文書責務領域）が
どのような種類のDocument Responsibility（文書責務）を担うかを示す
一般Concept（概念）であり、
Definition（定義）を担う責務へ限定されない。

本Framework（体系）は、
その一般Concept（概念）を本Framework（体系）の範囲において具体化し、
**Definition Responsibility（定義責務）の種類による領域分割**
としてAreaを構成する。

```text
Documentation Structure Architecture
    Area Responsibility
    = Document Responsibility一般の責務領域

Repository Governance Documentation Framework
    Area Responsibilities
    = Definition Responsibilityの種類による領域分割
```

これは本Framework（体系）が
Definition（定義）中心の体系であることによる具体化であり、
Documentation Structure（文書構造）一般の要求ではない。

#### Area Membership Handling（Area所属の扱い）

同Architectureは、
すべてのDocumentation Asset（文書資産）が
Documentation Area（文書責務領域）へ所属することを要求しない。

本Framework（体系）は、
**本Framework（体系）に属する
Documentation Asset（文書資産）** について、
4つのAreaのいずれかへ所属するModelを採る。

これは本Framework（体系）の範囲における判断であり、
Documentation Structure（文書構造）一般の要求ではない。

### Responsibility Boundary（責務境界）

[Repository Governance](repository-governance.md)
は、
**本文書とは別Subject** を扱う。

| 文書 | 扱うSubject |
| --- | --- |
| Repository Governance | Repository間のOwnership（所有責任）、Shared Development Foundation、Foundation Application、Repository-specific Responsibility |
| 本文書 | Documentation Framework（文書体系）、Area Composition、Area Responsibility（領域責務）、Documentation上のDefinition Responsibility（定義責務）の分離 |

名称および用語が類似することを理由に、両者を統合しない。

Repository Governanceは
**Repositoryを跨ぐ所有と適用の関係** を扱い、
本文書は
**Documentation上で定義責務をどう分離するか** を扱う。

本文書は、Repository Governanceが定義する
Ownership（所有責任）・Shared Scope・
Foundation Applicationを
再定義・上書きしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 本Framework（体系）のFramework Responsibility（体系責務）
- Area Composition
- 各AreaのArea Responsibility（領域責務）、
  およびOwns／Does Not Own
- Area間の境界判断の基準
- 現在採用するPhysical Representation（物理表現）

### Out of Scope（本文書が定義しない範囲）

- 個々のDocumentation Asset（文書資産）の内容
- Documentation Asset（文書資産）の命名、Path、File構成に関する
  Normative Rule（規範的規則）
- Area間の固定的なLayer Hierarchyや
  一般的な依存規則
- 他のDocumentation Framework（文書体系）との
  Composition・Priority・Refinement（具体化）
- MetadataおよびDeclarationのSchema
- Documentation Lifecycle（文書の生涯管理）・Review・Validation

詳細は「Non-goals」に示す。

## Framework Responsibility（体系責務）

Repository Governance Documentation Frameworkは、
次のFramework Responsibility（体系責務）を担う。

> Repository、およびRepositoryで管理・実施される対象について、
> 正式な判断根拠となるDefinition（定義）を、
> その **Semantic Responsibility（意味上の責務）の違い** に応じて分離し、
> Documentation上の責務体系として保持する。

この責務分離により、
各Definition（定義）について次が追跡可能になる。

- そのDefinition（定義）のDefinition Authority（定義権限）が
  どのDocumentation Asset（文書資産）にあるか。
- そのDefinition（定義）が、どの定義を根拠とし、
  どの定義を具体化するか。

### Traceability Positioning（Traceabilityの位置づけ）

Traceabilityは、
本Framework（体系）の最上位目的ではない。

本Framework（体系）が第一に行うのは
**Semantic Responsibility（意味上の責務）による分離** であり、
Traceabilityは
その分離の結果として成立する性質として扱う。

したがって、Traceabilityを高めること自体を根拠として、
責務分離に反する構造を導入しない。

## Area Composition（領域構成）

本Framework（体系）は、次の4つの
Documentation Area（文書責務領域）から構成される。

```text
Repository Governance Documentation Framework
│
├─ Philosophy Area
├─ Architecture Area
├─ Conventions Area
└─ Specifications Area
```

### Do Not Define Enumeration Order as Hierarchy（列挙順をHierarchyとして定義しない）

上記の列挙順は、
**Linear Layer Hierarchyではない** 。

本文書は、Area間に固定的な上下関係・依存順序を定義しない。

Area間のDependency（依存）は、
個々のDefinition（定義）が持つ
Semantic Need（意味上の必要性）から個別に成立する。
すなわち、あるDefinition（定義）が
他のDefinition（定義）を根拠として必要とする場合に、
その関係として依存が成立する。
Areaに属することそれ自体からは、依存関係を導出しない。

### Membership Decision Criteria（帰属の判断基準）

あるDocumentation Asset（文書資産）がどのAreaに属するかは、
**その資産が何を定義する責務を持つか** 、すなわち
Definition Responsibility（定義責務）によって決まる。

次によっては決まらない。

- どのSubjectを扱っているか
- どの程度抽象的か
- どのDirectoryに配置されているか

SubjectとAreaが独立であることの例として、
[Convention Architecture](convention.md) がある。
同文書はConvention（規約）をSubjectとするが、
Normative Rule（規範的規則）を定義するのではなく、
Convention（規約）を成立させるConcept（概念）・Responsibility（責務）・
Relationshipを定義する。
したがって同文書はArchitecture Area（アーキテクチャ領域）に属し、
Conventions Area（規約領域）には属さない。

Framework Membershipについても同じ判断による。
あるDocumentation Asset（文書資産）が本Framework（体系）に属するかは、
その資産のDocument Responsibility（文書責務）が
本Framework（体系）のいずれかの
Area Responsibility（領域責務）の配分結果として成立するかによって決まる。
Area Membershipと別の判断を設けない。

したがって、次はそれだけではFramework Membershipを否定しない。

- 本Framework（体系）を定義する資産自身であること
- Design Dependency（設計依存）において本Framework（体系）の上流に位置すること
- 本Framework（体系）とは別のSubjectを扱うこと

本文書自身も、この判断の例外ではない。

## Philosophy Area（思想領域）

### Philosophy Area Responsibility（思想領域の領域責務）

特定のConcept Model（概念モデル）や具体構造から独立して、
Repositoryにおける設計・判断の根拠となる
**Fundamental Principle（根本原則）** を定義する。

### Philosophy Area Owns（思想領域が所有する対象）

- Fundamental Principle（根本原則）
- Value / Judgment Basis

### Philosophy Area Does Not Own（思想領域が所有しない対象）

- Concrete Concept Model
- Responsibility Allocation
- Relationship / Boundary（境界）
- Reusable Normative Rule
- Subject-specific Contract

### Boundary with Architecture Area（Architecture Areaとの境界）

ここで示すのは、
**Philosophy Area（思想領域）と
Architecture Area（アーキテクチャ領域）の二者間** で
Definition Authority（定義権限）がどちらにあるべきかを判断する場合の
境界である。

すなわち、あるDefinition（定義）が
Fundamental Principle（根本原則）として成立するのか、
Semantic / Structural Modelとして成立するのかを
判定する場面に限って適用する。

両者の境界判断に用いるのは、
**抽象度ではない** 。

用いるのは次の基準である。

> Philosophy Area（思想領域）と
> Architecture Area（アーキテクチャ領域）の間で責務を判定する場合、
> そのDefinition（定義）が、特定のConcept Model（概念モデル）から
> 独立してFundamental Principle（根本原則）として成立するかを
> 境界とする。

- 独立してFundamental Principle（根本原則）として成立する
  → Philosophy Area（思想領域）
- 特定のConcept Model（概念モデル）を前提として初めて成立する
  → Architecture Area（アーキテクチャ領域）

### Do Not Use as a General Decision Criterion（一般判定として用いない）

この基準を、
**4つのArea全体に対する一般判定として用いない** 。

次の推論は成立しない。

> あるDefinition（定義）が
> 特定のConcept Model（概念モデル）へ依存している。
> したがってArchitecture Area（アーキテクチャ領域）に属する。

Convention（規約）およびSpecificationも、
Architecture Area（アーキテクチャ領域）が定義するModelへ
依存し得る。
Modelへの依存があること自体は、
Architecture Area（アーキテクチャ領域）への帰属を意味しない。

Conventions Area（規約領域）および
Specifications Area（仕様領域）への帰属判定は、
それぞれのArea Responsibility（領域責務）が示す
Definition Responsibility（定義責務）によって別途行う。
判定の基準は
「Area Boundary Summary」に示す。

## Architecture Area（アーキテクチャ領域）

### Architecture Area Responsibility（アーキテクチャ領域の領域責務）

Repositoryが扱うSubjectについて、
その意味を成立させる
**Semantic / Structural Model** を定義する。

ここでいうModelには、次が含まれる。

- Concept（概念）
- Responsibility（責務）
- Relationship
- Boundary（境界）
- Definition Authority（定義権限）

### Architecture Area Does Not Own（アーキテクチャ領域が所有しない対象）

- Modelから独立したFundamental Principle（根本原則）
- Reusable Normative Standard（再利用可能な規範標準） / Rule
- Subject-specific Concrete Contract

### Local Design Principle Handling（Local Design Principleの扱い）

Architecture Area（アーキテクチャ領域）の文書が、
自身が定義するModelの内部で成立する
Local Design Principle（局所設計原則）を含むことは許容する。

ただし、それを
Philosophy Area（思想領域）が所有する
Fundamental Principle（根本原則）と混同しない。

Local Design Principle（局所設計原則）は、
そのModelを前提として初めて意味を持つ。
Modelから独立して成立するものではない。

## Conventions Area（規約領域）

### Conventions Area Responsibility（規約領域の領域責務）

複数の該当する成果物・作業・表現へ
**再利用・反復適用される
Normative Standard / Rule** を定義する。

### Identification Axis（識別軸）

本Areaの本質的な識別軸は、
**Normativeであること** だけではない。

識別軸となるのは、
その定義が
**独立したReusable Standardとして
反復適用されるか** である。

Normativeであっても、
特定Subjectを成立させるために固有に定められる契約は、
Specifications Area（仕様領域）に属する。

### Conventions Area Does Not Own（規約領域が所有しない対象）

- Ruleが前提とする
  Concept（概念）・Responsibility（責務）・
  Relationship・Boundary（境界）の
  Definition Authority（定義権限）
- 特定Subject全体を成立させる
  Concrete Contract
- Runtime Application Result

Ruleが前提とする概念や責務のDefinition Authority（定義権限）は
Architecture Area（アーキテクチャ領域）にある。
Conventions Area（規約領域）は、それらを参照して規範を定める。

## Specifications Area（仕様領域）

### Specifications Area Responsibility（仕様領域の領域責務）

特定Subjectについて、
そのSubjectを成立・実現・運用・検証可能にする
**Concrete Contract** を定義する。

### Boundary with Conventions Area（Conventions Areaとの境界）

両者の差は、
**Normativeか Non-normativeかではない** 。

差は次である。

```text
Convention
= reusable normative standard

Specification
= subject-specific concrete contract
```

判断に用いる問いは次である。

> その定義は、複数の対象へ反復適用される標準として成立するか。
> それとも、特定の対象を成立させるために固有に定められる契約か。

### Specifications Area Does Not Own（仕様領域が所有しない対象）

- Subjectから独立したReusable Standard
- 上位Concept Model（概念モデル）
- Fundamental Principle（根本原則）

## Area Boundary Summary（領域境界の要約）

各Areaは、
Definition Responsibility（定義責務）によって区別される。
抽象度によって区別されるのではない。

| Area | 何を定義するか | 区別の基準 |
| --- | --- | --- |
| Philosophy Area（思想領域） | Fundamental Principle（根本原則） | 特定Concept Model（概念モデル）から独立してFundamental Principle（根本原則）として成立するか（Architecture Area（アーキテクチャ領域）との二者間判定） |
| Architecture Area（アーキテクチャ領域） | Semantic / Structural Model | 対象の意味を成立させるConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）を定めるか |
| Conventions Area（規約領域） | Reusable Normative Standard（再利用可能な規範標準） | 独立した標準として複数対象へ反復適用されるか |
| Specifications Area（仕様領域） | Subject-specific Concrete Contract | 特定対象を成立・実現・運用・検証可能にする契約か |

## Physical Representation（物理表現）

本Framework（体系）が現在採用している
Physical Representation（物理表現）は次である。

```text
docs/
├─ philosophy/
├─ architecture/
├─ conventions/
└─ specifications/
```

対応は次である。

| Documentation Area（文書責務領域） | 現在のPhysical Representation（物理表現） |
| --- | --- |
| Philosophy Area（思想領域） | `docs/philosophy/` |
| Architecture Area（アーキテクチャ領域） | `docs/architecture/` |
| Conventions Area（規約領域） | `docs/conventions/` |
| Specifications Area（仕様領域） | `docs/specifications/` |

### Mapping Positioning（Mappingの位置づけ）

この対応は、
**Logical Identity（論理的同一性）の成立条件ではない** 。

[Documentation Structure Architecture](documentation-structure.md)
が定めるとおり、次を維持する。

```text
Area ≠ Directory
```

したがって次が成立する。

- Area Identityを、
  対応するDirectoryから導出しない。
- Directoryが存在しないことだけを理由に、
  そのAreaが成立していないと判断しない。
- この対応は、現時点で採用している
  Physical Representation（物理表現）の記録であり、
  変更され得る。

### `docs/` Handling（`docs/`の扱い）

`docs/` 自体を
Documentation Area（文書責務領域）として定義しない。
`docs/` は本Framework（体系）のPhysical Representation（物理表現）を
収める配置上の単位である。

### 1 Area → 1 top-level Directory Handling（1 Area → 1 top-level Directoryの扱い）

本Framework（体系）の4つのAreaについて、
1 Area → 1 top-level Directoryという対応を採用してよい。

ただしこれを、
Documentation Structure（文書構造）全般に適用される
普遍Ruleへ一般化しない。
これは本Framework（体系）が現在採る対応であり、
一般Modelの要求ではない。

### Mapping Rule Ownership（Mapping Ruleの所有）

具体的なPhysical Mapping Ruleを
最終的にどのConvention（規約）が所有するかは、
本文書では確定しない。

必要な範囲では、
本文書が
Current Physical Representationとして関係を記録する。
Naming Conventionや
Documentation Structure Conventionといった
未設計のAssetを、本文書のために先行して新設しない。

## Design Principles（設計原則）

### Separation by Definition Responsibility（定義責務で分離する）

Areaの分離は、
抽象度・粒度・対象の種類ではなく、
Definition Responsibility（定義責務）の違いによって行う。

### Single Definition Authority（定義権限を一箇所に置く）

あるDefinition（定義）のDefinition Authority（定義権限）は、
一つのDocumentation Asset（文書資産）に置く。
他のAssetは、それを再定義せず参照する。

### No Fixed Layer Hierarchy（固定階層を設けない）

Areaの列挙順を階層として扱わない。
Area間の依存は、
個々のDefinition（定義）のSemantic Need（意味上の必要性）から成立する。

### Traceability as Consequence（追跡可能性は結果である）

Traceabilityは責務分離の結果として成立する性質であり、
それ自体を目的として責務分離を歪めない。

### Logical Identity over Physical Location（同一性は物理配置に優先する）

Area Identityを
Directory構成から導出しない。
Physical Representation（物理表現）は
現在の対応の記録であって、成立条件ではない。

### No Anticipatory Asset（先行してAssetを新設しない）

現時点で必要性が確認されていない
Convention（規約）・Specificationを、
体系の見た目を整えるために先行して新設しない。

## Non-goals（現在扱わない事項）

本文書は次を定義しない。
ここで示す事項はDesign Gapではない。
本文書の現在の責務に基づいて、意図的に
定義・解決・導入の対象外としている事項であり、
必要な事項のみ後続設計へ委譲する。

### Documentation Asset Content（文書資産の内容に関する事項）

- 各Areaに属する個々のDocumentation Asset（文書資産）の内容
- AreaごとのDocumentation Asset（文書資産）一覧

### Structure / Naming（構造・命名に関する事項）

- Naming Convention
- Documentation Structure Convention
- Physical Mapping Ruleの最終的な所有先
- File名・Directory名・Pathの具体規則

### Composition（体系間構成に関する事項）

- 他のDocumentation Framework（文書体系）との共存
- Framework（体系）間のPriority／Refinement（具体化）／Dependency（依存）

### Declaration / Representation Format（宣言・記述形式に関する事項）

- MetadataおよびDeclarationのSchema
- Area帰属の機械可読な表現形式

### Concepts Not Introduced（導入しないConcept）

- Representative Document
- Navigation Document

いずれも
[Documentation Structure Architecture](documentation-structure.md)
の判断に従い、本Framework（体系）でも導入しない。
Area全体に関わる責務が必要な場合は、
通常のDocumentation Asset（文書資産）と
Document Responsibility（文書責務）で表現する。

## Usage by Downstream Design（下位設計からの参照）

後続設計は、本文書を参照して次を判断できる。

1. ある定義が、本Framework（体系）のどのAreaに属するか。
   → 各AreaのArea Responsibility（領域責務）と
   「Area Boundary Summary」による。
2. ある定義を、Convention（規約）として定めるべきか、
   Specificationとして定めるべきか。
   → Reusable Standardか
   Subject-specific Contractかによる。
3. ある定義が前提とするConcept（概念）・Responsibility（責務）の
   Definition Authority（定義権限）がどこにあるか。
   → Architecture Area（アーキテクチャ領域）にある。

本文書からは判断できないのは、
個々のDocumentation Asset（文書資産）の内容そのものと、
その記述・命名・配置の具体規則である。
これらは後続設計の責務に属する。
