# Documentation Structure Architecture（文書構造のArchitecture）

## Purpose（目的）

本文書は、`noxris42` において
**Documentation Structure（文書構造）** が何によって成立するのかを定義する
上位Modelである。

本文書が扱う問いは次の5点である。

1. Documentation Structure（文書構造）は、何に基づいて成立するのか。
2. Documentation上の論理単位として、どのような単位が存在するのか
   （Documentation Framework／Documentation Area／Documentation Asset）。
3. それぞれの論理単位は、何を担うのか
   （Framework Responsibility／Area Responsibility／
   Document Responsibility）。
4. Documentation Asset（文書資産）の内部では、
   Document Responsibility（文書責務）がどのような
   最小のSemantic Structure（意味構造）へ分担され得るのか
   （Section／Section Responsibility）。
5. Logical Structure（論理構造）と、Directory / File等の
   Physical Structure（物理構造）、および
   Heading（見出し）等のRepresentation（表現）は、
   どのような境界を持つのか。

本文書は上位Architectureとして自己完結する。
具体的なDocumentation Framework（文書体系）の存在や内容、
Directory構成、命名規則、記述形式を前提としない。

## Position（上位Architectureとの関係）

本文書は
[Repository Governance Architecture](repository-governance.md)
（Repository間の統治・責務Architecture）を
上位Source（上位の情報源）として参照する。

同Architectureは
「Documentation階層およびDirectory構造の正式確定」を
Non-goals / Delegation（後続へ委譲する事項）としている。
本文書は、その委譲先の一つとして、
**Documentation Structure（文書構造）の一般Model** を定義する。

Design Dependency（設計依存）は
**Repository Governance Architecture → 本文書 →
具体的なDocumentation Framework（文書体系）**
の一方向とする。

本文書は、同Architectureが定義する
Ownership（所有責任）・Shared Scope（共有範囲）・
Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）を
再定義・上書きしない。

したがって次は本文書の責務ではない。

- あるDocumentation Asset（文書資産）が
  Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）か、
  Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）か
  の判定。
  → Repository Governance Architectureの
  「Ownership Boundary（所有責任の境界）」による。
- Documentation Asset（文書資産）が特定Repositoryで有効になる関係。
  → Repository Governance Architectureの
  Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）による。

本文書は、Documentationが
**どのような論理単位と責務の分担として構成されるか**
のみを定義する。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Documentation Structure（文書構造）が
  Responsibility（責務）に基づく
  Logical Structure（論理構造）として成立すること
- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）の定義
- Definition Authority（定義権限）が成立する条件
- Documentation Area（文書責務領域）と
  Area Responsibility（領域責務）の定義
- Documentation Framework（文書体系）と
  Framework Responsibility（体系責務）の定義
- Area（領域）へ所属するAsset（資産）についての責務粒度の関係
- Documentation Asset（文書資産）内部の
  Section（節）とSection Responsibility（Section責務）の定義
- Section Responsibility（Section責務）までを含む責務粒度の関係、
  およびNested Section Structure（Section入れ子構造）における
  Responsibility Decomposition（責務分解）
- Logical Structure（論理構造）と
  Physical Structure（物理構造）の境界
- Section（節）と、Heading（見出し）・Heading Label（見出しラベル）・
  Markdown Heading Marker（Markdown見出し記号）等の
  Representation（表現）との境界

### Out of Scope（本文書が定義しない範囲）

- 具体的なDocumentation Framework（文書体系）と、
  それを構成するArea（領域）の一覧
- Path、Directory名、File名、およびそれらのNaming Rule（命名規則）
- Logical Structure（論理構造）と
  Physical Structure（物理構造）のMapping Rule（対応規則）
- Document Responsibility（文書責務）の分類体系
- Asset Identity（資産同一性）／Area Identity（領域同一性）の
  完全な成立条件、およびIdentity Model（同一性モデル）
- Documentation Area（文書責務領域）へ属さない
  Documentation Asset（文書資産）の分類体系および成立条件
- Section（節）と、Heading（見出し）・Heading Label（見出しラベル）・
  Markdown Heading Marker（Markdown見出し記号）との
  具体的なMapping Rule（対応規則）、
  およびHeading Level（見出しレベル）の意味対応
- `Purpose`・`Scope`等、具体的なStandard Section（標準Section）の定義
- Section Identity（Section同一性）の成立条件、
  およびSection Identifier（Section識別子）等のIdentity Model（同一性モデル）
