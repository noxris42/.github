# Documentation Structure Architecture（文書構造アーキテクチャ）

## Purpose（目的）

本文書は、`noxris42` において**Documentation Structure（文書構造）** が何によって成立するのかを定義する上位Modelである。

本文書が扱う問いは次の5点である。

1. Documentation Structure（文書構造）は、何に基づいて成立するのか。
2. Documentation上の論理単位として、どのような単位が存在するのか— Documentation Framework（文書体系）／Documentation Area（文書責務領域）／Documentation Asset（文書資産）。
3. それぞれの論理単位は、何を担うのか— Framework Responsibility（体系責務）／Area Responsibility（領域責務）／Document Responsibility（文書責務）。
4. Documentation Asset（文書資産）の内部では、Document Responsibility（文書責務）がどのような最小のSemantic Structure（意味構造）へ分担され得るのか— Section／Section Responsibility（Section責務）。
5. Logical Structure（論理構造）と、Directory / File等のPhysical Structure（物理構造）、およびHeading（見出し）等のRepresentation（表現）は、どのような境界を持つのか。

本文書は上位Architectureとして自己完結する。具体的なDocumentation Framework（文書体系）の存在や内容、Directory構成、命名規則、記述形式を前提としない。

## Relationships（関係）

### Responsibility Boundary（責務境界）

本文書は、[Repository Governance](repository-governance.md)が定義するOwnership（所有責任）・Shared Scope・ Foundation Applicationを再定義・上書きしない。

したがって次は本文書の責務ではない。

- あるDocumentation Asset（文書資産）がShared Foundation Assetか、Repository-owned Assetかの判定。→ Repository Governanceの「Ownership Boundary（所有責任の境界）」による。
- Documentation Asset（文書資産）が特定Repositoryで有効になる関係。→ Repository GovernanceのFoundation Applicationによる。

本文書は、Documentationが**どのような論理単位と責務の分担として構成されるか**のみを定義する。

### Position（設計上の位置づけ）

本文書は[Repository Governance](repository-governance.md)を上位Sourceとして参照する。

同文書は「Documentation階層およびDirectory構造の正式確定」をNon-goalsとしている。本文書は、その委譲先の一つとして、**Documentation Structure（文書構造）の一般Model** を定義する。

Design Dependency（設計依存）は**Repository Governance → 本文書 →具体的なDocumentation Framework（文書体系）**の一方向とする。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Documentation Structure（文書構造）がResponsibility（責務）に基づくLogical Structure（論理構造）として成立すること
- Documentation Asset（文書資産）とDocument Responsibility（文書責務）の定義
- Definition Authority（定義権限）が成立する条件
- Documentation Area（文書責務領域）とArea Responsibility（領域責務）の定義
- Documentation Framework（文書体系）とFramework Responsibility（体系責務）の定義
- Areaへ所属するAssetについての責務粒度の関係
- Documentation Asset（文書資産）内部のSectionとSection Responsibility（Section責務）の定義
- Section Responsibility（Section責務）までを含む責務粒度の関係、およびNested Section StructureにおけるResponsibility Decomposition（責務分解）
- Logical Structure（論理構造）とPhysical Structure（物理構造）の境界
- Sectionと、Heading（見出し）・Heading Label（見出しラベル）・Markdown Heading Marker（Markdown見出し記号）等のRepresentation（表現）との境界
- Documentation Asset（文書資産）とDocument Title（文書題名）との境界

### Out of Scope（本文書が定義しない範囲）

- 具体的なDocumentation Framework（文書体系）と、それを構成するAreaの一覧
- Path、Directory名、File名、およびそれらのNaming Rule（命名規則）
- Logical Structure（論理構造）とPhysical Structure（物理構造）のMapping Rule（対応規則）
- Document Responsibility（文書責務）の分類体系
- Asset Identity／Area Identityの完全な成立条件、およびIdentity Model
- Documentation Area（文書責務領域）へ属さないDocumentation Asset（文書資産）の分類体系および成立条件
- Sectionと、Heading（見出し）・Heading Label（見出しラベル）・Markdown Heading Marker（Markdown見出し記号）との具体的なMapping Rule（対応規則）、およびHeading Level（見出しレベル）の意味対応
- `Purpose`・`Scope`等、具体的なStandard Section（標準Section）の定義
- Section Identity（Section同一性）の成立条件、およびSection Identifier等のIdentity Model
- Section ResponsibilitiesがDocument Responsibility（文書責務）を網羅することの要求
- Documentation Asset（文書資産）の記述形式・Document Title（文書題名）の構成規則
- Documentation Asset（文書資産）間のDependency（依存）・Refinement（具体化）関係の一般Model
- 複数のDocumentation Framework（文書体系）が共存する場合のComposition
- MetadataおよびDeclarationのSchema
- Documentation Lifecycle（文書の生涯管理）・Review・Validation

