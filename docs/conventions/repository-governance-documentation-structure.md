# Repository Governance Documentation Structure Convention（Repository統治文書構造規約）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Governance Documentation Framework（Repository統治文書体系）に属する
Documentation Asset（文書資産）の内部Semantic Structure（意味構造）について、
Framework Responsibility（体系責務）および
Area Responsibility（領域責務）から反復して成立する
Section Responsibility（Section責務）を、
本Framework（体系）固有の
Reusable Normative Standard（再利用可能な規範標準）として定義し、
一貫して適用可能にする**
Convention Asset（規約資産）である。

本文書が扱う問いは次の2点である。

1. 本Framework（体系）に属するDocumentation Asset（文書資産）へ
   反復して成立するSection Responsibility（Section責務）として、
   現在何が成立するのか。
2. その各Section Responsibility（Section責務）は、
   どのApplicability Scope（適用範囲）において
   Standard Section（標準Section）として成立するのか。

[Documentation Structure Convention](documentation-structure.md)
は、Standard Section（標準Section）の一般機構と、
Applicability Scope（適用範囲）を
Documentation-wide（Documentation全体）とする
Standard Section（標準Section）を定義する。
ただし同Convention（規約）は、
Framework-scoped / Area-scoped Standard Section
（文書体系・領域限定標準Section）の具体Catalog（一覧）を
意図的に定義していない。

本文書はその余地において、
本Framework（体系）に固有の
Standard Section（標準Section）を定義する。

本文書は、上位設計および
[Documentation Structure Convention](documentation-structure.md)
が定義するConcept（概念）・機構を再定義しない。