- Section Responsibilities（Section責務群）が
  Document Responsibility（文書責務）を網羅することの要求
- Documentation Asset（文書資産）の記述形式・
  Document Title（文書題名）の構成規則
- Documentation Asset（文書資産）間の
  Dependency（依存）・Refinement（具体化）関係の一般Model
- 複数のDocumentation Framework（文書体系）が
  共存する場合のComposition（体系間構成）
- Metadata（構造化メタデータ）およびDeclaration（明示的宣言）のSchema
- Documentation Lifecycle（文書の生涯管理）・Review・Validation

詳細は「Non-goals / Delegation（今回扱わず後続へ委譲する事項）」に示す。

## Structural Basis（文書構造が成立する根拠）

Documentation Structure（文書構造）は、
Directory / File等のPhysical Structure（物理構造）ではなく、
**Responsibility（責務）に基づくLogical Structure（論理構造）**
として成立する。

すなわち、ある論理単位の意味と責務範囲は、
その単位が担うResponsibility（責務）を中心的な
Semantic Basis（意味上の基礎）として成立する。
Physical Structure（物理構造）上にどう現れているかによっては決まらない。

## Concept Model（概念モデル）

Documentation Structure（文書構造）は、最低限、次の3つの論理単位から成る。
Documentation Asset（文書資産）の内部には、
さらにSection（節）が成立し得る。

```text
Documentation Framework（文書体系）
    │
    └─ Documentation Area（文書責務領域）
            │
            └─ Area所属Documentation Asset（文書資産）
                    │
                    └─ Section（節）［任意］
                            │
                            └─ Child Section（子Section）［任意］
```

Documentation Asset（文書資産）は、
Documentation Area（文書責務領域）へ所属しない場合も成立し得る。

上図が示すのは、
**Area（領域）へ所属するAsset（資産）との構造関係** であり、
Documentation Asset（文書資産）一般の
所属Requirement（所属要求）を示すものではない
（「Area所属を一般Requirementとしない」を参照）。

Section（節）およびChild Section（子Section）は任意である。
Documentation Asset（文書資産）がSection（節）を持つことも、
Section（節）がChild Section（子Section）を持つことも、
本文書は要求しない
（「Section（節）を一般Requirementとしない」を参照）。

### Documentation Asset（文書資産）

Documentation Asset（文書資産）は、
一つのDocument Responsibility（文書責務）を担う
Documentation上の論理的Asset（資産）である。

Documentation Asset（文書資産）は、
**File（ファイル）そのものとして定義しない** 。

```text
Documentation Asset ≠ File
```

Documentation Asset（文書資産）の意味および責務範囲を成立させる
中心的なSemantic Basis（意味上の基礎）は、
それが担うDocument Responsibility（文書責務）である。

Documentation Asset（文書資産）のIdentity（同一性）を、
何個のFileに分割されているか、
どのPathに置かれているかから導出しない。

本文書は、Asset Identity（資産同一性）の
**完全な成立条件を定義しない** 。
定めるのは、
Document Responsibility（文書責務）が意味上の基礎であることと、
Physical Location（物理配置）から
Identity（同一性）を導出しないことである。

### Document Responsibility（文書責務）

Document Responsibility（文書責務）は、
あるDocumentation Asset（文書資産）が
**Documentation上で何を保持・提供する責務を担うのか**
を示す責務である。

Document Responsibility（文書責務）は、
Definition（定義）を保持する責務に限定されない。
Documentation上で成立し得る責務には、
Definition（定義）のほか、
記録・説明・Navigation（案内）等も含まれ得る。

本文書は、Document Responsibility（文書責務）が
どのような種類に分かれるかの分類体系を定義しない。
その分類は、個々のDocumentation Framework（文書体系）が
自身のFramework Responsibility（体系責務）に応じて定める。

### Definition Authority（定義権限）

Definition Authority（定義権限）は、
あるConcept（概念）・Rule（規則）・Contract（契約）等について、
**その内容を最終的に定義する責務を持つのはどのAssetか**
を確定させるものである。

Definition Authority（定義権限）は、
Documentation Asset（文書資産）一般が当然に持つものではない。

```text
Definition Authority
= Definition（定義）を担うDocument Responsibilityの場合に成立する責務
```

