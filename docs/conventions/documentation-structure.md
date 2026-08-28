# Documentation Structure Convention（文書構造規約）

## Purpose（目的）

本文書は、`noxris42` において
**Documentation Asset（文書資産）の内部Semantic Structure（意味構造）について、
Document Responsibility（文書責務）に従う
Section Structureの構成規範と、
複数のDocumentation Asset（文書資産）へ反復適用される
Standard Section Mechanismおよび
Documentation-wide Standard Sectionsを定義し、
一貫して適用可能にする
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の3点である。

1. Documentation Asset（文書資産）のSection Structureは、
   何に基づいて成立していなければならないのか。
2. 複数のDocumentation Asset（文書資産）へ反復適用される
   Standard Section（標準Section）は、
   どのような機構として成立するのか。
3. 現在、Documentation全体へ適用される
   Standard Section（標準Section）として何が成立するのか。

[Documentation Structure Architecture](../architecture/documentation-structure.md)
は、Section・Section Responsibility（Section責務）・
Responsibility Decomposition（責務分解）の一般
Semantic Model（意味モデル）を定義する。
ただし同Architectureは、具体的な
Standard Section（標準Section）を意図的に定義せず、
後続のConvention（規約）へ委譲している。

本文書はその委譲先として、
一般Section Modelを前提に、
Sectionの適用に関する規範、
Standard Section（標準Section）の一般機構、および
現在成立するDocumentation-wide Standard Sectionsを定める。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は
[Documentation Structure Architecture](../architecture/documentation-structure.md)
および
[Convention Authoring Convention](convention-authoring.md)
を上位Sourceとして参照する。

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ refines
Documentation Structure Convention

Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Documentation Structure Convention
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Documentation Asset（文書資産）という反復的に成立する成果物へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Areaを代表・集約するAssetではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- SectionとSection Responsibility（Section責務）
- Section Responsibility（Section責務）が
  Document Responsibility（文書責務）の
  Responsibility Boundary（責務境界）に従属すること
- Nested Section Structureにおける
  Responsibility Decomposition（責務分解）
- `Section ≠ Heading` をはじめとする
  Logical / Representation Boundary
- Documentation Framework（文書体系）と
  Documentation Area（文書責務領域）
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的ルール）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（ルールモデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（ルール同一性）とその安定性
- Rule ID Format（規約ルールID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  StabilityのField表現
- Namespace Code（名前空間コード）の割当

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Documentation Asset（文書資産）から
  Document Responsibility（文書責務）を識別可能にする要求
- Sectionを構成する場合の
  Section Responsibility（Section責務）に関する要求
- Section Responsibility（Section責務）および
  Child Section Responsibilityの
  Responsibility Boundary（責務境界）に関する要求
- Standard Section（標準Section）の定義要件、
  Applicability Scope（適用範囲）に基づく適用、
  Standard Section Identity（標準Section同一性）の選択と適合
- Standard Section Definitionと
  Presence Requirement（設置要求）の分離
- Standard Section Heading Representation（標準Section見出し表現）の
  定義方法、およびその定義権限の所在
- 定義済みStandard Section Heading Representation（標準Section見出し表現）の
  再利用要求
- 本文書が定義するDocumentation-wide Standard Sections
  のうち、Standard Section Heading Representation（標準Section見出し表現）を
  宣言するものについてのConcrete Heading Representation
- Standard Section Catalogの開放性と、
  Document-specific Section（文書固有Section）の許容
- Applicability Scope（適用範囲）を跨ぐ
  Standard Identityの非重複
- Documentation-wide Standard Sectionsの
  Section Responsibility（Section責務）、
  他のStandard Section（標準Section）の
  Responsibility Decomposition（責務分解）として成立する場合の
  その関係、および
  必要な場合のPresence Requirement（設置要求）

### Out of Scope（本文書が定義しない範囲）

- Section・Section Responsibility（Section責務）・
  Responsibility Decomposition（責務分解）の
  一般Semantic Model（意味モデル）
- すべてのDocumentation Asset（文書資産）へ要求される
  Fixed Section Set、
  およびSection Order（Section順序）
- Section Responsibilitiesによる
  Document Responsibility（文書責務）のCoverage（網羅）要求
- Framework-scoped / Area-scoped Standard Section
  の具体Catalog
