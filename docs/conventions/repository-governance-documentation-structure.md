# Repository Governance Documentation Structure Convention（Repository統治文書構造規約）

## Purpose（目的）

本文書は、`noxris42` において**Repository Governance Documentation Frameworkに属するDocumentation Asset（文書資産）の内部Semantic Structure（意味構造）について、Framework Responsibility（体系責務）およびArea Responsibility（領域責務）から反復して成立するSection Responsibility（Section責務）を、本Framework（体系）固有のReusable Normative Standard（再利用可能な規範標準）として定義し、一貫して適用可能にする**Convention Asset（規約資産）である。

本文書が扱う問いは次の2点である。

1. 本Framework（体系）に属するDocumentation Asset（文書資産）へ反復して成立するSection Responsibility（Section責務）として、現在何が成立するのか。
2. その各Section Responsibility（Section責務）は、どのApplicability Scope（適用範囲）においてStandard Section（標準Section）として成立するのか。

[Documentation Structure Convention](documentation-structure.md)は、Standard Section（標準Section）の一般機構と、Applicability Scope（適用範囲）をDocumentation-wideとするStandard Section（標準Section）を定義する。ただし同Convention（規約）は、Framework-scoped / Area-scoped Standard Sectionの具体Catalogを意図的に定義していない。

本文書はその余地において、本Framework（体系）に固有のStandard Section（標準Section）を定義する。

本文書は、上位設計および[Documentation Structure Convention](documentation-structure.md)が定義するConcept（概念）・機構を再定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するConventions Area（規約領域）に属する通常のDocumentation Asset（文書資産）である。本Framework（体系）に属するDocumentation Asset（文書資産）という反復的に成立する成果物へ繰り返し適用されるReusable Normative Standard（再利用可能な規範標準）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）および機構のDefinition Authority（定義権限）は上位設計にある。本文書はこれらを参照するのみで、再定義しない。

- Documentation Framework（文書体系）・Documentation Area（文書責務領域）・Documentation Asset（文書資産）と、Framework Responsibility（体系責務）・Area Responsibility（領域責務）・Document Responsibility（文書責務）
- SectionとSection Responsibility（Section責務）、およびResponsibility Decomposition（責務分解）
- `Section ≠ Heading` をはじめとするLogical / Representation Boundary
- 本Framework（体系）のArea Composition、各AreaのArea Responsibility（領域責務）、およびArea間の境界判断の基準
- Philosophy Area（思想領域）が所有するFundamental Principle（根本原則）と、Architecture Area（アーキテクチャ領域）が許容するLocal Design Principle（局所設計原則）の区別
- Standard Section（標準Section）の定義要件、Applicability Scope（適用範囲）に基づく適用、Standard Section Identity（標準Section同一性）の選択と適合
- Standard Section DefinitionとPresence Requirement（設置要求）の分離
- Standard Section Catalogの開放性、およびDocument-specific Section（文書固有Section）の許容
- Applicability Scope（適用範囲）を跨ぐStandard Identityの非重複
- Convention（規約）およびConvention Responsibility（規約責務）、Normative Rule（規範的規則）とNon-normative Content（非規範的内容）の区別、Rule Model（規則モデル）、Requirement Level（要求レベル）、Rule Identity（規則同一性）とその安定性
- Rule ID Format（規則ID形式）、Rule Field（規則フィールド）の構成・順序・Markdown表現、StabilityのField表現
- Namespace Code（名前空間コード）の割当

### Position（設計上の位置づけ）

本文書は、次を上位Sourceとして参照する。