すなわち、Definition Authority（定義権限）が成立するのは、
そのDocumentation Asset（文書資産）の
Document Responsibility（文書責務）が
Definition（定義）を保持する責務である場合に限られる。

Definition（定義）を保持しない
Document Responsibility（文書責務）を担うAsset（資産）は、
Definition Authority（定義権限）を持たない。

### Section（節）

Section（節）は、
Documentation Asset（文書資産）の内部で
そのDocument Responsibility（文書責務）を分担する
Semantic Unit（意味単位）である。

Section（節）は、
**Heading（見出し）そのものとして定義しない** 。

```text
Section ≠ Heading
Section is internal to Documentation Asset（Asset内部に従属する）
```

Section（節）は、包含するDocumentation Asset（文書資産）に従属する
内部単位であり、独立したDocumentation Asset（文書資産）ではない。

Documentation Asset（文書資産）がSection（節）を持つことは必須ではない。
Section（節）を持たないDocumentation Asset（文書資産）も成立する。

Section（節）の意味および責務範囲を成立させる
中心的なSemantic Basis（意味上の基礎）は、
それが担うSection Responsibility（Section責務）である。
Heading（見出し）の有無・表記・階層から導出しない。

### Section Responsibility（Section責務）

Section Responsibility（Section責務）は、
あるSection（節）が、
そのDocumentation Asset（文書資産）の
Document Responsibility（文書責務）を果たすために、
**Asset内部で何を保持・提供する責務を担うのか** を示す責務である。

Section Responsibility（Section責務）は、
包含するDocumentation Asset（文書資産）の
Document Responsibility（文書責務）に従属する。

```text
Section Responsibility is bounded by Document Responsibility
（Section責務は文書責務のResponsibility Boundary内部にある）
```

すなわちSection Responsibility（Section責務）は、
包含するDocument Responsibility（文書責務）の
Responsibility Boundary（責務境界）の内部にあり、
その境界を越えた独立の責務を持たない。

この関係は責務境界の内包を示すものであり、
集合としての包含関係（Subset）を定義するものではない。
本文書は、Document Responsibility（文書責務）を
Section Responsibilities（Section責務群）の集合として定義しない。

Section（節）を導入したことによって、
新たなDefinition Authority（定義権限）Modelは成立しない。
Definition Authority（定義権限）は、
引き続きDocumentation Asset（文書資産）と
Document Responsibility（文書責務）に基づいて成立する。

### Nested Section Structure（Section入れ子構造）

Section Responsibility（Section責務）は、必要に応じて
Child Section（子Section）の
Section Responsibility（Section責務）へ、さらに意味的に分解できる。

親Section（節）と子Section（節）の関係の意味は、
**Responsibility Decomposition（責務分解）** である。

```text
Section Responsibility（親）
    ↓ decomposed into（意味的に分解される）
Section Responsibilities（子）
```

この関係は、
Refinement（具体化）・Dependency（依存）・Ordering（順序）等の
別の関係ではない。

ここでのResponsibility Decomposition（責務分解）は、
分解元の責務を余さず分解し尽くすことを意味しない。
分解されずに、
包含するDocumentation Asset（文書資産）または
Parent Section（親Section）が直接担う責務が残り得る。

本文書は、Section階層（Section Hierarchy）を必須としない。
また、階層の深さに関する要求も設けない。

### Documentation Area（文書責務領域）

Documentation Area（文書責務領域）は、
まとまった一つのArea Responsibility（領域責務）を担う
Documentation上の論理単位である。

```text
Documentation Area ≠ Documentation Assetの単なる集合
Documentation Area ≠ Directory
```

Documentation Area（文書責務領域）は、
Directoryが存在することによっても、
一定数のDocumentation Asset（文書資産）が存在することによっても成立しない。

Documentation Area（文書責務領域）の意味および責務範囲を成立させる
中心的なSemantic Basis（意味上の基礎）は、
**Area Responsibility（領域責務）** である。

Documentation Area（文書責務領域）のIdentity（同一性）を、
Directoryの存在・構成から導出しない。

本文書は、Area Identity（領域同一性）の
**完全な成立条件を定義しない** 。

### Area Responsibility（領域責務）

Area Responsibility（領域責務）は、
そのDocumentation Area（文書責務領域）が
**どのような種類のDocument Responsibility（文書責務）を担うのか**
を示す責務である。