- Applicability Scope（適用範囲）粒度の
  Closed Taxonomy
- SectionとHeading（見出し）・Heading Level（見出しレベル）の
  Mapping Rule（対応規則）
- Document-specific Section（文書固有Section）の
  Heading Representation（見出し表現）のModel
- Heading Registry等、
  Heading Representation（見出し表現）の中央登録簿
- Section Identifier、
  Section Registry
- Standard Section Heading Representation（標準Section見出し表現）の
  定義および再利用を除く、
  Natural Language Representation（自然言語表現）、
  日英表記、文体、用語選択
- Markdown Syntax、Markdown Heading Marker（Markdown見出し記号）、
  その他Markdown固有の表現
- File名、Directory名、Path等のNaming Convention
- Document Title（文書題名）、Formal Asset Name、
  およびそれらの構成規則
- Documentation Asset（文書資産）間の
  Dependency（依存）・Refinement（具体化）関係のModel
- MetadataおよびDeclarationのSchema、
  Template
- Validation・Lint等のTool要求
- Documentation Lifecycle（文書の生涯管理）・Review

## Concrete Declarations（具体宣言）

本節はConcrete Assignment（具体割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: DST
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

### Standard Section Heading Representation（標準Section見出し表現）

本文書が定義するDocumentation-wide Standard Sections
のうち、次に挙げるものに対する
Standard Section Heading Representation（標準Section見出し表現）を、
Standard Section（標準Section）ごとに次のとおり宣言する。
ここに挙げないStandard Section（標準Section）については、
Standard Section Heading Representation（標準Section見出し表現）を宣言しない。
以下の宣言はいずれも、
Standard Section Identity（標準Section同一性）の
Meaning（意味）を変更しない。

以下の各Child Section（子Section）のHeading（見出し）は、
どのStandard Section（標準Section）に対する
Concrete Assignment（具体割当）を宣言しているかを示すものであり、
Standard Section Heading Representation（標準Section見出し表現）そのものではない。

#### Purpose Standard Section（目的標準Section）

```text
Standard Section:                Purpose
English Heading Representation:  Purpose
Japanese Heading Explanation:    目的
```

#### Scope Standard Section（対象範囲標準Section）

```text
Standard Section:                Scope
English Heading Representation:  Scope
Japanese Heading Explanation:    対象範囲
```

`Scope` のJapanese Heading Explanation（日本語見出し説明）を
`対象範囲` とするのは、当該Standard Section（標準Section）が
適用される範囲だけでなく、何を扱い何を扱わないかという
Responsibility Boundary（責務境界）まで含むためである。

#### Relationships Standard Section（関係標準Section）

```text
Standard Section:                Relationships
English Heading Representation:  Relationships
Japanese Heading Explanation:    関係
```

`Relationships` のJapanese Heading Explanation（日本語見出し説明）を
`関係` とするのは、当該Standard Section（標準Section）が
他のDocumentation Asset（文書資産）・Responsibility（責務）・
Concept（概念）等とのSemantic Relationship全般を
対象とするためである。

#### In Scope Standard Section（対象範囲内標準Section）

```text
Standard Section:                In Scope
English Heading Representation:  In Scope
Japanese Heading Explanation:    本文書が定義する範囲
```

#### Out of Scope Standard Section（対象範囲外標準Section）

```text
Standard Section:                Out of Scope
English Heading Representation:  Out of Scope
Japanese Heading Explanation:    本文書が定義しない範囲
```

`In Scope` / `Out of Scope` のJapanese Heading Explanation（日本語見出し説明）
を
`本文書が定義する範囲` / `本文書が定義しない範囲` とするのは、
両者がいずれもScope Standard Sectionの
Responsibility Decomposition（責務分解）であり、
当該Documentation Asset（文書資産）自身の
Document Responsibility（文書責務）の内外を対象とすることを
示すためである。

#### Responsibility Boundary Standard Section（責務境界標準Section）

```text
Standard Section:                Responsibility Boundary
English Heading Representation:  Responsibility Boundary
Japanese Heading Explanation:    責務境界
```

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的ルール）を読むための補足である。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。
Standard Section（標準Section）の要件・適用・責務は、
すべてNormative Rule（規範的ルール）側で確定する。

### Standard Section（標準Section）の位置づけ