詳細は「Non-goals」に示す。

## Structural Basis（文書構造が成立する根拠）

Documentation Structure（文書構造）は、Directory / File等のPhysical Structure（物理構造）ではなく、**Responsibility（責務）に基づくLogical Structure（論理構造）**として成立する。

すなわち、ある論理単位の意味と責務範囲は、その単位が担うResponsibility（責務）を中心的なSemantic Basis（意味上の基礎）として成立する。Physical Structure（物理構造）上にどう現れているかによっては決まらない。

## Concept Model（概念モデル）

Documentation Structure（文書構造）は、最低限、次の3つの論理単位から成る。Documentation Asset（文書資産）の内部には、さらにSectionが成立し得る。

```text
Documentation Framework
    │
    └─ Documentation Area
            │
            └─ Area所属Documentation Asset
                    │
                    └─ Section［任意］
                            │
                            └─ Child Section［任意］
```

Documentation Asset（文書資産）は、Documentation Area（文書責務領域）へ所属しない場合も成立し得る。

上図が示すのは、**Areaへ所属するAssetとの構造関係** であり、Documentation Asset（文書資産）一般の所属Requirementを示すものではない（「Area所属を一般Requirementとしない」を参照）。

SectionおよびChild Section（子Section）は任意である。Documentation Asset（文書資産）がSectionを持つことも、SectionがChild Section（子Section）を持つことも、本文書は要求しない（「Sectionを一般Requirementとしない」を参照）。

### Documentation Asset（文書資産）

Documentation Asset（文書資産）は、一つのDocument Responsibility（文書責務）を担うDocumentation上の論理的Assetである。

Documentation Asset（文書資産）は、**Fileそのものとして定義しない** 。

```text
Documentation Asset ≠ File
```

Documentation Asset（文書資産）の意味および責務範囲を成立させる中心的なSemantic Basis（意味上の基礎）は、それが担うDocument Responsibility（文書責務）である。

Documentation Asset（文書資産）のIdentity（同一性）を、何個のFileに分割されているか、どのPathに置かれているかから導出しない。

本文書は、Asset Identityの**完全な成立条件を定義しない** 。定めるのは、Document Responsibility（文書責務）が意味上の基礎であることと、Physical Location（物理配置）からIdentity（同一性）を導出しないことである。

### Document Responsibility（文書責務）

Document Responsibility（文書責務）は、あるDocumentation Asset（文書資産）が**Documentation上で何を保持・提供する責務を担うのか**を示す責務である。

Document Responsibility（文書責務）は、Definition（定義）を保持する責務に限定されない。Documentation上で成立し得る責務には、Definition（定義）のほか、記録・説明・Navigation等も含まれ得る。

本文書は、Document Responsibility（文書責務）がどのような種類に分かれるかの分類体系を定義しない。その分類は、個々のDocumentation Framework（文書体系）が自身のFramework Responsibility（体系責務）に応じて定める。

### Definition Authority（定義権限）

Definition Authority（定義権限）は、あるConcept（概念）・Rule・Contract等について、**その内容を最終的に定義する責務を持つのはどのAssetか**を確定させるものである。

Definition Authority（定義権限）は、Documentation Asset（文書資産）一般が当然に持つものではない。

```text
Definition Authority
= Definitionを担うDocument Responsibilityの場合に成立する責務
```

すなわち、Definition Authority（定義権限）が成立するのは、そのDocumentation Asset（文書資産）のDocument Responsibility（文書責務）がDefinition（定義）を保持する責務である場合に限られる。

Definition（定義）を保持しないDocument Responsibility（文書責務）を担うAssetは、Definition Authority（定義権限）を持たない。

### Section（節）

Sectionは、Documentation Asset（文書資産）の内部でそのDocument Responsibility（文書責務）を分担するSemantic Unitである。

Sectionは、**Heading（見出し）そのものとして定義しない** 。

```text
Section ≠ Heading
Section is internal to Documentation Asset
```