Area Responsibility（領域責務）は、
その領域に属するDocumentation Asset（文書資産）が持ち得る
Document Responsibility（文書責務）の範囲を意味的に定める。

一般Modelにおいて、
Area Responsibility（領域責務）を
Definition（定義）を担う責務へ限定しない。

Document Responsibility（文書責務）が
Definition（定義）に限定されないのと同様に、
Definition（定義）以外の
Document Responsibility（文書責務）を組織する
Documentation Area（文書責務領域）も成立し得る。

どの種類のDocument Responsibility（文書責務）によって
Area（領域）を分割するかは、
個々のDocumentation Framework（文書体系）が
自身のFramework Responsibility（体系責務）に応じて定める。

### Documentation Framework（文書体系）

Documentation Framework（文書体系）は、
複数のDocumentation Area（文書責務領域）を、
**一つのFramework Responsibility（体系責務）の分担** として
組織する論理単位である。

```text
Documentation Framework ≠ Directory
```

Documentation Framework（文書体系）は、
Area（領域）を任意に束ねたものではない。
Framework Responsibility（体系責務）が
複数のArea Responsibility（領域責務）へ意味的に分解されることによって成立する。

### Framework Responsibility（体系責務）

Framework Responsibility（体系責務）は、
そのDocumentation Framework（文書体系）が
**Documentation全体として何を成立させるのか** を示す責務である。

## Responsibility Granularity（責務粒度）

論理単位は、責務の粒度によって関係づけられる。

この粒度関係は、
**Documentation Area（文書責務領域）へ所属する
Documentation Asset（文書資産）** について次のように成立する。

```text
Framework Responsibility（体系責務）
    ↓ decomposed into（意味的に分解される）
Area Responsibilities（領域責務）
    ↓ distributed into（意味的に配分される）
Area所属AssetのDocument Responsibilities（文書責務）
    ↓ decomposed into（意味的に分解される・任意／部分的でよい）
Section Responsibilities（Section責務）
    ↓ decomposed into（意味的に分解される・任意／部分的でよい）
Child Section Responsibilities（子Section責務）
```

この関係について、次が成立する。

- Area Responsibility（領域責務）は、
  Framework Responsibility（体系責務）の
  **意味的な分解結果** として成立する。
  既存Documentation Asset（文書資産）を分類した結果として成立しない。
- Area（領域）へ所属するDocumentation Asset（文書資産）の
  Document Responsibility（文書責務）は、
  Area Responsibility（領域責務）の
  **意味的な配分結果** として成立する。
- Section Responsibility（Section責務）は、
  Document Responsibility（文書責務）の
  **意味的な分解結果** として成立する。
  Asset内部の記述量・構成・Heading（見出し）の有無からは成立しない。
- Section Responsibility（Section責務）への分解は任意であり、
  かつ部分的でよい。
  分解された責務は分解元の
  Responsibility Boundary（責務境界）の内部に留まるが、
  分解元の責務が下位へ分配し尽くされることを意味しない
  （「Section（節）を一般Requirementとしない」を参照）。

したがって、あるDocumentation Asset（文書資産）が
どのDocumentation Area（文書責務領域）に属するかは、
その配置ではなく、
そのDocument Responsibility（文書責務）が
どのArea Responsibility（領域責務）の配分として成立するかによって決まる。

### Area所属を一般Requirementとしない

本文書は、
**すべてのDocument Responsibility（文書責務）が
Area Responsibility（領域責務）の配分として成立することを要求しない** 。

したがって、
すべてのDocumentation Asset（文書資産）が
いずれかのDocumentation Area（文書責務領域）へ
所属しなければならないというRequirement（要求）は、
本文書では成立しない。

特定のArea（領域）へ属さない
Documentation Asset（文書資産）が成立し得る余地を残す。

ただし本文書は、その余地を確保するに留める。
次は定義しない。

- Area（領域）へ属さないAsset（資産）の分類体系
- そうしたAsset（資産）が成立する条件・範囲
- Area（領域）の外側に置かれる追加のScope Concept（範囲概念）

個々のDocumentation Framework（文書体系）が、
自身のFramework Responsibility（体系責務）の範囲において、
所属するAsset（資産）にArea（領域）帰属を要求することは妨げない。

### Section（節）を一般Requirementとしない

Document Responsibility（文書責務）は、必要に応じて複数の
Section Responsibility（Section責務）へ意味的に分解できる。
ただしそれは可能性であり、要求ではない。