Standard Section（標準Section）は、
複数のDocumentation Asset（文書資産）へ反復適用され得る
Section Responsibility（Section責務）に対して、
共通のStandard Section Identity（標準Section同一性）を与える機構である。

この機構が分離しているのは次の3点である。

```text
Standard Section Definition
    ≠ Presence Requirement

Standard Section Identity
    ≠ Heading Representation

Standard Section Catalog
    ≠ Closed Section Vocabulary
```

Standard Section Identity（標準Section同一性）は
Section Responsibility（Section責務）とApplicability Scope（適用範囲）によって成立する。
Heading（見出し）の文字列、Heading Level（見出しレベル）、
Markdown Marker、Section Order（Section順序）は
その成立条件ではない。

`Purpose`・`Scope`・`Relationships`・
`In Scope`・`Out of Scope`・`Responsibility Boundary` は
Standard Section Identity（標準Section同一性）を指す名称であり、
それ自体がHeading（見出し）として記述されるべき
Heading Representation（見出し表現）であることを意味しない。
Heading Representation（見出し表現）は、
Standard Section Heading Representation（標準Section見出し表現）として
別に定義された場合にのみ成立する。

### Standard Section Heading Representation（標準Section見出し表現）

Standard Section Heading Representation（標準Section見出し表現）は、
Standard Section Identity（標準Section同一性）を
Human-readable Headingとして表現するための
Representation（表現）である。
Identity（同一性）の成立条件ではない。

現在成立するModelは次である。

```text
Standard Section
    │
    ├─ Standard Section Identity
    │     ├─ Applicability Scope
    │     └─ Section Responsibility
    │
    └─ 0..1 Standard Section Heading Representation
          ├─ English Heading Representation
          └─ Japanese Heading Explanation
```

Standard Section Heading Representation（標準Section見出し表現）は
`0..1` である。
定義されていないことは、
Standard Section（標準Section）の成立を妨げない。

同一のHeading（見出し）文字列であることから
Standard Section Identity（標準Section同一性）を導出しない。

Japanese Heading Explanation（日本語見出し説明）は
Canonical Japanese Support Representation（正規日本語補助表現）ではない。

```text
Japanese Heading Explanation
    ≠ Canonical Japanese Support Representation

same value
    ≠ same semantic responsibility
```

同一のJapanese Valueが
Canonical Japanese Support（正規日本語補助）側にも存在し得ることは
禁止されない。
両者はSemantic Responsibility（意味上の責務）が異なる。

Standard Section Heading Representation（標準Section見出し表現）には
Preferred / Canonical等の複数段階を設けない。
定義されたRepresentation（表現）が存在する場合、
それが再利用の対象である。

Definition Authority（定義権限）の所在は次である。

```text
Standard Sectionの意味定義
    → そのStandard Sectionを定義するConvention

Standard Section Heading Representationの機構
    → 本文書

具体のStandard Section Heading Representation
    → そのStandard Sectionを定義するConvention
```

したがって中央のHeading Registryは導入しない。

本機構はStandard Section Identity（標準Section同一性）にのみ適用される。
Document-specific Section（文書固有Section）の
Heading Representation（見出し表現）へは自動的に適用されない。

### Applicability Scope（適用範囲）

Applicability Scope（適用範囲）は、
あるStandard Section（標準Section）が
どのDocumentation Asset（文書資産）に対して適用され得るかを示す。

本文書が今回定義するStandard Section（標準Section）の
Applicability Scope（適用範囲）は
Documentation-wideのみである。
Framework-scoped / Area-scoped Standard Section
の具体Catalogは、
本文書では定義しない。

### 責務との境界

本文書が扱うのは、Sectionの適用、
Section Responsibility（Section責務）との整合、および
Standard Section（標準Section）の機構と責務までである。

次は本文書の責務ではない。

- Standard Section Heading Representation（標準Section見出し表現）の
  定義および再利用を除く、
  Natural Language Representation（自然言語表現）、
  日英表記、文体、用語選択
- Markdown Syntax、Heading Marker等の
  Markdown固有表現
- File / Directory / Path等の命名

本文書は、これらの責務を担うConvention（規約）の
存在や内容を前提とせず、
それらを本文書側で新たに成立させることもしない。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的ルール）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Section Structure（Section構造）

#### DST-SF-001 — Document Responsibility Clarity