- [Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Convention Architecture](../architecture/convention.md)
- [Documentation Structure Convention](documentation-structure.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ refines
Repository Governance Documentation Framework
        ▲
        │ refines
Repository Governance Documentation Structure Convention

Documentation Structure Convention
        ▲
        │ conforms to
Repository Governance Documentation Structure Convention

Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Repository Governance Documentation Structure Convention
```

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository Governance Documentation Framework全体をApplicability Scope（適用範囲）とするStandard Section（標準Section）のSection Responsibility（Section責務）
- 本Framework（体系）と特定のAreaの組合せをApplicability Scope（適用範囲）とするStandard Section（標準Section）のSection Responsibility（Section責務）
- それらのStandard Section（標準Section）が、他のStandard Section（標準Section）のResponsibility Decomposition（責務分解）として成立する場合のその関係
- それら固有のStandard Section（標準Section）のうち、Standard Section Heading Representation（標準Section見出し表現）を宣言するものについての、その具体のStandard Section Heading Representation（標準Section見出し表現）
- それら固有のStandard Section（標準Section）について、将来Semantic Need（意味上の必要性）が確認された場合のPresence Requirement（設置要求）

### Out of Scope（本文書が定義しない範囲）

- Standard Section（標準Section）の一般機構。すなわち定義要件、Applicability Scope（適用範囲）に基づく適用、Standard Section Identity（標準Section同一性）の選択と適合、Standard Section DefinitionとPresence Requirement（設置要求）の分離、Standard Section Catalogの開放性、Standard Identityの非重複
- Applicability Scope（適用範囲）をDocumentation-wideとするStandard Section（標準Section）
- Section・Section Responsibility（Section責務）・Responsibility Decomposition（責務分解）の一般Semantic Model（意味モデル）
- 本Framework（体系）のArea Composition、 Area Responsibility（領域責務）、およびArea帰属の判定
- 本Framework（体系）に属するDocumentation Asset（文書資産）へ要求されるFixed Section Set、およびSection Order（Section順序）
- Section ResponsibilitiesによるDocument Responsibility（文書責務）のCoverage（網羅）要求
- SectionとHeading（見出し）・Heading Level（見出しレベル）のMapping Rule（対応規則）
- Natural Language Representation（自然言語表現）、日英表記、文体、用語選択
- Markdown Syntax、Markdown Heading Marker（Markdown見出し記号）、その他Markdown固有の表現
- File名、Directory名、Path等のNaming Convention
- Documentation Asset（文書資産）間のDependency（依存）・Refinement（具体化）関係のModel
- MetadataおよびDeclarationのSchema、 Template
- Documentation Lifecycle（文書の生涯管理）・Review・Validation

本文書は、本Framework（体系）におけるDocumentation Asset（文書資産）のAuthoring全般を所有しない。現在のNormative Rule（規範的規則）は、Standard Section（標準Section）の定義のみで構成される。

## Concrete Declarations（具体宣言）

本節はConcrete Assignment（具体割当）の宣言である。**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: RDS
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、[Convention Authoring Convention](convention-authoring.md)が割り当てたNamespace Code（名前空間コード） `SF` （Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

### Standard Section Heading Representation（標準Section見出し表現）

本文書が定義するStandard Section（標準Section）に対するStandard Section Heading Representation（標準Section見出し表現）を、Standard Section（標準Section）ごとに次のとおり宣言する。以下の宣言はいずれも、Standard Section Identity（標準Section同一性）のMeaning（意味）を変更しない。

| Standard Section | English Heading Representation | Primary Language Heading Explanation |
| --- | --- | --- |
| Position | Position | 設計上の位置づけ |
| Concept Model | Concept Model | 概念モデル |
| Design Principles | Design Principles | 設計原則 |
| Non-goals | Non-goals | 現在扱わない事項 |
| Concrete Declarations | Concrete Declarations | 具体宣言 |
| Convention Code | Convention Code | 規約コード |
| Namespace Code | Namespace Code | 名前空間コード |
| Normative Rules | Normative Rules | 規範的ルール |
| Self Application | Self Application | 本文書自身への適用 |

`Position` のPrimary Language Heading Explanation（主要言語見出し説明）を`設計上の位置づけ` とするのは、当該Standard Section（標準Section）のSection Responsibility（Section責務）が、上位Sourceとの関係に限らず、本Framework（体系）における当該資産の位置づけ全体を対象とするためである。

`Non-goals` のPrimary Language Heading Explanation（主要言語見出し説明）にDelegationを含めないのは、`RDS-SF-004` においてDelegationが必要な場合にのみ付随する情報であり、当該Standard Section（標準Section）のSection Responsibility（Section責務）を常に構成するものではないためである。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的規則）を読むための補足である。本節はNon-normative Content（非規範的内容）であり、Normative Meaning（規範的意味）を保持しない。Standard Section（標準Section）の要件・適用・責務は、すべてNormative Rule（規範的規則）側で確定する。

### Scope Owned by This Document（本文書が所有する範囲）

[Documentation Structure Convention](documentation-structure.md)は、Standard Section（標準Section）の一般機構と、Applicability Scope（適用範囲）をDocumentation-wideとするStandard Section（標準Section）を所有する。

本文書が所有するのは、本Framework（体系）を前提として初めて成立するStandard Section（標準Section）である。

```text
Documentation Structure Convention
    = 標準Section機構 ＋ Documentation全体標準Section

Repository Governance Documentation Structure Convention
    = Repository統治文書体系に固有の標準Section
```

本文書は一般機構を再定義しない。その機構へ適合する側として、個別のStandard Section（標準Section）を定義する。

### Standard Section Identity and Standard Section Heading Representation（標準Section同一性と標準Section見出し表現）

`Position`・`Concept Model`・`Design Principles`・`Non-goals`・ `Concrete Declarations`・`Convention Code`・`Namespace Code`・ `Normative Rules`・`Self Application` は、Standard Section Identity（標準Section同一性）を指す名称である。Standard Section Identity（標準Section同一性）はHeading（見出し）文字列の一致によって成立するものではなく、Applicability Scope（適用範囲）とSection Responsibility（Section責務）によって成立する。

これらのStandard Section Identity（標準Section同一性）に対するStandard Section Heading Representation（標準Section見出し表現）は、「Concrete Declarations」で宣言している。Standard Section Identity（標準Section同一性）をHeading（見出し）として表現する場合、宣言したRepresentation（表現）が再利用の対象である。宣言されたRepresentation（表現）が存在することは、当該Sectionの設置を要求しない。

Heading Level（見出しレベル）、Markdown Heading Marker（Markdown見出し記号）、Section Order（Section順序）は、本文書では定めない。

### Catalog Openness（一覧の開放性）

本文書が現在定義するStandard Section（標準Section）は、本Framework（体系）において使用可能なSection Responsibility（Section責務）またはSection Identity（Section同一性）のClosed Set（閉じた集合）ではない。

本Framework（体系）に属するDocumentation Asset（文書資産）は、自身のDocument Responsibility（文書責務）を果たすために必要なSection Responsibility（Section責務）を、Document-specific Section（文書固有Section）として構成できる。

将来、反復して成立するSection Responsibility（Section責務）が新たに確認された場合、本文書へ追加され得る。

### Definition and Presence Requirement（定義と設置要求）

本文書が現在定義するStandard Section（標準Section）について、Presence Requirement（設置要求）は定めない。

Standard Section（標準Section）として定義されていることがそのまま設置要求を意味しないことは、[Documentation Structure Convention](documentation-structure.md)の一般Ruleによる。

したがって、各Documentation Asset（文書資産）がこれらのSectionを持つか否かは、その資産のDocument Responsibility（文書責務）に照らして個別に判断される。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、Rule ID（規則ID）はCategory（分類）を表現しない。

### Framework-wide Standard Sections（文書体系全体標準Section）

#### RDS-SF-001 — Position Standard Section（位置標準Section）

**Rule ID:** `RDS-SF-001`

**Rule Name:** Position Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation Framework全体とするPosition Standard Sectionを定義する。そのSection Responsibility（Section責務）は、[Documentation Structure Convention](documentation-structure.md)が定義するRelationships Standard SectionのResponsibility Decomposition（責務分解）として、本Framework（体系）に属するDocumentation Asset（文書資産）自身が、どの上位Definition（定義）を前提とし、何をRefinement（具体化）し、一方向のDesign Dependency（設計依存）の中でどの位置を占めるのかを明確にすることである。

**Reason:** 本Framework（体系）は、Definition（定義）をSemantic Responsibility（意味上の責務）の違いに応じて分離する体系である。そのため、上位Definition（定義）への依存やRefinement（具体化）の関係を示す責務が、本Framework（体系）に属する資産へ反復して現れる。その責務が成立する資産ごとに別のIdentity（同一性）で現れると、同じ位置情報が資産ごとに別物として解釈される。共通のIdentity（同一性）を与えることで、読み手はその資産をどの前提の下で読むべきかを一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）とRelationships Standard Sectionの関係は、Responsibility Decomposition（責務分解）である。Relationships Standard Sectionが担うのは、当該資産の意味成立に必要なSemantic Relationship一般である。本Standard Section（標準Section）が担うのは、そのうち、当該資産自身のDefinition（定義）上の前提・Refinement（具体化）・一方向のDesign Dependency（設計依存）上の位置を確定させる部分である。本Standard Section（標準Section）を、Relationships Standard Sectionから独立したSemantic Responsibility（意味上の責務）として扱わない。Relationships Standard Sectionの責務のうち、分解されていない部分はRelationships Standard Section自身が直接担う。

Responsibility Boundary Standard Sectionとは、同一のRelationships Standard Sectionに対するResponsibility Decomposition（責務分解）における別のChild Responsibility（子責務）である。Framework / Areaへの帰属、Definition Authority（定義権限）の所在、および隣接する責務主体とのBoundary（境界）は、それだけでは本Standard Section（標準Section）のSection Responsibility（Section責務）ではない。

### Architecture Area Standard Sections（アーキテクチャ領域標準Section）

#### RDS-SF-002 — Concept Model Standard Section（概念モデル標準Section）

**Rule ID:** `RDS-SF-002`

**Rule Name:** Concept Model Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびArchitecture Area（アーキテクチャ領域）とするConcept Model Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Architecture Asset（アーキテクチャ資産）が定義するSubjectを成立させる主要Concept（概念）と、それらの基本的な意味・成立条件・Semantic Relationshipを、後続の詳細Modelが前提として利用できる全体像として明確にすることである。

**Reason:** Architecture Area（アーキテクチャ領域）のArea Responsibility（領域責務）は、Subjectの意味を成立させるSemantic / Structural Modelを定義することである。そのため、詳細Modelが前提とするConcept（概念）の全体像を先に保持する責務が、同領域の資産へ反復して現れる。その責務が成立する資産ごとに別のIdentity（同一性）で現れると、読み手はどこに前提となるConcept（概念）が置かれているかを資産ごとに探すことになる。共通のIdentity（同一性）を与えることで、その所在を一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）は、Architecture Asset（アーキテクチャ資産）の固定Templateではない。Architecture Asset（アーキテクチャ資産）が専門Modelへ直接分解され、独立したConcept Model（概念モデル）としてのSection Responsibility（Section責務）が成立しない場合もある。

#### RDS-SF-003 — Design Principles Standard Section（設計原則標準Section）

**Rule ID:** `RDS-SF-003`

**Rule Name:** Design Principles Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびArchitecture Area（アーキテクチャ領域）とするDesign Principles Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Architecture Asset（アーキテクチャ資産）が定義するSemantic Model（意味モデル）またはStructural Modelについて、設計判断および解釈を一貫させるためのLocal Design Principlesを明確にすることである。

**Reason:** Architecture Asset（アーキテクチャ資産）が定義するModelに、それを前提として成立するLocal Design Principlesが伴う場合がある。そうした判断基準を保持する責務は、Modelを定義する同領域の資産へ反復して現れる。その責務が成立する資産ごとに別のIdentity（同一性）で現れると、判断基準がModelの記述と区別されないまま読まれ、何が解釈を一貫させるための基準なのかが不明確になる。共通のIdentity（同一性）を与えることで、その区別を一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）が扱うのは、そのArchitecture Asset（アーキテクチャ資産）が定義する個別のModelへ従属するLocal Design Principlesである。Philosophy Area（思想領域）が所有するFundamental Principle（根本原則）を所有しない。両者の境界は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)による。

#### RDS-SF-004 — Non-goals Standard Section（非目標標準Section）

**Rule ID:** `RDS-SF-004`

**Rule Name:** Non-goals Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびArchitecture Area（アーキテクチャ領域）とするNon-goals Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Architecture Asset（アーキテクチャ資産）が、そのResponsibility Boundary（責務境界）を踏まえて意図的に定義・解決しない事項を明確にし、必要な場合には、その事項を担う後続のDesign ResponsibilityまたはDocumentation Asset（文書資産）へのDelegationを示すことである。

**Reason:** Architecture Asset（アーキテクチャ資産）が、自身の責務境界を踏まえて意図的に定義・解決しないという設計判断を持つ場合がある。その判断を保持する責務は、同領域の資産へ反復して現れる。その責務が成立する資産ごとに別のIdentity（同一性）で現れると、読み手は意図的な設計判断と単に検討されていない事項とを区別する根拠を資産ごとに探すことになり、委譲先の所在も同様に定まらない。共通のIdentity（同一性）を与えることで、その区別と委譲先を一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

Scope Standard SectionとはSection Responsibility（Section責務）が異なる。Scope Standard Sectionが担うのは、Document Responsibility（文書責務）のResponsibility Boundary（責務境界）そのものである。本Standard Section（標準Section）が担うのは、その境界を踏まえたうえで意図的に定義・解決しないという設計上の判断である。両者を同一の責務として扱わない。

Delegationは、Non-goalsに必要に応じて付随する情報として扱う。本文書はDelegationを独立したStandard Section（標準Section）として定義しない。

### Conventions Area Standard Sections（規約領域標準Section）

#### RDS-SF-005 — Concrete Declarations Standard Section（具体宣言標準Section）

**Rule ID:** `RDS-SF-005`

**Rule Name:** Concrete Declarations Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびConventions Area（規約領域）とするConcrete Declarations Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Convention Asset（規約資産）が必要とするConcrete Assignment（具体割当）およびConcrete Declarationを、Normative Rule（規範的規則）から区別して保持することである。

**Reason:** Convention Asset（規約資産）は、識別子の形式および使用条件を定めるNormative Rule（規範的規則）と、どの値が実際に割り当てられているかというConcrete Assignment（具体割当）の両方を必要とする。両者が区別されないまま置かれると、値の変更が規範の変更として読まれ、規範の変更が値の変更として読まれる。この区別を保持する責務は、Conventions Area（規約領域）の資産へ反復して現れる。共通のIdentity（同一性）を与えることで、その区別を一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）はNon-normative Content（非規範的内容）を保持する責務であり、Normative Effectを持たない。

#### RDS-SF-006 — Convention Code Standard Section（規約コード標準Section）

**Rule ID:** `RDS-SF-006`

**Rule Name:** Convention Code Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびConventions Area（規約領域）とするConvention Code Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Concrete Declarations Standard SectionのResponsibility Decomposition（責務分解）として、包含するConvention Asset（規約資産）へ割り当てられたConvention Code（規約コード）のConcrete Assignment（具体割当）を宣言することである。

**Reason:** Convention Code（規約コード）は、その規約が定めるRule ID（規則ID）の解釈に必要な前提である。どの値が割り当てられているかを保持する責務は、Conventions Area（規約領域）の資産へ反復して現れる。共通のIdentity（同一性）を与えることで、その所在を資産横断で同じ根拠から確認できる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

Convention Authoring Conventionに存在するConvention Code（規約コード）関連のSectionと、Heading Stringが一致することだけを理由として、同一のStandard Section Identity（標準Section同一性）とみなさない。Standard Section Identity（標準Section同一性）はApplicability Scope（適用範囲）とSection Responsibility（Section責務）によって成立する。

#### RDS-SF-007 — Namespace Code Standard Section（名前空間コード標準Section）

**Rule ID:** `RDS-SF-007`

**Rule Name:** Namespace Code Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびConventions Area（規約領域）とするNamespace Code Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Concrete Declarations Standard SectionのResponsibility Decomposition（責務分解）として、当該Convention Asset（規約資産）のNormative Rulesが使用する割当済みNamespace Code（名前空間コード）をConcrete Declarationとして示すことである。

**Reason:** Rule ID（規則ID）はConvention（規約）とNamespaceの組合せの中で成立する。自身のRuleがどのNamespace Code（名前空間コード）に属するかが示されなければ、Rule ID（規則ID）の一意性の根拠が確定しない。この責務は、Conventions Area（規約領域）の資産へ反復して現れる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

Convention Authoring Conventionの`Namespace Code Assignment` とは別のStandard Section Identity（標準Section同一性）である。本Standard Section（標準Section）が担うのは、当該資産が使用するNamespace Code（名前空間コード）の宣言である。`Namespace Code Assignment` が担うのは、Namespace Code（名前空間コード）そのものの割当である。両者を同一の責務として扱わない。

#### RDS-SF-008 — Normative Rules Standard Section（規範的ルール標準Section）

**Rule ID:** `RDS-SF-008`

**Rule Name:** Normative Rules Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびConventions Area（規約領域）とするNormative Rules Standard Sectionを定義する。そのSection Responsibility（Section責務）は、Convention（規約）がNormative Effectを持たせるNormative Rule（規範的規則）群を保持し、Non-normative Content（非規範的内容）から意味的に区別することである。

**Reason:** Convention Asset（規約資産）は、規範的効力を持つ内容と持たない内容を併せ持つ。どこからどこまでが規範であるかが構造から判別できなければ、補足や説明が規範として運用され、あるいは規範が参考情報として扱われる。この区別を保持する責務は、Conventions Area（規約領域）の資産へ反復して現れる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）は、個々のNormative Rule（規範的規則）およびそのCategory（分類）を、Standard Section（標準Section）として定義しない。

#### RDS-SF-009 — Self Application Standard Section（自己適用標準Section）

**Rule ID:** `RDS-SF-009`

**Rule Name:** Self Application Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）をRepository Governance Documentation FrameworkおよびConventions Area（規約領域）とするSelf Application Standard Sectionを定義する。そのSection Responsibility（Section責務）は、当該Convention Asset（規約資産）自身へ適用されるConvention（規約）およびRuleについて、そのSelf ApplicationおよびConformanceを明確にすることである。

**Reason:** Convention Asset（規約資産）は、自身も他のConvention（規約）の適用対象であり、場合によっては自身が定めるRuleの適用対象でもある。その適合状況が示されなければ、規約が自身に適用されない例外として運用され、規約の妥当性を自身の記述から検証できなくなる。この責務は、Conventions Area（規約領域）の資産へ反復して現れる。

**Note:** 本Ruleは定義であり、Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）はNon-normative Content（非規範的内容）を保持する責務であり、新たなNormative Requirement（規範要求）を成立させない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、[Convention Authoring Convention](convention-authoring.md)が定めるRuleに従って記述されている。

- Convention Code（規約コード）を「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が`RDS-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）が、必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が`Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、`Retired Rule IDs` の記録を設けていない。

また本文書は、[Documentation Structure Convention](documentation-structure.md)および本文書自身が定めるRuleにも従っている。

- Document Responsibility（文書責務）を内容から識別可能にしている。
- Purpose・Relationships・Scopeの各Standard Section Identity（標準Section同一性）を、それぞれの責務に適合するSectionへ使用している。
- 本文書はConventions Area（規約領域）に属するため、Conventions Area（規約領域）をApplicability Scope（適用範囲）に含むStandard Section（標準Section）が適用可能である。Concrete Declarations・Convention Code（規約コード）・Namespace Code（名前空間コード）・Normative Rules・Self Applicationの各Section Responsibility（Section責務）を独立したSectionとして構成しているため、対応するStandard Section Identity（標準Section同一性）を使用している。
- 本文書はConventions Area（規約領域）に属するため、Architecture Area（アーキテクチャ領域）をApplicability Scope（適用範囲）に含むStandard Section（標準Section）は適用されない。
- Relationships Standard SectionのResponsibility Decomposition（責務分解）として構成しているSectionへ、Position・Responsibility BoundaryのStandard Section Identity（標準Section同一性）を使用している。
- Scope Standard SectionのResponsibility Decomposition（責務分解）として構成しているSectionへ、In Scope・Out of ScopeのStandard Section Identity（標準Section同一性）を使用している。
- その他のSectionはDocument-specific Section（文書固有Section）である。
- 本文書が定義するStandard Section（標準Section）のStandard Section Heading Representation（標準Section見出し表現）を、「Concrete Declarations」で宣言している。
- 本文書自身のPosition・Concrete Declarations・Convention Code（規約コード）・Namespace Code（名前空間コード）・Normative Rules・Self ApplicationのHeading（見出し）は、宣言したStandard Section Heading Representation（標準Section見出し表現）と一致している。
- Concept Model（概念モデル）・Design Principles・Non-goalsのStandard Section Identity（標準Section同一性）は、Architecture Area（アーキテクチャ領域）をApplicability Scope（適用範囲）に含むため、Conventions Area（規約領域）に属する本文書ではHeading（見出し）として表現していない。
- 本文書自身のPurpose・Relationships・Responsibility Boundary・Scope・In Scope・Out of ScopeのHeading（見出し）は、[Documentation Structure Convention](documentation-structure.md)が宣言したStandard Section Heading Representation（標準Section見出し表現）と一致している。

本文書自身のHeading Level（見出しレベル）・Markdown Heading Marker（Markdown見出し記号）・Section Order（Section順序）は、本文書が定めるものではない。

本節はNon-normative Content（非規範的内容）であり、新たなNormative Requirement（規範要求）を追加しない。