Sectionは、包含するDocumentation Asset（文書資産）に従属する内部単位であり、独立したDocumentation Asset（文書資産）ではない。

Documentation Asset（文書資産）がSectionを持つことは必須ではない。Sectionを持たないDocumentation Asset（文書資産）も成立する。

Sectionの意味および責務範囲を成立させる中心的なSemantic Basis（意味上の基礎）は、それが担うSection Responsibility（Section責務）である。Heading（見出し）の有無・表記・階層から導出しない。

### Section Responsibility（Section責務）

Section Responsibility（Section責務）は、あるSectionが、そのDocumentation Asset（文書資産）のDocument Responsibility（文書責務）を果たすために、**Asset内部で何を保持・提供する責務を担うのか** を示す責務である。

Section Responsibility（Section責務）は、包含するDocumentation Asset（文書資産）のDocument Responsibility（文書責務）に従属する。

```text
Section Responsibility is bounded by Document Responsibility
```

すなわちSection Responsibility（Section責務）は、包含するDocument Responsibility（文書責務）のResponsibility Boundary（責務境界）の内部にあり、その境界を越えた独立の責務を持たない。

この関係は責務境界の内包を示すものであり、集合としての包含関係を定義するものではない。本文書は、Document Responsibility（文書責務）をSection Responsibilitiesの集合として定義しない。

Sectionを導入したことによって、新たなDefinition AuthorityModelは成立しない。Definition Authority（定義権限）は、引き続きDocumentation Asset（文書資産）とDocument Responsibility（文書責務）に基づいて成立する。

### Nested Section Structure（Section入れ子構造）

Section Responsibility（Section責務）は、必要に応じてChild Section（子Section）のSection Responsibility（Section責務）へ、さらに意味的に分解できる。

親Sectionと子Sectionの関係の意味は、**Responsibility Decomposition（責務分解）** である。

```text
Section Responsibility
    ↓ decomposed into
Section Responsibilities
```

この関係は、Refinement（具体化）・Dependency（依存）・Ordering等の別の関係ではない。

ここでのResponsibility Decomposition（責務分解）は、分解元の責務を余さず分解し尽くすことを意味しない。分解されずに、包含するDocumentation Asset（文書資産）またはParent Sectionが直接担う責務が残り得る。

本文書は、Section階層を必須としない。また、階層の深さに関する要求も設けない。

### Documentation Area（文書責務領域）

Documentation Area（文書責務領域）は、まとまった一つのArea Responsibility（領域責務）を担うDocumentation上の論理単位である。

```text
Documentation Area ≠ Documentation Assetの単なる集合
Documentation Area ≠ Directory
```

Documentation Area（文書責務領域）は、Directoryが存在することによっても、一定数のDocumentation Asset（文書資産）が存在することによっても成立しない。

Documentation Area（文書責務領域）の意味および責務範囲を成立させる中心的なSemantic Basis（意味上の基礎）は、**Area Responsibility（領域責務）** である。

Documentation Area（文書責務領域）のIdentity（同一性）を、Directoryの存在・構成から導出しない。

本文書は、Area Identityの**完全な成立条件を定義しない** 。

### Area Responsibility（領域責務）

Area Responsibility（領域責務）は、そのDocumentation Area（文書責務領域）が**どのような種類のDocument Responsibility（文書責務）を担うのか**を示す責務である。

Area Responsibility（領域責務）は、その領域に属するDocumentation Asset（文書資産）が持ち得るDocument Responsibility（文書責務）の範囲を意味的に定める。

一般Modelにおいて、Area Responsibility（領域責務）をDefinition（定義）を担う責務へ限定しない。

Document Responsibility（文書責務）がDefinition（定義）に限定されないのと同様に、Definition（定義）以外のDocument Responsibility（文書責務）を組織するDocumentation Area（文書責務領域）も成立し得る。

どの種類のDocument Responsibility（文書責務）によってAreaを分割するかは、個々のDocumentation Framework（文書体系）が自身のFramework Responsibility（体系責務）に応じて定める。

### Documentation Framework（文書体系）

Documentation Framework（文書体系）は、複数のDocumentation Area（文書責務領域）を、**一つのFramework Responsibility（体系責務）の分担** として組織する論理単位である。

```text
Documentation Framework ≠ Directory
```

Documentation Framework（文書体系）は、Areaを任意に束ねたものではない。Framework Responsibility（体系責務）が複数のArea Responsibility（領域責務）へ意味的に分解されることによって成立する。