**Rule ID:** `DST-SF-001`

**Rule Name:** Document Responsibility Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Documentation Asset（文書資産）は、
自身が何を保持・提供する責務を担うのか、
すなわちDocument Responsibility（文書責務）を、
その内容から識別可能にしなければならない。

**Reason:** Document Responsibility（文書責務）は、
Documentation Asset（文書資産）の意味と責務範囲を成立させる
Semantic Basis（意味上の基礎）である。
それが内容から識別できなければ、
その資産に何を書くべきか、何を書くべきでないかを判断できず、
Sectionの妥当性も評価できない。

**Note:** 本Ruleは識別可能性のみを要求する。
どのSectionでそれを担うかは要求しない。
Purpose Standard Sectionの
Presence Requirement（設置要求）は `DST-SF-013` が別に定める。

#### DST-SF-002 — Responsibility-based Sectioning

**Rule ID:** `DST-SF-002`

**Rule Name:** Responsibility-based Sectioning

**Stability:** Development

**Requirement:** MUST

**Rule:** Documentation Asset（文書資産）がSectionを構成する場合、
各Sectionは、
Document Responsibility（文書責務）を内部で分担する
Section Responsibility（Section責務）に基づかなければならない。

**Reason:** Sectionは
Section Responsibility（Section責務）によって成立する
Semantic Unitである。
責務に基づかない区切りが混在すると、
内部構成が意味構造ではなく記述量や体裁の都合で決まり、
どこに何を書くかの判断根拠が失われる。

#### DST-SF-003 — Section Responsibility Boundary

**Rule ID:** `DST-SF-003`

**Rule Name:** Section Responsibility Boundary

**Stability:** Development

**Requirement:** MUST

**Rule:** Section Responsibility（Section責務）は、
包含するDocumentation Asset（文書資産）の
Document Responsibility（文書責務）の範囲内に
留まらなければならない。

**Reason:** 責務境界を越えたSectionは、
その資産が担っていない責務を実質的に持ち込む。
結果として、その資産自身の
Responsibility Boundary（責務境界）が崩れ、
その内容を保持・提供する責務を
どの資産が担っているのかが不明確になる。

#### DST-SF-004 — Child Section Responsibility Boundary

**Rule ID:** `DST-SF-004`

**Rule Name:** Child Section Responsibility Boundary

**Stability:** Development

**Requirement:** MUST

**Rule:** Child Section（子Section）の
Section Responsibility（Section責務）は、
Parent Sectionの
Section Responsibility（Section責務）を
分担または具体化する範囲内に留まらなければならない。

**Reason:** 親子関係の意味は
Responsibility Decomposition（責務分解）である。
子が親の範囲外の責務を持つと、
入れ子構造が責務分解ではなく単なる配置となり、
どの階層がどこまでを担うのかを構造から読み取れなくなる。

### Standard Section Mechanism（標準Section機構）

#### DST-SF-005 — Standard Section Definition

**Rule ID:** `DST-SF-005`

**Rule Name:** Standard Section Definition

**Stability:** Development

**Requirement:** MUST

**Rule:** Standard Section（標準Section）は、
少なくともApplicability Scope（適用範囲）と
Section Responsibility（Section責務）を明示して
定義しなければならない。

**Reason:** この2つが欠けると、
そのStandard Section（標準Section）が
どのDocumentation Asset（文書資産）に関係し、
何を保持・提供する責務なのかが確定しない。
確定しないStandard Section（標準Section）は、
名称の一致だけで異なる責務へ適用され、
共通化した意味が失われる。

#### DST-SF-006 — Standard Section Applicability

**Rule ID:** `DST-SF-006`

**Rule Name:** Standard Section Applicability

**Stability:** Development

**Requirement:** MUST

**Rule:** Standard Section（標準Section）は、
そのApplicability Scope（適用範囲）に含まれる
Documentation Asset（文書資産）にのみ適用する。

**Reason:** 適用範囲を限定しなければ、
特定のDocumentation Framework（文書体系）や
Documentation Area（文書責務領域）の事情に由来する標準が、
無関係な資産へ波及する。
Applicability Scope（適用範囲）を適用条件とすることで、
標準の妥当性がその範囲の中で評価できる。