本文書は次を要求しない。

- すべてのDocument Responsibility（文書責務）を
  Section Responsibility（Section責務）へ分解すること
- すべてのDocumentation Asset（文書資産）が
  Section（節）を持つこと
- Section（節）がChild Section（子Section）を持つこと、
  および特定のSection階層を成立させること
- Section Responsibilities（Section責務群）が
  Document Responsibility（文書責務）の全内容を網羅すること

とくに最後の点について、
Section Responsibilities（Section責務群）による
Document Responsibility（文書責務）の
Coverage（網羅）を一般Requirement（一般要求）としない。
Document Responsibility（文書責務）のうち、
どのSection Responsibility（Section責務）へも
分解されていない部分が残ることを許容する。
その部分は、包含するDocumentation Asset（文書資産）が直接担う。
Parent Section Responsibility（親Section責務）と
Child Section Responsibility（子Section責務）の関係についても同様に、
分解されていない部分はParent Section（親Section）が直接担う。

本文書は、この余地を扱うために
Coverage Model（網羅モデル）やSection（節）の分類体系を導入しない。

個々のDocumentation Framework（文書体系）や
後続のConvention（規約）が、
自身の責務範囲においてSection（節）の存在や
Coverage（網羅）を要求することは妨げない。

### Subject（対象）とArea（領域）の区別

Documentation Asset（文書資産）が
どのSubject（対象）を扱うかと、
どのDocumentation Area（文書責務領域）に属するかは、別の事柄である。

Area（領域）への帰属を決めるのは、
Subject（対象）が何であるかではなく、
**そのSubjectについてどのような
Document Responsibility（文書責務）を担うか** である。

## Logical / Physical Boundary（論理／物理境界）

### 境界

Documentation Structure（文書構造）は
Logical Structure（論理構造）である。
Directory / Fileはその
Physical Representation（物理表現）になり得るが、
Logical Structure（論理構造）そのものではない。

```text
Documentation Area  ≠ Directory
Documentation Asset ≠ File
```

### Identity（同一性）を物理配置から導出しない

論理単位のIdentity（同一性）を、
Physical Location（物理配置）から導出しない。

すなわち、次の推論は成立しない。

- 「Directoryが存在するから、
  そこにDocumentation Area（文書責務領域）が成立する」
- 「同一Directoryにあるから、同一のArea（領域）に属する」
- 「一つのFileであるから、一つのDocumentation Asset（文書資産）である」

### 物理表現の不在を論理構造の不在と判断しない

逆方向の推論も成立しない。

対応するDirectory / Fileが存在しないことだけを理由に、
Logical Structure（論理構造）が存在しないと判断しない。

Area Responsibility（領域責務）が成立していれば、
Physical Representation（物理表現）を持たない
Documentation Area（文書責務領域）も成立し得る。

### Physical Representationの扱い

Logical Structure（論理構造）を
Physical Structure（物理構造）へどう対応づけるかは、
個々のDocumentation Framework（文書体系）が
**現在採用しているPhysical Representation（物理表現）** として記録する。

具体的なPath、Directory名、File名、
およびNaming Rule（命名規則）は、
本文書のような一般Structure Architectureでは定義しない。

## Logical / Representation Boundary（論理／表現境界）

### Representationとの境界

Section（節）はSemantic Structure（意味構造）であり、
Heading（見出し）・Heading Label（見出しラベル）・
Markdown Heading Marker（Markdown見出し記号）は
そのRepresentation（表現）になり得るが、
Semantic Structure（意味構造）そのものではない。

```text
Section                ≠ Heading
Section Responsibility ≠ Heading Label
Heading                ≠ Markdown Heading Marker
```

すなわち本文書は、次を同一のConcept（概念）として扱わない。

- Section（節）とHeading（見出し）
- Section Responsibility（Section責務）と
  Heading Label（見出しラベル）
- Heading（見出し）と
  Markdown Heading Marker（Markdown見出し記号）

### 対応関係を一般Requirementとしない

本文書は次のいずれも要求しない。

- すべてのSection（節）がHeading（見出し）で表現されること
- すべてのHeading（見出し）がSection（節）を表現すること

Heading（見出し）は、Section（節）を表現しない目的でも用いられ得る。
また、Heading（見出し）を伴わないSection（節）も成立し得る。

### Representationの不在をSemantic Structureの不在と判断しない