### Framework Responsibility（体系責務）

Framework Responsibility（体系責務）は、そのDocumentation Framework（文書体系）が**Documentation全体として何を成立させるのか** を示す責務である。

## Responsibility Granularity（責務粒度）

論理単位は、責務の粒度によって関係づけられる。

この粒度関係は、**Documentation Area（文書責務領域）へ所属するDocumentation Asset（文書資産）** について次のように成立する。

```text
Framework Responsibility
    ↓ decomposed into
Area Responsibilities
    ↓ distributed into
Area所属AssetのDocument Responsibilities
    ↓ decomposed into
Section Responsibilities
    ↓ decomposed into
Child Section Responsibilities
```

この関係について、次が成立する。

- Area Responsibility（領域責務）は、Framework Responsibility（体系責務）の**意味的な分解結果** として成立する。既存Documentation Asset（文書資産）を分類した結果として成立しない。
- Areaへ所属するDocumentation Asset（文書資産）のDocument Responsibility（文書責務）は、Area Responsibility（領域責務）の**意味的な配分結果** として成立する。
- Section Responsibility（Section責務）は、Document Responsibility（文書責務）の**意味的な分解結果** として成立する。Asset内部の記述量・構成・Heading（見出し）の有無からは成立しない。
- Section Responsibility（Section責務）への分解は任意であり、かつ部分的でよい。分解された責務は分解元のResponsibility Boundary（責務境界）の内部に留まるが、分解元の責務が下位へ分配し尽くされることを意味しない（「Sectionを一般Requirementとしない」を参照）。

したがって、あるDocumentation Asset（文書資産）がどのDocumentation Area（文書責務領域）に属するかは、その配置ではなく、そのDocument Responsibility（文書責務）がどのArea Responsibility（領域責務）の配分として成立するかによって決まる。

### Do Not Make Area Membership a General Requirement（Area所属を一般Requirementとしない）

本文書は、**すべてのDocument Responsibility（文書責務）がArea Responsibility（領域責務）の配分として成立することを要求しない** 。

したがって、すべてのDocumentation Asset（文書資産）がいずれかのDocumentation Area（文書責務領域）へ所属しなければならないというRequirementは、本文書では成立しない。

特定のAreaへ属さないDocumentation Asset（文書資産）が成立し得る余地を残す。

ただし本文書は、その余地を確保するに留める。次は定義しない。

- Areaへ属さないAssetの分類体系
- そうしたAssetが成立する条件・範囲
- Areaの外側に置かれる追加のScope Concept

個々のDocumentation Framework（文書体系）が、自身のFramework Responsibility（体系責務）の範囲において、所属するAssetにArea帰属を要求することは妨げない。

### Do Not Make Section a General Requirement（Sectionを一般Requirementとしない）

Document Responsibility（文書責務）は、必要に応じて複数のSection Responsibility（Section責務）へ意味的に分解できる。ただしそれは可能性であり、要求ではない。

本文書は次を要求しない。

- すべてのDocument Responsibility（文書責務）をSection Responsibility（Section責務）へ分解すること
- すべてのDocumentation Asset（文書資産）がSectionを持つこと
- SectionがChild Section（子Section）を持つこと、および特定のSection階層を成立させること
- Section ResponsibilitiesがDocument Responsibility（文書責務）の全内容を網羅すること

とくに最後の点について、Section ResponsibilitiesによるDocument Responsibility（文書責務）のCoverage（網羅）を一般Requirementとしない。Document Responsibility（文書責務）のうち、どのSection Responsibility（Section責務）へも分解されていない部分が残ることを許容する。その部分は、包含するDocumentation Asset（文書資産）が直接担う。Parent Section ResponsibilityとChild Section Responsibilityの関係についても同様に、分解されていない部分はParent Sectionが直接担う。

本文書は、この余地を扱うためにCoverage ModelやSectionの分類体系を導入しない。

個々のDocumentation Framework（文書体系）や後続のConvention（規約）が、自身の責務範囲においてSectionの存在やCoverage（網羅）を要求することは妨げない。

### Distinction between Subject and Area（SubjectとAreaの区別）

Documentation Asset（文書資産）がどのSubjectを扱うかと、どのDocumentation Area（文書責務領域）に属するかは、別の事柄である。

Areaへの帰属を決めるのは、Subjectが何であるかではなく、**そのSubjectについてどのようなDocument Responsibility（文書責務）を担うか** である。