**Note:** 現在必要なScope粒度として、
Documentation-wide、
Framework-wide、
Framework（体系） + Areaを扱える。
これは現時点で必要な粒度の例示であり、
将来にわたるClosed Taxonomyではない。

#### DST-SF-007 — Standard Identity Selection

**Rule ID:** `DST-SF-007`

**Rule Name:** Standard Identity Selection

**Stability:** Development

**Requirement:** MUST

**Rule:** Documentation Asset（文書資産）が、
適用可能なStandard Section（標準Section）と
同一のSection Responsibility（Section責務）を
独立したSectionとして構成する場合、
対応するStandard Section Identity（標準Section同一性）を
使用しなければならない。

**Reason:** 同じ責務が資産ごとに別のIdentity（同一性）で現れると、
標準として共通化した意味が反復適用されず、
読み手は同じ責務のSectionを毎回別物として解釈することになる。

**Note:** 責務の部分一致や類似だけでは本Ruleは適用されない。
Section Responsibility（Section責務）が同一である場合に限られる。

#### DST-SF-008 — Standard Identity Conformance

**Rule ID:** `DST-SF-008`

**Rule Name:** Standard Identity Conformance

**Stability:** Development

**Requirement:** MUST

**Rule:** Standard Section Identity（標準Section同一性）を使用する
Sectionは、
そのStandard Section（標準Section）の
Section Responsibility（Section責務）へ適合しなければならない。

**Reason:** Identity（同一性）と責務が一致しなければ、
読み手はそのSectionから得られる情報を予測できず、
Standard Section（標準Section）は名称の慣習に退化する。
適合を要求することで、
Identity（同一性）が責務の保証として機能する。

#### DST-SF-009 — Standard Identity and Presence Separation

**Rule ID:** `DST-SF-009`

**Rule Name:** Standard Identity and Presence Separation

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Standard Section（標準Section）として
定義されていることだけを根拠として、
そのSectionの設置を要求してはならない。

**Reason:** 定義と設置要求を同一視すると、
Standard Section（標準Section）を追加するたびに
すべての対象資産へ実質的な必須Sectionが増え、
Fixed Section Setと変わらなくなる。
設置の要否は、その資産の
Document Responsibility（文書責務）に照らして
個別に判断されるべきである。

**Note:** Presence Requirement（設置要求）が必要な場合は、
そのStandard Section（標準Section）ごとに
独立したNormative Rule（規範的ルール）として定める。

#### DST-SF-010 — Open Section Vocabulary

**Rule ID:** `DST-SF-010`

**Rule Name:** Open Section Vocabulary

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Standard Section Catalogを、
使用可能なSection Responsibility（Section責務）または
Section Identity（Section同一性）の
Closed Set（閉じた集合）として扱ってはならない。

**Reason:** Document Responsibility（文書責務）は資産ごとに異なるため、
必要な責務の集合を事前に列挙し尽くすことはできない。
一覧を閉じた語彙として扱うと、
責務上必要な情報が既存の枠へ押し込まれ、
Section Responsibility（Section責務）が不明瞭になる。

**Note:** Open Vocabularyであることの帰結として、
適用可能なStandard Section（標準Section）に一致しない
Section Responsibility（Section責務）は、
一致しないことだけを理由として排除されない。
そうした責務がDocument Responsibility（文書責務）を果たすために
必要な場合、
Document-specific Section（文書固有Section）として構成できる。

#### DST-SF-011 — Standard Section Non-duplication

**Rule ID:** `DST-SF-011`

**Rule Name:** Standard Section Non-duplication

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** より広いApplicability Scope（適用範囲）で
すでに定義されたStandard Section（標準Section）と
同一のSection Responsibility（Section責務）について、
より狭いScopeで
別のStandard Section Identity（標準Section同一性）を
定義してはならない。

**Reason:** 同一責務に複数のIdentity（同一性）が並立すると、
どちらを使用すべきかがScopeの重なりによって決まり、
`DST-SF-007` によるIdentity（同一性）の選択が一意に定まらなくなる。
広いScopeの定義を唯一のIdentity（同一性）とすることで、
同じ責務が常に同じIdentity（同一性）で現れる。

**Note:** より狭いScopeにおいて、
既存Standard Section（標準Section）の
Section Responsibility（Section責務）と
異なる責務が必要な場合は、
別のStandard Section（標準Section）としての定義を妨げない。