## Position（上位設計との関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Convention Architecture](../architecture/convention.md)
- [Documentation Structure Convention](documentation-structure.md)
- [Convention Authoring Convention](convention.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture（文書構造の一般意味モデル）
        ▲
        │ refines（具体的な文書体系へ具体化する）
Repository Governance Documentation Framework Architecture
        ▲
        │ refines（体系固有の規範標準へ具体化する）
Repository Governance Documentation Structure Convention（本文書）

Documentation Structure Convention（標準Section機構とDocumentation全体標準Section）
        ▲
        │ conforms to（標準Section機構へ適合する）
Repository Governance Documentation Structure Convention（本文書）

Convention Architecture（規約の意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（規約記述表記）
        ▲
        │ conforms to（記述表記に従う）
Repository Governance Documentation Structure Convention（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
本Framework（体系）に属するDocumentation Asset（文書資産）という
反復的に成立する成果物へ繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Area（領域）またはFramework（体系）を代表・集約する
Asset（資産）ではない。

本文書が使用する次のConcept（概念）および機構の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Framework（文書体系）・
  Documentation Area（文書責務領域）・
  Documentation Asset（文書資産）と、
  Framework Responsibility（体系責務）・
  Area Responsibility（領域責務）・
  Document Responsibility（文書責務）
- Section（節）とSection Responsibility（Section責務）、
  およびResponsibility Decomposition（責務分解）
- `Section ≠ Heading` をはじめとする
  Logical / Representation Boundary（論理／表現境界）
- 本Framework（体系）のArea Composition（領域構成）、
  各Area（領域）のArea Responsibility（領域責務）、
  およびArea（領域）間の境界判断の基準
- Philosophy Area（思想領域）が所有する
  Fundamental Principle（根本原則）と、
  Architecture Area（アーキテクチャ領域）が許容する
  Local Design Principle（局所設計原則）の区別
- Standard Section（標準Section）の定義要件、
  Applicability Scope（適用範囲）に基づく適用、
  Standard Section Identity（標準Section同一性）の選択と適合
- Standard Section Definition（標準Section定義）と
  Presence Requirement（設置要求）の分離
- Standard Section Catalog（標準Section一覧）の開放性、
  およびDocument-specific Section（文書固有Section）の許容
- Applicability Scope（適用範囲）を跨ぐ
  Standard Identity（標準同一性）の非重複
- Convention（規約）およびConvention Responsibility（規約責務）、
  Normative Rule（規範的ルール）と
  Non-normative Content（非規範的内容）の区別、
  Rule Model（ルールモデル）、Requirement Level（要求レベル）、
  Rule Identity（ルール同一性）とその安定性
- Rule ID Format（規約ルールID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  Stability（安定性）のField表現
- Namespace Code（名前空間コード）の割当

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository Governance Documentation Framework（Repository統治文書体系）
  全体をApplicability Scope（適用範囲）とする
  Standard Section（標準Section）の
  Section Responsibility（Section責務）
- 本Framework（体系）と特定のArea（領域）の組合せを
  Applicability Scope（適用範囲）とする
  Standard Section（標準Section）の
  Section Responsibility（Section責務）
- それら固有のStandard Section（標準Section）について、
  将来Semantic Need（意味上の必要性）が確認された場合の
  Presence Requirement（設置要求）

### Out of Scope（本文書が定義しない範囲）

- Standard Section（標準Section）の一般機構。
  すなわち定義要件、
  Applicability Scope（適用範囲）に基づく適用、
  Standard Section Identity（標準Section同一性）の選択と適合、
  Standard Section Definition（標準Section定義）と
  Presence Requirement（設置要求）の分離、
  Standard Section Catalog（標準Section一覧）の開放性、
  Standard Identity（標準同一性）の非重複
- Applicability Scope（適用範囲）を
  Documentation-wide（Documentation全体）とする
  Standard Section（標準Section）
- Section（節）・Section Responsibility（Section責務）・
  Responsibility Decomposition（責務分解）の
  一般Semantic Model（意味モデル）
- 本Framework（体系）のArea Composition（領域構成）、
  Area Responsibility（領域責務）、
  およびArea（領域）帰属の判定
- 本Framework（体系）に属する
  Documentation Asset（文書資産）へ要求される
  Fixed Section Set（固定Section集合）、
  およびSection Order（Section順序）
- Section Responsibilities（Section責務群）による
  Document Responsibility（文書責務）のCoverage（網羅）要求
- Section（節）とHeading（見出し）・Heading Level（見出しレベル）の
  Mapping Rule（対応規則）、および
  Canonical Heading Representation（正規見出し表現）
- Natural Language Representation（自然言語表現）、
  日英表記、文体、用語選択
- Markdown Syntax、Markdown Heading Marker（Markdown見出し記号）、
  その他Markdown固有の表現
- File名、Directory名、Path等のNaming Convention（命名規約）
- Documentation Asset（文書資産）間の
  Dependency（依存）・Refinement（具体化）関係のModel（モデル）
- Metadata（構造化メタデータ）およびDeclaration（明示的宣言）のSchema、
  Template（雛形）
- Documentation Lifecycle（文書の生涯管理）・Review・Validation

本文書は、本Framework（体系）における
Documentation Asset（文書資産）のAuthoring（記述）全般を所有しない。
現在のNormative Rule（規範的ルール）は、
Standard Section（標準Section）の定義のみで構成される。

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: RDS
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace／共有基盤名前空間）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的ルール）を読むための補足である。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。
Standard Section（標準Section）の要件・適用・責務は、
すべてNormative Rule（規範的ルール）側で確定する。

### 本文書が所有する範囲

[Documentation Structure Convention](documentation-structure.md)
は、Standard Section（標準Section）の一般機構と、
Applicability Scope（適用範囲）を
Documentation-wide（Documentation全体）とする
Standard Section（標準Section）を所有する。

本文書が所有するのは、
本Framework（体系）を前提として初めて成立する
Standard Section（標準Section）である。

```text
Documentation Structure Convention
    = 標準Section機構 ＋ Documentation全体標準Section

Repository Governance Documentation Structure Convention（本文書）
    = Repository統治文書体系に固有の標準Section
```

本文書は一般機構を再定義しない。
その機構へ適合する側として、
個別のStandard Section（標準Section）を定義する。

### Identity（同一性）とRepresentation（表現）

`Position`・`Concept Model`・`Design Principles`・`Non-goals` は、
Standard Section Identity（標準Section同一性）を指す名称であり、
そのまま記述されるべき
Canonical Heading Representation（正規見出し表現）ではない。

Heading（見出し）の文字列、日本語併記の有無、
Heading Level（見出しレベル）、
Markdown Heading Marker（Markdown見出し記号）、
Section Order（Section順序）は、本文書では定めない。

### 一覧の開放性

本文書が現在定義するStandard Section（標準Section）は、
本Framework（体系）において使用可能な
Section Responsibility（Section責務）または
Section Identity（Section同一性）の
Closed Set（閉じた集合）ではない。

本Framework（体系）に属するDocumentation Asset（文書資産）は、
自身のDocument Responsibility（文書責務）を果たすために必要な
Section Responsibility（Section責務）を、
Document-specific Section（文書固有Section）として構成できる。

将来、反復して成立する
Section Responsibility（Section責務）が新たに確認された場合、
本文書へ追加され得る。

### 定義と設置要求

本文書が現在定義するStandard Section（標準Section）について、
Presence Requirement（設置要求）は定めない。

Standard Section（標準Section）として定義されていることが
そのまま設置要求を意味しないことは、
[Documentation Structure Convention](documentation-structure.md)
の一般Rule（ルール）による。

したがって、各Documentation Asset（文書資産）が
これらのSection（節）を持つか否かは、
その資産のDocument Responsibility（文書責務）に照らして
個別に判断される。

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Framework-wide Standard Sections（文書体系全体標準Section）

#### RDS-SF-001 — Position Standard Section

**Rule ID:** `RDS-SF-001`

**Rule Name:** Position Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Repository Governance Documentation Framework（Repository統治文書体系）
全体とするPosition Standard Section（位置標準Section）を定義する。
そのSection Responsibility（Section責務）は、
本Framework（体系）に属するDocumentation Asset（文書資産）が、
どの上位Definition（定義）を前提とし、
何をRefinement（具体化）し、
Design Dependency（設計依存）の中でどの位置を占めるのかを
明確にすることである。

**Reason:** 本Framework（体系）は、
Definition（定義）をSemantic Responsibility（意味上の責務）の違いに応じて
分離する体系である。
そのため、上位Definition（定義）への依存や
Refinement（具体化）の関係を示す責務が、
本Framework（体系）に属する資産へ反復して現れる。
その責務が成立する資産ごとに別のIdentity（同一性）で現れると、
同じ位置情報が資産ごとに別物として解釈される。
共通のIdentity（同一性）を与えることで、
読み手はその資産をどの前提の下で読むべきかを
一貫した根拠から確認できる。

**Note:** 本Rule（ルール）は定義であり、
Presence Requirement（設置要求）を定めない。

Relationships Standard Section（関係標準Section）とは
Section Responsibility（Section責務）が異なる。
Relationships Standard Section（関係標準Section）が担うのは、
当該資産の意味成立に必要な
Semantic Relationship（意味上の関係）一般である。
本Standard Section（標準Section）が担うのは、
本Framework（体系）内における
Definition（定義）・Refinement（具体化）・
Design Dependency（設計依存）上の位置である。
両者を同一の責務として扱わない。

### Architecture Area Standard Sections（アーキテクチャ領域標準Section）

#### RDS-SF-002 — Concept Model Standard Section

**Rule ID:** `RDS-SF-002`

**Rule Name:** Concept Model Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Repository Governance Documentation Framework（Repository統治文書体系）
およびArchitecture Area（アーキテクチャ領域）とする
Concept Model Standard Section（概念モデル標準Section）を定義する。
そのSection Responsibility（Section責務）は、
Architecture Asset（アーキテクチャ資産）が定義する
Subject（対象）を成立させる主要Concept（概念）と、
それらの基本的な意味・成立条件・
Semantic Relationship（意味上の関係）を、
後続の詳細Model（モデル）が前提として利用できる
全体像として明確にすることである。

**Reason:** Architecture Area（アーキテクチャ領域）の
Area Responsibility（領域責務）は、
Subject（対象）の意味を成立させる
Semantic / Structural Model（意味・構造モデル）を定義することである。
そのため、詳細Model（モデル）が前提とするConcept（概念）の全体像を
先に保持する責務が、同領域の資産へ反復して現れる。
その責務が成立する資産ごとに別のIdentity（同一性）で現れると、
読み手はどこに前提となるConcept（概念）が置かれているかを
資産ごとに探すことになる。
共通のIdentity（同一性）を与えることで、
その所在を一貫した根拠から確認できる。

**Note:** 本Rule（ルール）は定義であり、
Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）は、
Architecture Asset（アーキテクチャ資産）の
固定Template（雛形）ではない。
Architecture Asset（アーキテクチャ資産）が
専門Model（専門モデル）へ直接分解され、
独立したConcept Model（概念モデル）としての
Section Responsibility（Section責務）が成立しない場合もある。

#### RDS-SF-003 — Design Principles Standard Section

**Rule ID:** `RDS-SF-003`

**Rule Name:** Design Principles Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Repository Governance Documentation Framework（Repository統治文書体系）
およびArchitecture Area（アーキテクチャ領域）とする
Design Principles Standard Section（設計原則標準Section）を定義する。
そのSection Responsibility（Section責務）は、
Architecture Asset（アーキテクチャ資産）が定義する
Semantic Model（意味モデル）または
Structural Model（構造モデル）について、
設計判断および解釈を一貫させるための
Local Design Principles（局所設計原則）を明確にすることである。

**Reason:** Architecture Asset（アーキテクチャ資産）が定義する
Model（モデル）に、それを前提として成立する
Local Design Principles（局所設計原則）が伴う場合がある。
そうした判断基準を保持する責務は、
Model（モデル）を定義する同領域の資産へ反復して現れる。
その責務が成立する資産ごとに別のIdentity（同一性）で現れると、
判断基準がModel（モデル）の記述と区別されないまま読まれ、
何が解釈を一貫させるための基準なのかが不明確になる。
共通のIdentity（同一性）を与えることで、
その区別を一貫した根拠から確認できる。

**Note:** 本Rule（ルール）は定義であり、
Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）が扱うのは、
そのArchitecture Asset（アーキテクチャ資産）が定義する
個別のModel（モデル）へ従属する
Local Design Principles（局所設計原則）である。
Philosophy Area（思想領域）が所有する
Fundamental Principle（根本原則）を所有しない。
両者の境界は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
による。

#### RDS-SF-004 — Non-goals Standard Section

**Rule ID:** `RDS-SF-004`

**Rule Name:** Non-goals Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Repository Governance Documentation Framework（Repository統治文書体系）
およびArchitecture Area（アーキテクチャ領域）とする
Non-goals Standard Section（非目標標準Section）を定義する。
そのSection Responsibility（Section責務）は、
Architecture Asset（アーキテクチャ資産）が、
そのResponsibility Boundary（責務境界）を踏まえて
意図的に定義・解決しない事項を明確にし、
必要な場合には、その事項を担う後続の
Design Responsibility（設計責務）または
Documentation Asset（文書資産）への
Delegation（委譲）を示すことである。

**Reason:** Architecture Asset（アーキテクチャ資産）が、
自身の責務境界を踏まえて意図的に定義・解決しないという
設計判断を持つ場合がある。
その判断を保持する責務は、同領域の資産へ反復して現れる。
その責務が成立する資産ごとに別のIdentity（同一性）で現れると、
読み手は意図的な設計判断と
単に検討されていない事項とを区別する根拠を資産ごとに探すことになり、
委譲先の所在も同様に定まらない。
共通のIdentity（同一性）を与えることで、
その区別と委譲先を一貫した根拠から確認できる。

**Note:** 本Rule（ルール）は定義であり、
Presence Requirement（設置要求）を定めない。

Scope Standard Section（対象範囲標準Section）とは
Section Responsibility（Section責務）が異なる。
Scope Standard Section（対象範囲標準Section）が担うのは、
Document Responsibility（文書責務）の
Responsibility Boundary（責務境界）そのものである。
本Standard Section（標準Section）が担うのは、
その境界を踏まえたうえで意図的に定義・解決しないという
設計上の判断である。
両者を同一の責務として扱わない。

Delegation（委譲）は、
Non-goals（非目標）に必要に応じて付随する情報として扱う。
本文書はDelegation（委譲）を
独立したStandard Section（標準Section）として定義しない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention.md)
が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `RDS-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Field（フィールド）を規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書は、
[Documentation Structure Convention](documentation-structure.md)
および本文書自身が定めるRule（規則）にも従っている。

- Document Responsibility（文書責務）を内容から識別可能にしている。
- Purpose・Scopeの各
  Standard Section Identity（標準Section同一性）を、
  それぞれの責務に適合するSection（節）へ使用している。
- 本文書は本Framework（体系）に属するため、
  Position Standard Section（位置標準Section）が適用可能である。
  対応するSection Responsibility（Section責務）を
  独立したSection（節）として構成しているため、
  そのStandard Section Identity（標準Section同一性）を使用している。
- 本文書はConventions Area（規約領域）に属するため、
  Architecture Area（アーキテクチャ領域）を
  Applicability Scope（適用範囲）に含む
  Standard Section（標準Section）は適用されない。
- その他のSection（節）は
  Document-specific Section（文書固有Section）である。

本文書自身のHeading（見出し）表現・Section Order（Section順序）は、
本文書が定めるものではない。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