## Logical / Physical Boundary（論理／物理境界）

### Boundary（境界）

Documentation Structure（文書構造）はLogical Structure（論理構造）である。Directory / FileはそのPhysical Representation（物理表現）になり得るが、Logical Structure（論理構造）そのものではない。

```text
Documentation Area  ≠ Directory
Documentation Asset ≠ File
```

### Do Not Derive Identity from Physical Location（Identityを物理配置から導出しない）

論理単位のIdentity（同一性）を、Physical Location（物理配置）から導出しない。

すなわち、次の推論は成立しない。

- 「Directoryが存在するから、そこにDocumentation Area（文書責務領域）が成立する」
- 「同一Directoryにあるから、同一のAreaに属する」
- 「一つのFileであるから、一つのDocumentation Asset（文書資産）である」

### Do Not Treat Absence of Physical Representation as Absence of Logical Structure（物理表現の不在を論理構造の不在と判断しない）

逆方向の推論も成立しない。

対応するDirectory / Fileが存在しないことだけを理由に、Logical Structure（論理構造）が存在しないと判断しない。

Area Responsibility（領域責務）が成立していれば、Physical Representation（物理表現）を持たないDocumentation Area（文書責務領域）も成立し得る。

### Physical Representation Handling（物理表現の扱い）

Logical Structure（論理構造）をPhysical Structure（物理構造）へどう対応づけるかは、個々のDocumentation Framework（文書体系）が**現在採用しているPhysical Representation（物理表現）** として記録する。

具体的なPath、Directory名、File名、およびNaming Rule（命名規則）は、本文書のような一般Structure Architectureでは定義しない。

## Logical / Representation Boundary（論理／表現境界）

### Boundary with Representation（Representationとの境界）

SectionはSemantic Structure（意味構造）であり、Heading（見出し）・Heading Label（見出しラベル）・Markdown Heading Marker（Markdown見出し記号）はそのRepresentation（表現）になり得るが、Semantic Structure（意味構造）そのものではない。

```text
Section                ≠ Heading
Section Responsibility ≠ Heading Label
Heading                ≠ Markdown Heading Marker
```

すなわち本文書は、次を同一のConcept（概念）として扱わない。

- SectionとHeading（見出し）
- Section Responsibility（Section責務）とHeading Label（見出しラベル）
- Heading（見出し）とMarkdown Heading Marker（Markdown見出し記号）

### Do Not Make the Mapping a General Requirement（対応関係を一般Requirementとしない）

本文書は次のいずれも要求しない。

- すべてのSectionがHeading（見出し）で表現されること
- すべてのHeading（見出し）がSectionを表現すること

Heading（見出し）は、Sectionを表現しない目的でも用いられ得る。また、Heading（見出し）を伴わないSectionも成立し得る。

### Do Not Treat Absence of Representation as Absence of Semantic Structure（Representationの不在をSemantic Structureの不在と判断しない）

対応するHeading（見出し）が存在しないことだけを理由に、Sectionが存在しないと判断しない。

Section Responsibility（Section責務）が成立していれば、Heading（見出し）によるRepresentation（表現）を持たないSectionも成立し得る。

### Mapping Delegation（Mappingの委譲）

Sectionと、Heading（見出し）・Heading Label（見出しラベル）・Markdown Heading Marker（Markdown見出し記号）との具体的なMappingは、本文書では定義せず、後続のConvention（規約）へ委譲する。

Heading Level（見出しレベル）にSemantic Mappingを与えることも、本文書のような一般Structure Architectureでは行わない。

### Boundary with Document Title（文書題名との境界）

Document Title（文書題名）は、Documentation Asset（文書資産）について読み手が識別・理解するためのHuman-readable Representation（人間可読表現）である。Document Title（文書題名）が表すのは、そのDocumentation Asset（文書資産）が主として扱うSubject / Meaning（対象／意味）である。

Document Title（文書題名）は、次と同一のConcept（概念）ではない。

```text
Document Title ≠ Documentation Asset Identity
Document Title ≠ Document Responsibility
Document Title ≠ Area Membership
Document Title ≠ File Name / Path
```

すなわち本文書は、次を同一のConcept（概念）として扱わない。

- Document Title（文書題名）とDocumentation Asset（文書資産）のIdentity（同一性）
- Document Title（文書題名）とDocument Responsibility（文書責務）
- Document Title（文書題名）とDocumentation Area（文書責務領域）への所属
- Document Title（文書題名）とFile名・Path等のPhysical Name（物理名称）