### Standard Section Heading Representation（標準Section見出し表現）

#### DST-SF-018 — Standard Section Heading Representation Definition

**Rule ID:** `DST-SF-018`

**Rule Name:** Standard Section Heading Representation Definition

**Stability:** Development

**Requirement:** MUST

**Rule:** Standard Section（標準Section）に対して
Standard Section Heading Representation（標準Section見出し表現）を
定義する場合、
その定義は、当該Standard Section（標準Section）を定義する
Convention（規約）上で行い、
1つのStandard Section（標準Section）につき最大1つとし、
English Heading Representationと、
それに対応するJapanese Heading Explanation（日本語見出し説明）によって
構成しなければならない。

**Reason:** 同一のStandard Section Identity（標準Section同一性）は
複数のDocumentation Asset（文書資産）でHeading（見出し）として
表現され得る。
再利用可能なHuman-readable Heading Representationが
定義されていなければ、
同じ責務のSectionが資産ごとに異なる見出しで現れる。
定義の所在をStandard Section（標準Section）の定義側へ置くのは、
Identity（同一性）とその表現の定義権限を分散させないためである。

**Note:** 本Ruleは
Standard Section Heading Representation（標準Section見出し表現）を
定義することを要求しない。
定義するかどうかは任意であり、
本Ruleが必須とするのは定義する場合の構成条件のみである。
定義されていないことは、
`DST-SF-005` によるStandard Section（標準Section）の成立を妨げない。
Japanese Heading Explanation（日本語見出し説明）は
当該Heading Representation（見出し表現）を日本語で説明するものであり、
Canonical Japanese Support Representation（正規日本語補助表現）ではない。

#### DST-SF-019 — Standard Section Heading Representation Reuse

**Rule ID:** `DST-SF-019`

**Rule Name:** Standard Section Heading Representation Reuse

**Stability:** Development

**Requirement:** MUST

**Rule:** Standard Section Heading Representation（標準Section見出し表現）が
定義されているStandard Section Identity（標準Section同一性）を、
Documentation Asset（文書資産）がHeading（見出し）として表現する場合、
定義されたStandard Section Heading Representation（標準Section見出し表現）を
使用しなければならない。

**Reason:** 定義された表現が使用されなければ、
表現は資産ごとに分岐し、
読み手は同じ責務のSectionを毎回別の見出しから解釈することになる。
再利用を要求することで、
Identity（同一性）と表現の対応が資産横断で一定に保たれる。

**Note:** 本RuleはHeading（見出し）による表現を要求しない。
Heading（見出し）として表現する場合の表現のみを定める。
本Ruleは
Standard Section Identity（標準Section同一性）にのみ適用され、
Document-specific Section（文書固有Section）へは適用されない。

### Documentation-wide Standard Sections（Documentation全体標準Section）

#### DST-SF-012 — Purpose Standard Section

**Rule ID:** `DST-SF-012`

**Rule Name:** Purpose Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
Purpose Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Documentation Asset（文書資産）が
何を保持・提供するために存在するのか、
すなわちそのDocument Responsibility（文書責務）と
文書として果たす役割を明確にすることである。

**Reason:** Document Responsibility（文書責務）は
すべてのDocumentation Asset（文書資産）に成立する責務であり、
それを明確にする責務も資産の種類を問わず反復して必要になる。
共通のIdentity（同一性）を与えることで、
読み手は資産の役割を一貫した根拠から確認できる。

**Note:** 本Ruleは定義であり、
設置を要求しない。
Presence Requirement（設置要求）は `DST-SF-013` が定める。

#### DST-SF-013 — Purpose Presence

**Rule ID:** `DST-SF-013`

**Rule Name:** Purpose Presence

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Documentation Asset（文書資産）は、
Purpose Standard Sectionを持つ。

**Reason:** Document Responsibility（文書責務）が
独立した責務として明示されない場合、
読み手は本文全体からその役割を推測することになり、
その資産が何を保持・提供する存在なのかの解釈が読み手ごとに分かれる。

**Note:** 短いAssetで、
Document Responsibility（文書責務）が他の内容から十分に明確であり、
独立したPurpose Sectionが
Semantic Clarityを実質的に増加させない場合は
省略できる。

#### DST-SF-014 — Scope Standard Section

**Rule ID:** `DST-SF-014`