対応するHeading（見出し）が存在しないことだけを理由に、
Section（節）が存在しないと判断しない。

Section Responsibility（Section責務）が成立していれば、
Heading（見出し）によるRepresentation（表現）を持たない
Section（節）も成立し得る。

### Mappingの委譲

Section（節）と、Heading（見出し）・Heading Label（見出しラベル）・
Markdown Heading Marker（Markdown見出し記号）との
具体的なMapping（対応）は、
本文書では定義せず、後続のConvention（規約）へ委譲する。

Heading Level（見出しレベル）に
Semantic Mapping（意味対応）を与えることも、
本文書のような一般Structure Architectureでは行わない。

## Design Principles（設計原則）

### 1. Responsibility as Semantic Basis（責務を意味上の基礎とする）

Documentation上の論理単位の意味および責務範囲は、
Physical Structure（物理構造）ではなく
Responsibility（責務）を中心的な
Semantic Basis（意味上の基礎）として成立する。

### 2. Logical Identity is Independent of Physical Location（同一性は物理配置から独立する）

論理単位のIdentity（同一性）を、
Path・Directory・Fileの構成から導出しない。
物理表現の有無は、論理構造の成立条件ではない。

### 3. Decomposition over Classification（分類ではなく分解で構成する）

Area Responsibility（領域責務）は、
Framework Responsibility（体系責務）の意味的な分解として定める。
既存文書を後から分類した結果として定めない。

### 4. Area is Not a Container（Areaは入れ物ではない）

Documentation Area（文書責務領域）は
Documentation Asset（文書資産）の集合ではない。
Asset数やDirectoryの存在は、Areaの成立条件ではない。

### 5. No Structural Role beyond Document Responsibility（責務を超えた構造的役割を設けない）

Documentation Asset（文書資産）に対して、
Document Responsibility（文書責務）とは別の
Structural Role（構造上の役割）を導入しない。
Area全体に関わる責務が必要な場合も、
通常のDocument Responsibility（文書責務）として表現する。

### 6. No Logical Concept for Physical Pattern（物理パターンのために論理概念を作らない）

Directory名と同名のFile、
`overview/overview.md` のような配置上のPatternを説明するために、
特別なLogical Concept（論理概念）を導入しない。

### 7. Semantic Structure over Representation（表現ではなく意味構造で構成する）

Asset内部の構造は、Section Responsibility（Section責務）による
Semantic Structure（意味構造）として成立する。
Heading（見出し）・Label（ラベル）・Markdown記法は
その表現であり、意味の成立条件ではない。

### 8. Minimal Model First（最小Modelから始める）

現時点で必要性が確認されていない上位Conceptを先行導入しない。
必要性が具体的に確認された時点で追加設計する。

## Non-goals / Delegation（今回扱わず後続へ委譲する事項）

本文書は次を定義しない。

### 導入しないConcept（概念）

- **Representative Document（代表文書）**

  Area（領域）そのものをSubject（対象）とし、
  Area-wide Common Foundation（領域共通基盤）を保持するAssetを、
  特別なConcept（概念）として導入しない。

  Area全体に関わる責務が必要な場合であっても、
  通常のDocumentation Asset（文書資産）と
  Document Responsibility（文書責務）で表現できる。
  Area名と同名のFileや、
  Directory名を反復するPhysical Pattern（物理パターン）を
  説明するための論理概念は設けない。

- **Navigation Document（案内文書）**

  Navigation（案内）を担う文書を、
  本Modelの必須Concept（概念）として導入しない。

  Navigation（案内）は補助的責務であり、
  必要性が確認された時点で
  Document Responsibility（文書責務）の一種として設計できる。
  現在のModelが成立するために必須の上位Conceptではない。

### Identity（同一性）に関する事項

- Asset Identity（資産同一性）の完全な成立条件
- Area Identity（領域同一性）の完全な成立条件
- Section Identity（Section同一性）。
  本文書はSection Identity（Section同一性）を
  Architecture Concept（アーキテクチャ概念）として導入しない。
  Section Identifier（Section識別子）・
  Section Registry（Section登録簿）・
  Stable Reference（安定参照）等も設計しない。
  現時点では、Section（節）と
  Section Responsibility（Section責務）で足りる。
- Subject（対象）／Responsibility（責務）／Identifier（識別子）等の
  組合せによるIdentity Model（同一性モデル）