### Do Not Derive Document Title from Identity, Document Responsibility, or Membership（文書題名を同一性・文書責務・所属から導出しない）

Document Title（文書題名）を、Documentation Asset（文書資産）のIdentity（同一性）、Document Responsibility（文書責務）、Documentation Area（文書責務領域）への所属、またはPhysical Name（物理名称）から機械的に導出しない。

あるDocumentation Asset（文書資産）がどのDocumentation Area（文書責務領域）へ属するか、どのDocument Responsibility（文書責務）を担うか、どのPhysical Location（物理配置）に置かれているかを識別する目的だけを理由として、Document Title（文書題名）へそれらを再提示することを、本文書は要求しない。

逆方向の推論も成立しない。ある語がDocument Title（文書題名）に現れないことだけを理由に、そのDocumentation Asset（文書資産）が特定のDocumentation Area（文書責務領域）へ属さない、または特定のDocument Responsibility（文書責務）を担わないとは判断しない。

### Document Title Composition Delegation（文書題名構成の委譲）

Document Title（文書題名）の具体的なComposition Rule（構成規則）は、本文書では定義せず、後続のConvention（規約）へ委譲する。

固定のTitle Schema、 Title Component（題名構成要素）の集合、およびそれらの表記順序は、本文書のような一般Structure Architectureでは定義しない。

## Design Principles（設計原則）

### Responsibility as Semantic Basis（責務を意味上の基礎とする）

Documentation上の論理単位の意味および責務範囲は、Physical Structure（物理構造）ではなくResponsibility（責務）を中心的なSemantic Basis（意味上の基礎）として成立する。

### Logical Identity is Independent of Physical Location（同一性は物理配置から独立する）

論理単位のIdentity（同一性）を、Path・Directory・Fileの構成から導出しない。物理表現の有無は、論理構造の成立条件ではない。

### Decomposition over Classification（分類ではなく分解で構成する）

Area Responsibility（領域責務）は、Framework Responsibility（体系責務）の意味的な分解として定める。既存文書を後から分類した結果として定めない。

### Area is Not a Container（Areaは入れ物ではない）

Documentation Area（文書責務領域）はDocumentation Asset（文書資産）の集合ではない。Asset数やDirectoryの存在は、Areaの成立条件ではない。

### No Structural Role beyond Document Responsibility（責務を超えた構造的役割を設けない）

Documentation Asset（文書資産）に対して、Document Responsibility（文書責務）とは別のStructural Roleを導入しない。Area全体に関わる責務が必要な場合も、通常のDocument Responsibility（文書責務）として表現する。

### No Logical Concept for Physical Pattern（物理パターンのために論理概念を作らない）

Directory名と同名のFile、 `overview/overview.md` のような配置上のPatternを説明するために、特別なLogical Conceptを導入しない。

### Semantic Structure over Representation（表現ではなく意味構造で構成する）

Asset内部の構造は、Section Responsibility（Section責務）によるSemantic Structure（意味構造）として成立する。Heading（見出し）・Label・Markdown記法はその表現であり、意味の成立条件ではない。

### Minimal Model First（最小Modelから始める）

現時点で必要性が確認されていない上位Concept（概念）を先行導入しない。必要性が具体的に確認された時点で追加設計する。

## Non-goals（現在扱わない事項）

本文書は次を定義しない。ここで示す事項はDesign Gapではない。本文書の現在の責務に基づいて、意図的に定義・解決・導入の対象外としている事項であり、必要なものは後続設計へ委譲する。

### Concepts Not Introduced（導入しないConcept）

- **Representative Document**

  AreaそのものをSubjectとし、Area-wide Common Foundationを保持するAssetを、特別なConcept（概念）として導入しない。

  Area全体に関わる責務が必要な場合であっても、通常のDocumentation Asset（文書資産）とDocument Responsibility（文書責務）で表現できる。Area名と同名のFileや、Directory名を反復するPhysical Patternを説明するための論理概念は設けない。

- **Navigation Document**

  Navigationを担う文書を、本Modelの必須Concept（概念）として導入しない。

  Navigationは補助的責務であり、必要性が確認された時点でDocument Responsibility（文書責務）の一種として設計できる。現在のModelが成立するために必須の上位Concept（概念）ではない。

### Identity（同一性に関する事項）