**Rule Name:** Scope Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
Scope Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Document Responsibility（文書責務）が適用される範囲および
必要な境界を明示し、
Documentation Asset（文書資産）が
何を扱い、何を扱わないかを区別可能にすることである。

**Reason:** 責務境界の明示は、
資産の種類を問わず必要になり得る反復的な責務である。
共通のIdentity（同一性）を与えることで、
境界の確認と見直しを資産横断で同じ根拠から行える。

**Note:** 本Ruleは定義であり、
設置を要求しない。
Scope Informationの保持要求は `DST-SF-015` が、
Sectionとしての構成は `DST-SF-016` が定める。

#### DST-SF-015 — Scope Information Requirement

**Rule ID:** `DST-SF-015`

**Rule Name:** Scope Information Requirement

**Stability:** Development

**Requirement:** MUST

**Rule:** Document Responsibility（文書責務）の
適用範囲または境界を明示しなければ
Material Ambiguityが生じる場合、
Documentation Asset（文書資産）は
必要なScope Informationを
保持しなければならない。

**Reason:** 責務境界が曖昧なまま残ると、
その資産が扱わない事柄が扱われているものとして参照され、
あるいは扱うべき事柄が他所で重複して定義される。
曖昧さが実際に生じる場合に限定するのは、
境界が自明な資産にまで形式的な記述を強いないためである。

**Note:** 本Ruleが要求するのは情報の保持であり、
独立したScope Sectionの設置ではない。

#### DST-SF-016 — Scope Presence

**Rule ID:** `DST-SF-016`

**Rule Name:** Scope Presence

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Scope Informationが
独立したSection Responsibility（Section責務）としての
意味的まとまりを持ち、
その分離が責務境界の理解を改善する場合、
Scope Standard Sectionとして構成する。

**Reason:** 境界に関する情報が本文各所へ散在すると、
その資産の境界を確認するために全体を読む必要が生じる。
一方、分離する意味がない場合にまで独立Sectionを要求すると、
責務を持たない区切りが増える。

**Note:** `In Scope` / `Out of Scope` 等を
固定のChild Section（子Section）として要求しない。

#### DST-SF-017 — Relationships Standard Section

**Rule ID:** `DST-SF-017`

**Rule Name:** Relationships Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
Relationships Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Documentation Asset（文書資産）またはそのSubjectが、
他のDocumentation Asset（文書資産）・Responsibility（責務）・
Concept（概念）等と持つ、
当該Assetの意味成立に必要な
Semantic Relationshipを明確にすることである。

**Reason:** 資産の意味は、
それ単体で閉じているとは限らない。
上位Source・Definition Authority（定義権限）の所在・
他資産との責務境界といった関係が示されなければ、
その資産の内容をどの前提の下で読むべきかが確定しない。
この責務は資産の種類を問わず反復して現れる。

**Note:** 本Ruleは定義であり、
Presence Requirement（設置要求）を定めない。

#### DST-SF-020 — In Scope Standard Section

**Rule ID:** `DST-SF-020`

**Rule Name:** In Scope Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
In Scope Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Scope Standard Sectionの
Responsibility Decomposition（責務分解）として、
当該Documentation Asset（文書資産）が
Document Responsibility（文書責務）の範囲内で扱う事項を
明確にすることである。

**Reason:** 何を扱うかと何を扱わないかは、
いずれもResponsibility Boundary（責務境界）を構成するが、
読み手と書き手が参照する場面は異なる。
扱う事項の側を独立した責務として分離できる場合、
その責務は資産の種類を問わず反復して現れる。
共通のIdentity（同一性）を与えることで、
その所在を資産横断で同じ根拠から確認できる。

**Note:** 本Ruleは定義であり、
Presence Requirement（設置要求）を定めない。
`DST-SF-016` は
`In Scope` / `Out of Scope` 等を固定のChild Section（子Section）として
要求しない旨を定めており、本Ruleはこれを変更しない。

本Standard Section（標準Section）と
Scope Standard Sectionの関係は、
Responsibility Decomposition（責務分解）である。
Scope Standard Sectionの責務のうち、
分解されていない部分は
Scope Standard Section自身が直接担う。

#### DST-SF-021 — Out of Scope Standard Section

**Rule ID:** `DST-SF-021`