本文書が定めるのは、
Responsibility（責務）が意味上の基礎であることと、
Physical Location（物理配置）から
Identity（同一性）を導出しないことに限られる。

### 構造・命名に関する事項

- 具体的なDocumentation Framework（文書体系）とArea（領域）の一覧
- Path、Directory名、File名、およびNaming Rule（命名規則）
- Logical Structure（論理構造）と
  Physical Structure（物理構造）のMapping Rule（対応規則）を
  どのConvention（規約）が所有するか

### Section（節）に関する事項

- **具体的なStandard Section（標準Section）**

  `Purpose`・`Scope`・`Relationships` 等、
  具体的なSection（節）を本文書では定義しない。

  それらは、Architecture Area（アーキテクチャ領域）が所有する
  Semantic / Structural Model（意味・構造モデル）ではない。
  複数のDocumentation Asset（文書資産）へ反復適用される定義は
  Reusable Normative Standard（再利用可能な規範標準）であり、
  Conventions Area（規約領域）のArea Responsibility（領域責務）に属する。

  本文書は一般Section Model（一般Sectionモデル）のみを定義する。
  後続のConvention（規約）は、
  このModelを前提として具体的なStandard Section（標準Section）を
  定義できる。

  本文書は、その責務を担う具体的な
  Documentation Asset（文書資産）を特定せず、
  その存在を前提にもしない。

- **Heading（見出し）へのMapping Rule（対応規則）**

  Section（節）とHeading（見出し）・
  Heading Label（見出しラベル）・
  Markdown Heading Marker（Markdown見出し記号）との対応規則、
  およびHeading Level（見出しレベル）の
  Semantic Mapping（意味対応）。

- **Section Ordering（Section順序）とCoverage（網羅）の要求**

  Section（節）の出現順序、必須Section（節）の集合、
  Section Responsibilities（Section責務群）による
  Document Responsibility（文書責務）のCoverage（網羅）要求。

### Composition（体系間構成）に関する事項

- 複数のDocumentation Framework（文書体系）の共存Model
- Framework間のPriority（優先）／Refinement（具体化）／Dependency（依存）

### 記述・宣言に関する事項

- Documentation Asset（文書資産）の記述形式
- Metadata（構造化メタデータ）およびDeclaration（明示的宣言）のSchema

これらはDesign Gap（設計不足）ではなく、
現時点で確定していない事項を先行決定しないための意図的な委譲である。

## Usage by Downstream Design（下位設計からの参照）

具体的なDocumentation Framework（文書体系）は、
本文書を参照して次を前提にできる。
これらを再定義する必要はない。

1. Documentation Structure（文書構造）が
   Responsibility（責務）に基づいて成立すること。
2. Documentation Framework（文書体系）・
   Documentation Area（文書責務領域）・
   Documentation Asset（文書資産）の意味と、それぞれの責務。
3. Definition Authority（定義権限）が、
   Definition（定義）を担う
   Document Responsibility（文書責務）の場合に成立すること。
4. Area（領域）へ所属するAsset（資産）についての、
   Framework Responsibility（体系責務）から
   Document Responsibility（文書責務）までの粒度関係。
5. Section（節）が
   Documentation Asset（文書資産）内部の
   Semantic Unit（意味単位）であり、
   Section Responsibility（Section責務）が
   Document Responsibility（文書責務）に従属すること。
6. Document Responsibility（文書責務）から
   Section Responsibility（Section責務）、
   さらにChild Section（子Section）への
   任意のResponsibility Decomposition（責務分解）。
7. Logical Structure（論理構造）と
   Physical Structure（物理構造）の境界、
   およびSection（節）とHeading（見出し）等
   Representation（表現）の境界。

Conventions Area（規約領域）に属する後続のConvention（規約）は、
上記のSection Model（Sectionモデル）を前提として、
具体的なStandard Section（標準Section）や
Heading（見出し）へのMapping Rule（対応規則）を定めることができる。
その際、Section（節）・Section Responsibility（Section責務）・
Responsibility Decomposition（責務分解）・
Representation（表現）との境界を再定義する必要はない。

本文書からは判断できないのは、
**どのようなArea（領域）で構成される
Documentation Framework（文書体系）を成立させるか** であり、
これは個々のFramework Architecture（体系アーキテクチャ）の責務に属する。

`noxris42` が現在採用する具体的なFramework（体系）は、
[Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)
が定義する。