- Asset Identityの完全な成立条件
- Area Identityの完全な成立条件
- Section Identity（Section同一性）。本文書はSection Identity（Section同一性）をArchitecture Conceptとして導入しない。Section Identifier・ Section Registry・ Stable Reference（安定参照）等も設計しない。現時点では、SectionとSection Responsibility（Section責務）で足りる。
- Subject／Responsibility（責務）／Identifier（識別子）等の組合せによるIdentity Model

本文書が定めるのは、Responsibility（責務）が意味上の基礎であることと、Physical Location（物理配置）からIdentity（同一性）を導出しないことに限られる。

### Structure / Naming（構造・命名に関する事項）

- 具体的なDocumentation Framework（文書体系）とAreaの一覧
- Path、Directory名、File名、およびNaming Rule（命名規則）
- Logical Structure（論理構造）とPhysical Structure（物理構造）のMapping Rule（対応規則）をどのConvention（規約）が所有するか

### Section（節に関する事項）

- **具体的なStandard Section（標準Section）**

  `Purpose`・`Scope`・`Relationships` 等、具体的なSectionを本文書では定義しない。

  それらは、Architecture Area（アーキテクチャ領域）が所有するSemantic / Structural Modelではない。複数のDocumentation Asset（文書資産）へ反復適用される定義はReusable Normative Standard（再利用可能な規範標準）であり、Conventions Area（規約領域）のArea Responsibility（領域責務）に属する。

  本文書は一般Section Modelのみを定義する。後続のConvention（規約）は、このModelを前提として具体的なStandard Section（標準Section）を定義できる。

  本文書は、その責務を担う具体的なDocumentation Asset（文書資産）を特定せず、その存在を前提にもしない。

- **Heading（見出し）へのMapping Rule（対応規則）**

  SectionとHeading（見出し）・Heading Label（見出しラベル）・Markdown Heading Marker（Markdown見出し記号）との対応規則、およびHeading Level（見出しレベル）のSemantic Mapping。

- **Section OrderingとCoverage（網羅）の要求**

  Sectionの出現順序、必須Sectionの集合、Section ResponsibilitiesによるDocument Responsibility（文書責務）のCoverage（網羅）要求。

### Composition（体系間構成に関する事項）

- 複数のDocumentation Framework（文書体系）の共存Model
- Framework（体系）間のPriority／Refinement（具体化）／Dependency（依存）

### Authoring / Declaration（記述・宣言に関する事項）

- Documentation Asset（文書資産）の記述形式
- Document Title（文書題名）の構成規則、固定のTitle Schema、およびTitle Component（題名構成要素）の集合
- MetadataおよびDeclarationのSchema

## Usage by Downstream Design（下位設計からの参照）

具体的なDocumentation Framework（文書体系）は、本文書を参照して次を前提にできる。これらを再定義する必要はない。

1. Documentation Structure（文書構造）がResponsibility（責務）に基づいて成立すること。
2. Documentation Framework（文書体系）・Documentation Area（文書責務領域）・Documentation Asset（文書資産）の意味と、それぞれの責務。
3. Definition Authority（定義権限）が、Definition（定義）を担うDocument Responsibility（文書責務）の場合に成立すること。
4. Areaへ所属するAssetについての、Framework Responsibility（体系責務）からDocument Responsibility（文書責務）までの粒度関係。
5. SectionがDocumentation Asset（文書資産）内部のSemantic Unitであり、Section Responsibility（Section責務）がDocument Responsibility（文書責務）に従属すること。
6. Document Responsibility（文書責務）からSection Responsibility（Section責務）、さらにChild Section（子Section）への任意のResponsibility Decomposition（責務分解）。
7. Logical Structure（論理構造）とPhysical Structure（物理構造）の境界、およびSectionとHeading（見出し）等Representation（表現）の境界。

Conventions Area（規約領域）に属する後続のConvention（規約）は、上記のSection Modelを前提として、具体的なStandard Section（標準Section）やHeading（見出し）へのMapping Rule（対応規則）を定めることができる。その際、Section・Section Responsibility（Section責務）・Responsibility Decomposition（責務分解）・Representation（表現）との境界を再定義する必要はない。

本文書からは判断できないのは、**どのようなAreaで構成されるDocumentation Framework（文書体系）を成立させるか** であり、これは個々のFramework Architectureの責務に属する。

`noxris42` が現在採用する具体的なFramework（体系）は、[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)が定義する。