**Rule Name:** Out of Scope Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
Out of Scope Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Scope Standard Sectionの
Responsibility Decomposition（責務分解）として、
当該Documentation Asset（文書資産）が
Document Responsibility（文書責務）の範囲外として扱わない事項を
明確にすることである。

**Reason:** 扱わない事項が明示されなければ、
その資産が担っていない事柄が担われているものとして参照され、
あるいは担うべき事柄が他所で重複して定義される。
この責務を独立して保持できる場合、
その責務は資産の種類を問わず反復して現れる。
共通のIdentity（同一性）を与えることで、
その所在を資産横断で同じ根拠から確認できる。

**Note:** 本Ruleは定義であり、
Presence Requirement（設置要求）を定めない。

本Standard Section（標準Section）が担うのは、
Document Responsibility（文書責務）の範囲外であるという
Responsibility Boundary（責務境界）上の事実である。
Architecture Asset（アーキテクチャ資産）が
自身の責務範囲を踏まえたうえで意図的に定義・解決しないという
設計判断は、これとは別の責務である。

#### DST-SF-022 — Responsibility Boundary Standard Section

**Rule ID:** `DST-SF-022`

**Rule Name:** Responsibility Boundary Standard Section

**Stability:** Development

**Requirement:** MUST

**Rule:** Applicability Scope（適用範囲）を
Documentation-wideとする
Responsibility Boundary Standard Sectionを定義する。
そのSection Responsibility（Section責務）は、
Relationships Standard Sectionの
Responsibility Decomposition（責務分解）として、
当該Documentation Asset（文書資産）が担う
Responsibility（責務）およびDefinition Authority（定義権限）と、
隣接する責務主体とのBoundary（境界）を
明確にすることである。

**Reason:** 他の責務主体との関係のうち、
どこまでを自身が担い、どこから先を他が担うのかという境界は、
参照関係や依存関係の記述とは別の判断根拠として使われる。
この境界を独立した責務として保持できる場合、
その責務は資産の種類を問わず反復して現れる。
共通のIdentity（同一性）を与えることで、
Definition Authority（定義権限）の所在を
資産横断で同じ根拠から確認できる。

**Note:** 本Ruleは定義であり、
Presence Requirement（設置要求）を定めない。

Scope Standard Sectionとは
Section Responsibility（Section責務）が異なる。
Scope Standard Sectionが担うのは、
当該資産自身のDocument Responsibility（文書責務）が
適用される範囲および境界である。
本Standard Section（標準Section）が担うのは、
隣接する責務主体との間で
Responsibility（責務）およびDefinition Authority（定義権限）が
どこで分かれるかである。

本Standard Section（標準Section）と
Relationships Standard Sectionの関係は、
Responsibility Decomposition（責務分解）である。
Relationships Standard Sectionの責務のうち、
分解されていない部分は
Relationships Standard Section自身が直接担う。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRuleに従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `DST-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書は、自身が定めるRuleにも従っている。

- Document Responsibility（文書責務）を内容から識別可能にしている。
- Purpose・Scope・Relationshipsの各
  Standard Section Identity（標準Section同一性）を、
  それぞれの責務に適合するSectionへ使用している。
- Scope Standard Sectionの
  Responsibility Decomposition（責務分解）として構成しているSectionへ、
  In Scope・Out of Scopeの
  Standard Section Identity（標準Section同一性）を使用している。
- Responsibility Boundary Standard Sectionに対応する
  Section Responsibility（Section責務）は、
  独立したSectionとして構成していない。
- その他のSectionは
  Document-specific Section（文書固有Section）である。
- 本文書が定義するStandard Section（標準Section）のうち、
  Standard Section Heading Representation（標準Section見出し表現）を
  宣言するものについて、その宣言を
  「Concrete Declarations」で行っている。
- 本文書自身のPurpose・Scope・Relationships・
  In Scope・Out of ScopeのHeading（見出し）は、
  宣言したStandard Section Heading Representation（標準Section見出し表現）と
  一致している。
- Responsibility Boundary（責務境界）のStandard Section Identity（標準Section同一性）は、
  対応するSectionを構成していないためHeading（見出し）として
  表現しておらず、`DST-SF-019` による再利用要求は生じない。

本文書自身のHeading Level（見出しレベル）・Section Order（Section順序）・
Markdown Heading Marker（Markdown見出し記号）は、
本文書が定めるものではない。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
