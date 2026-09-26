# Foundation Application State Specification（基盤適用状態仕様）

## Purpose（目的）

本文書は、`noxris42` において**Foundation Application（共通開発基盤資産の適用関係）の状態を、Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）がどのDeclarationとして保持し、そこからEffective Foundation State（有効基盤状態）がどのように一意・決定論的に導出されるのかというConcrete Contract（具体契約）を定義する**Specification Asset（仕様資産）である。

本文書が扱う問いは次の6点である。

1. Foundation Applicationに関するDecision Authority（判断権限）は、Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）の間で、どのDeclarationへ配分されるのか。
2. Repository-levelのFoundation Application State（基盤適用状態）は、どの値を取り、どのように解決されるのか。
3. Repository-levelで適用されたConvention（規約）のRuleが特定Targetへ適用されるか否かは、どのように宣言・解決されるのか。
4. Effective Foundation State（有効基盤状態）は、どのAuthoritative Input（正式入力）から、どのように決定論的に導出されるのか。
5. これらのDeclarationは、どのConcrete Representation（具体表現）・Field・Allowed Value・Validation Conditionとして成立するのか。
6. Foundation Application State（基盤適用状態）と、AI Integration（AI連携）およびFoundation ProviderのLocationとの境界はどこにあるのか。

本文書が定義するのは、この6点に対するConcrete Contract（具体契約）に限られる。本文書は、Foundation ApplicationのSemantic / Structural Model（意味／構造モデル）を定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するSpecifications Area（仕様領域）に属する通常のDocumentation Asset（文書資産）である。Foundation Applicationという特定Subjectについて、その状態を宣言・解決・検証可能にするConcrete Contract（具体契約）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

Foundation Application State（基盤適用状態）のConcrete Contract（具体契約）、すなわちそのDeclarationのConcrete Representation（具体表現）、Effective Foundation State（有効基盤状態）の導出方式、およびValidation ConditionについてのDefinition Authority（定義権限）は本文書が持つ。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は上位設計にある。本文書はこれらを参照するのみで、再定義・上書きしない。

- Shared Development Foundation、Shared Foundation Asset、Repository-owned Asset、Ownership（所有責任）、Foundation Application、およびFoundation Applicationの判断主体が適用先Repositoryであること
- Ownership（所有責任）とFoundation Applicationの分離、およびApplication Mechanism（適用方式）を上位で固定しないこと
- Target-specific Applicability（対象固有適用範囲）の意味、その判断主体、Foundation Applicationとの境界、およびRule自身が定めるApplicabilityとの境界
- `.github` のSelf Application
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）
- Effective Foundation State（有効基盤状態）の意味、すなわちFoundation Applicationの結果として成立し、解決済みのFoundation ApplicationとTarget-specific Applicability（対象固有適用範囲）を含み得ること、およびAI Integration（AI連携）にとって外部から与えられる入力であること
- Effective Foundation State Access（有効基盤状態参照）、Task Relevance（タスク関連性）、およびDefinition Authority（定義権限）・Foundation Application・Task Relevance（タスク関連性）の分離
- Convention（規約）、Normative Rule（規範的規則）、Rule Identity（規則同一性）
- Rule ID（規則ID）の形式

したがって次は本文書の責務ではない。

- Foundation Applicationの意味、およびその判断主体の所在。→ [Repository Governance](../architecture/repository-governance.md)による。
- Target-specific Applicability（対象固有適用範囲）の意味、およびFoundation Application・Rule自身が定めるApplicabilityとの境界。→ [Repository Governance](../architecture/repository-governance.md)による。
- Effective Foundation State（有効基盤状態）のArchitecture上の意味、およびそれがTarget-specific Applicability（対象固有適用範囲）を含み得ること。→ [AI Integration Architecture](../architecture/ai-integration.md)による。
- あるAssetがShared Foundation Assetとして成立するか否かの判定。→ [Repository Governance](../architecture/repository-governance.md)の「Ownership Boundary（所有責任の境界）」による。
- Convention（規約）およびNormative Rule（規範的規則）の意味、ならびにRule Identity（規則同一性）の成立。→ [Convention Architecture](../architecture/convention.md)による。
- Rule ID（規則ID）の具体形式。→ [Convention Authoring Convention](../conventions/convention-authoring.md)による。
- 各Normative Rule（規範的規則）が自身の内容として定めるApplicability。→ 当該Normative Rule（規範的規則）を定義するConvention Asset（規約資産）による。
- AI Integration（AI連携）がEffective Foundation State（有効基盤状態）を参照・利用する責務。→ [AI Integration Architecture](../architecture/ai-integration.md)による。

本文書が定めるのは、これらによってすでに成立しているModelを前提として、Foundation Applicationの状態をどのDeclarationとして保持し、どのように解決するかである。すなわち本文書が所有するのは、Shared Application Default（共有適用既定）のDeclaration、Consumer Declaration（利用側宣言）、Resolution Algorithm（解決手順）、Target Scope（対象範囲）、Composition（合成）、YAML Representation（YAML表現）、Field Contract（Field契約）、およびValidation Condition（検証条件）というConcrete Contract（具体契約）に限られる。

### Position（設計上の位置づけ）

本文書は[Repository Governance](../architecture/repository-governance.md)を上位Sourceとして参照する。

同文書は、Foundation Applicationの判断主体を適用先Repositoryと定め、Foundation ApplicationとTarget-specific Applicability（対象固有適用範囲）の意味と境界を定める一方、Target-specific Applicability（対象固有適用範囲）におけるTargetの指定方式・合成方式、Application State（適用状態）の機械可読な表現形式、MetadataおよびDeclarationの具体Schemaを意図的に定義せず、後続設計へ委譲している。また同文書は、必要な具体状態を後続設計においてMetadataやDeclarationとして明示的に表現できることを許容している。本文書は、その委譲先として、Foundation Application State（基盤適用状態）のConcrete Contract（具体契約）を定義する。

Design Dependency（設計依存）は次の一方向とする。

```text
Repository Governance
        ▲
        │ refines
Foundation Application State Specification
```

[AI Integration Architecture](../architecture/ai-integration.md)は、Foundation Application State Designを、AI Integration（AI連携）の下位設計ではなく、AI Integration（AI連携）がその結果であるEffective Foundation State（有効基盤状態）を消費する隣接Subjectとして扱う。本文書はAI Integration Architecture（AI連携アーキテクチャ）をRefinement（具体化）しない。同文書が定義するEffective Foundation State（有効基盤状態）の意味を前提として、その生成方式とConcrete Representation（具体表現）を本文書が定める。

本文書は、Convention（規約）およびNormative Rule（規範的規則）を[Convention Architecture](../architecture/convention.md)が定める意味で参照する。Convention Architecture（規約アーキテクチャ）をRefinement（具体化）しない。

本文書は、上位Architecture（アーキテクチャ）の意味を変更・補完しない。本文書が定めるConcrete Contract（具体契約）から、上位のConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）を導出・上書きしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）の間における、Foundation Application State（基盤適用状態）に関するDecision Authority（判断権限）の配分
- Shared Application Default（共有適用既定）
- Consumer Repository（利用Repository）のApplication Decision（適用判断）
- Repository-level Foundation Application State（Repositoryレベル基盤適用状態）と、そのApplication State（適用状態）の値
- Target-specific Applicability（対象固有適用範囲）のDeclarationと解決
- Target Scope（対象範囲）
- Hierarchical Resolution（階層的解決）
- Convention-level Composition（規約単位の合成）におけるIndependent / RefineのComposition Semantics（合成意味）
- Effective Foundation State（有効基盤状態）の決定論的導出
- Provider Declaration（提供側宣言）およびConsumer Declaration（利用側宣言）のConcrete Representation（具体表現）
- 各Declarationの最小Field、Allowed Value、およびValidation Condition
- AI Integration（AI連携）との境界
- Foundation ProviderのLocationとの境界
- `.github` のSelf Applicationにおける本Contract（契約）の適用

### Out of Scope（本文書が定義しない範囲）

- Foundation Applicationの意味、およびその判断主体の所在
- Target-specific Applicability（対象固有適用範囲）の意味、およびFoundation Application・Rule自身が定めるApplicabilityとの境界
- Effective Foundation State（有効基盤状態）のArchitecture上の意味
- 個々のShared Foundation Assetを適用するか否かの判断そのもの、および判断基準
- Shared Foundation AssetのAsset Type（資産種別）、およびその確定
- Application Mechanism（適用方式）、およびAsset Type（資産種別）ごとの適用手順
- Convention（規約）およびNormative Rule（規範的規則）の内容、ならびに各Normative Rule（規範的規則）が自身の内容として定めるApplicability
- `.foundation/application-defaults.yaml` および `.foundation/application.yaml` の実体、およびCurrent State（現在状態）の投入
- Effective Foundation State（有効基盤状態）のMaterialization / Cache（実体化／キャッシュ）の設計
- Stable Asset ID体系
- Schema Version
- Selection / Pattern / Mandatory / Optional等、`applied` / `not-applied` 以外のApplication State（適用状態）Model
- Exception / Waiver（例外／免除）
- Generic Glob / Regex / Extension Pattern、およびDeclaration間のPriority
- Foundation Provider（基盤提供主体）のLocationの値、その決定方式、およびRemote Locationとしての解決方式
- AI Integration（AI連携）によるEffective Foundation State（有効基盤状態）の参照方式、およびTask Relevance Resolution（タスク関連性解決）
- 本Contract（契約）に対するValidation Tool、Enforcement、およびCI要求

## Authority Allocation（権限の配分）

[Repository Governance](../architecture/repository-governance.md)が定めるとおり、Foundation ApplicationおよびTarget-specific Applicability（対象固有適用範囲）の判断主体は適用先Repository、すなわちConsumer Repository（利用Repository）である。本文書はこれを前提として、Declaration内容の所有主体を次のとおり配分する。Foundation Provider（基盤提供主体）は、Consumer Repository（利用Repository）がBaseline（基準状態）として採用できるShared Application Default（共有適用既定）を定義できる。

本文書が扱う各Declaration内容の所有主体は次である。

| Declaration内容 | 何を確定させるか | 所有主体 |
| --- | --- | --- |
| Shared Application Default（共有適用既定） | 各Shared Foundation AssetのDefault State（既定状態） | Foundation Provider（基盤提供主体） |
| Repository-specific Application Decision（Repository固有適用判断） | 当該RepositoryにおけるShared Foundation AssetごとのShared Defaultとの差分 | Consumer Repository（利用Repository） |
| Target-specific Applicability（対象固有適用範囲） | Repository-levelで適用されたConvention（規約）のRuleが、特定TargetへApplicableか否か | Consumer Repository（利用Repository） |

Shared Application Default（共有適用既定）は、Consumer Repository（利用Repository）のFoundation Applicationを決定しない。Consumer Repository（利用Repository）がBaseline（基準状態）として採用した場合に、差分が宣言されていないShared Foundation AssetのApplication State（適用状態）を与える。

```text
Shared Application Default
= Consumer RepositoryがBaselineとして採用する既定

Shared Application Default
≠ Consumer RepositoryのFoundation Applicationの決定
```

AI Integration（AI連携）およびAI Consumer（AI利用主体）は、いずれの内容の所有主体でもない。

## Repository-level Foundation Application（Repositoryレベルの基盤適用）

### Application State（適用状態）

Repository-level Foundation Application State（Repositoryレベル基盤適用状態）は、Shared Foundation Assetごとに、そのAssetが当該Repositoryで有効か否かを示す状態である。

Application State（適用状態）が取る値は次の2つに限られる。

| 値 | 意味 |
| --- | --- |
| `applied` | 当該Shared Foundation Assetは、当該Repositoryで有効である |
| `not-applied` | 当該Shared Foundation Assetは、当該Repositoryで有効ではない |

Selection・Pattern・Mandatory・Optional等、これ以外の状態Modelを本文書は導入しない。

### Shared Application Default（共有適用既定）

Shared Application Default（共有適用既定）は、Foundation Provider（基盤提供主体）が定義する、Shared Foundation AssetごとのDefault State（既定状態）である。Default State（既定状態）の値はApplication State（適用状態）の値である。

Provider Declaration（提供側宣言）は、Foundation Provider（基盤提供主体）が提供するすべてのShared Foundation Assetについて、Default State（既定状態）を網羅して保持する。

### Consumer Repository Application Decision（利用Repositoryの適用判断）

Consumer Repository（利用Repository）は、Shared Application Default（共有適用既定）をBaseline（基準状態）として採用し、Repository-specificに必要な差分のみを保持する。

Consumer Declaration（利用側宣言）が保持するのは次の3つに限られる。

1. Shared Application Default（共有適用既定）のBaseline Adoption（基準採用）
2. Repository-level Application Difference（Repositoryレベル適用差分）
3. Target-specific Applicability（対象固有適用範囲）

Repository-level Application Difference（Repositoryレベル適用差分）は、Shared Foundation Assetについて、Shared Application Default（共有適用既定）と異なるApplication State（適用状態）を当該Repositoryが判断した場合にのみ保持する。Shared Application Default（共有適用既定）と同じApplication State（適用状態）を重ねて保持しない。

あるShared Foundation AssetについてのRepository-specific Application Decision（Repository固有適用判断）が、Consumer Repository（利用Repository）が所有する別のAuthoritative Declaration（正式宣言）からすでに一意に成立している場合、Consumer Declaration（利用側宣言）はそれを重複宣言しない。その場合、当該Authoritative Declaration（正式宣言）が、そのShared Foundation AssetについてのRepository-specific Application Decision（Repository固有適用判断）を与える。

別のAuthoritative Declaration（正式宣言）をRepository-specific Application Decision（Repository固有適用判断）のInputとして扱えるのは、そのDeclarationを所有する既存のDefinition Authority（定義権限）側で、当該DeclarationがRepository-specific Application Decision（Repository固有適用判断）を成立させるSourceであることが明示的に定義されている場合に限られる。

- File・Declarationの存在、内容、名称、およびPhysical Location（物理配置）から、それがRepository-specific Application Decision（Repository固有適用判断）のSourceであることを推論しない。
- そのようなSourceを探索・判定するGeneric Discovery Mechanismを本文書は導入しない。
- 該当する別のAuthoritative Declaration（正式宣言）がRepositoryに存在しないことは、本Contract（契約）のDesign Gap（設計上の不足）ではない。その場合、Repository-specific Application Decision（Repository固有適用判断）はConsumer Declaration（利用側宣言）の `applications` のみから得られる。

### Repository-level Resolution（Repositoryレベルの解決）

あるShared Foundation AssetのResolved Repository-level Application State（解決済みRepositoryレベル適用状態）は、次によって一意に定まる。

1. 当該Shared Foundation AssetについてRepository-specific Application Decision（Repository固有適用判断）が成立している場合、そのApplication State（適用状態）
2. 成立していない場合、当該Shared Foundation AssetのShared Application Default（共有適用既定）

```text
Resolved Repository-level Application State
= Repository-specific Application Decision（成立している場合）
= Shared Application Default（それ以外）
```

Repository-specific Application Decision（Repository固有適用判断）が優先されるのは、[Repository Governance](../architecture/repository-governance.md)がFoundation Applicationの判断主体を適用先Repositoryと定めているためである。本文書が新たなPriorityを導入するものではない。

## Target-specific Applicability（対象固有適用範囲）

### Upper Model Handling（上位Modelの扱い）

Target-specific Applicability（対象固有適用範囲）の意味、Foundation Applicationとの境界、およびRule自身が定めるApplicabilityとの境界は[Repository Governance](../architecture/repository-governance.md)が定める。本文書はこれらを再定義せず、それを前提として、Target Declaration（対象宣言）とその解決をConcrete Contract（具体契約）として具体化する。

上位Modelが定める境界は、本Contract（契約）において次のとおり具体化される。

- Target Declaration（対象宣言）は、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `applied` であるConvention（規約）についてのみ置ける。`not-applied` であるConvention（規約）へのTarget Declaration（対象宣言）は、「Validation Conditions（検証条件）」により無効である。
- Target Declaration（対象宣言）の解決は、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）を変更しない。
- Target Declaration（対象宣言）の解決結果は、Rule自身が定めるApplicabilityによってさらに限定される。

Exception / Waiver（例外／免除）は本Contract（契約）に含めない。

### Rule-defined Applicability（Rule自身が定めるApplicability）

本文書では、Normative Rule（規範的規則）が自身の内容として定めるApplicabilityを、説明上Rule-defined Applicabilityと表記する。これは本文書内のLocal Term（局所用語）であり、独立した上位Concept（概念）を成立させない。その内容のDefinition Authority（定義権限）は、当該Normative Rule（規範的規則）を定義するConvention Asset（規約資産）にある。

本Contract（契約）において、あるLocationであるRuleがApplicableであることは次によって判定される。

```text
あるLocationであるRuleがApplicableである
= Target Declarationの解決結果に含まれる
  かつ
  そのLocationがRule-defined Applicabilityの範囲内である
```

Target Declaration（対象宣言）の解決結果、すなわち本文書におけるResolved Applicability（解決済み適用範囲）は、Consumer Repository（利用Repository）側で選択されたRule Set（規則集合）であり、LocationにおけるRuleの最終的なApplicabilityそのものではない。本文書における「Repository側でApplicable対象とする」「Applicable対象へ加える」等の表現は、このRepository側のRule Selection（規則選択）を指す。

`include` / `add` 等によってRuleをRule Set（規則集合）へ含めることは、Rule-defined Applicabilityを拡張・上書きしない。Rule-defined Applicabilityの範囲外にあるLocationでは、Resolved Applicability（解決済み適用範囲）に含まれるRuleであってもApplicableではない。

### Target Scope（対象範囲）

Target Declaration（対象宣言）が扱うTarget Scope（対象範囲）は次の2つに限られる。

| Target Scope | `scope` の値 | 包含するTarget |
| --- | --- | --- |
| Directory Subtree | `subtree` | `path` が示すDirectory自身と、その配下のすべてのDirectoryおよびFile |
| Exact File | `file` | `path` が示すFileのみ |

Repository全体に対する状態は、Repository-level Foundation Application State（Repositoryレベル基盤適用状態）が担う。Target Declaration（対象宣言）は、Repository rootをTargetとしない。

Generic Glob・Regex・Extension Pattern等のTarget Matching機構を本文書は導入しない。`path` は文字どおりのPathとして扱い、Patternとして解釈しない。

### Hierarchical Resolution（階層的解決）

Target-specific Applicability（対象固有適用範囲）は、Target Inclusion（対象包含）のみから決定論的に解決する。

あるRepository内Location `L` について、Convention（規約） `C` のResolved Applicability（解決済み適用範囲）を解決する場合、次のDeclaration Chain（宣言連鎖）を用いる。

```text
Repository
→ Directory Subtree
→ deeper Directory Subtree
→ Exact File
```

1. Repository：Repository-levelで `applied` である `C` について、`C` が定めるすべてのRuleを、Repository側でApplicable対象とする。
2. Directory Subtree：`L` を包含するDirectory Subtreeのうち、`C` についてのDeclarationを持つものを、浅いものから深いものへ順に用いる。
3. Exact File：`L` が `path` と一致するExact Fileであり、`C` についてのDeclarationを持つ場合、それを最後に用いる。

`L` を包含する複数のDirectory Subtreeは、互いに祖先・子孫の関係にあるため、深さによる順序は一意に定まる。

Declaration Chain（宣言連鎖）の各段は、直前の段で解決済みのApplicabilityをParent Resolved Applicability（親解決済み適用範囲）として受け取る。ある段に `C` のDeclarationがない場合、その段はParent Resolved Applicability（親解決済み適用範囲）をそのまま継承する。

Consumer Declaration（利用側宣言）上の記述順は、Resolution Priority（解決優先度）として扱わない。

### Convention-level Composition（規約単位の合成）

Composition Behavior（合成挙動）は、TargetごとにConvention（規約）単位で `mode` として指定する。

| `mode` | Composition Behavior | Parent Resolved Applicability |
| --- | --- | --- |
| `independent` | Independent（独立） | 継承しない |
| `refine` | Refine（具体化） | Inputとする |

#### Independent（独立）

Independent（独立）は、Parent Resolved Applicability（親解決済み適用範囲）を継承せず、当該TargetにおけるRule Set（規則集合）を完全に定義する。

Independent（独立）は、`include` と `exclude` のいずれか一方のみを持つ。

| Field | Resolved Applicability（解決済み適用範囲） |
| --- | --- |
| `include` | 列挙したRuleのみを、Repository側でApplicable対象とする |
| `exclude` | `C` が定めるすべてのRuleから、列挙したRuleを除いたものを、Repository側でApplicable対象とする |

#### Refine（具体化）

Refine（具体化）は、Parent Resolved Applicability（親解決済み適用範囲）をInputとし、差分を与える。

| Field | 差分 |
| --- | --- |
| `add` | 列挙したRuleを、Repository側でApplicable対象へ加える |
| `remove` | 列挙したRuleを、Repository側でApplicable対象から除く |

同一のRuleを `add` と `remove` の双方へ指定しない。したがって、`add` と `remove` の適用順序は結果に影響しない。

#### Resolution Formula（解決式）

`All(C)` を `C` が定めるすべてのRuleの集合（各RuleのRule-defined Applicabilityによる限定を含まない）、`P` をParent Resolved Applicability（親解決済み適用範囲）とするとき、各段のResolved Applicability（解決済み適用範囲） `R` は次である。

```text
Repository段:            R = All(C)
Declarationなし:         R = P
independent + include:   R = include
independent + exclude:   R = All(C) − exclude
refine:                  R = (P ∪ add) − remove
```

`refine` において `add` または `remove` を持たない場合、その値は空集合として扱う。双方を持たない `refine` の結果は `R = P` である。

Location `L` において `C` のRule `r` がApplicableであるのは、`r` がDeclaration Chain（宣言連鎖）の最終段の `R` に含まれ、かつ `L` が `r` のRule-defined Applicabilityの範囲内にある場合である。

#### Resolution Example（解決の例示）

次は解決の成立を示すための例示である。Current State（現在状態）の宣言ではなく、いかなるRepositoryのApplication Decision（適用判断）も表さない。

```text
前提:
  C = docs/conventions/writing.md（Repository-levelで applied）
  All(C) = { WRT-SF-001, …, WRT-SF-009 }

Declaration:
  docs/specifications（subtree）       independent include [WRT-SF-001, WRT-SF-003]
  docs/specifications/example.md（file） refine add [WRT-SF-007] remove [WRT-SF-003]

L = docs/specifications/example.md の解決:
  Repository               R = { WRT-SF-001, …, WRT-SF-009 }
  docs/specifications      R = { WRT-SF-001, WRT-SF-003 }
  example.md               R = { WRT-SF-001, WRT-SF-007 }

L = docs/specifications/other.md の解決:
  Repository               R = { WRT-SF-001, …, WRT-SF-009 }
  docs/specifications      R = { WRT-SF-001, WRT-SF-003 }
  （Exact File Declarationなし） R = { WRT-SF-001, WRT-SF-003 }
```

いずれの場合も、各Ruleが実際にApplicableであるかは、さらにRule-defined Applicabilityによって限定される。

## Effective Foundation State（有効基盤状態）

### Composition（構成）

[AI Integration Architecture](../architecture/ai-integration.md)は、Effective Foundation State（有効基盤状態）が解決済みのFoundation ApplicationとTarget-specific Applicability（対象固有適用範囲）を含み得ることを定める。本文書はその意味を前提として、本Contract（契約）から導出されるEffective Foundation State（有効基盤状態）の具体的な構成を次とする。

```text
Effective Foundation State
= Resolved Repository-level Foundation Application
+ Resolved Target-specific Applicability
```

- Resolved Repository-level Foundation Application（解決済みRepositoryレベル基盤適用）：すべてのShared Foundation Assetについての、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）
- Resolved Target-specific Applicability（解決済み対象固有適用範囲）：Repository-levelで `applied` である各Convention（規約）についての、Repository内の各LocationにおけるResolved Applicability（解決済み適用範囲）

### Deterministic Derivation（決定論的導出）

Effective Foundation State（有効基盤状態）は、次のAuthoritative Input（正式入力）のみから導出する。

- Provider Declaration（提供側宣言）
- Consumer Declaration（利用側宣言）
- Consumer Repository（利用Repository）が所有し、「Consumer Repository Application Decision（利用Repositoryの適用判断）」が定める条件を満たしてRepository-specific Application Decision（Repository固有適用判断）を一意に成立させている他のAuthoritative Declaration（正式宣言）
- Target-specific Applicability（対象固有適用範囲）の解決に用いる各Convention（規約）のRule Set（規則集合）

同じAuthoritative Input（正式入力）からは、同じEffective Foundation State（有効基盤状態）が一意・決定論的に導出されなければならない。本文書が定める解決は、Declaration上の記述順、Declarationの読込順、およびResolutionを行う主体に依存しない。

### Materialization / Cache（実体化／キャッシュ）

Effective Foundation State（有効基盤状態）を将来Materialization / Cache（実体化／キャッシュ）として保持する場合、それは本文書が定める解決済み状態のDerived Representation（派生表現）である。

Materialization / Cache（実体化／キャッシュ）はDefinition Authority（定義権限）を持たない。その内容とAuthoritative Input（正式入力）から導出される結果とが一致しない場合、成立している内容はAuthoritative Input（正式入力）側である。

Materialization / Cache（実体化／キャッシュ）そのものの設計は、本文書の対象外である。

## Concrete Representation（具体表現）

### Physical Location（物理配置）

Foundation Application State（基盤適用状態）のDeclarationは、次のPhysical Location（物理配置）に置く。

```text
Repository root
└─ .foundation/
     ├─ application-defaults.yaml
     └─ application.yaml
```

| File | 保持するDeclaration | 所有主体 |
| --- | --- | --- |
| `application-defaults.yaml` | Provider Declaration（提供側宣言）：Shared Application Default（共有適用既定） | Foundation Provider（基盤提供主体） |
| `application.yaml` | Consumer Declaration（利用側宣言）：当該RepositoryのFoundation Application State（基盤適用状態） | Consumer Repository（利用Repository） |

`.foundation/` は、Foundation Applicationに関するConcrete Declaration（具体宣言）を収めるPhysical Container（物理的入れ物）である。本文書は `.foundation/` に対して、Documentation Area（文書責務領域）、Architecture上のResponsibility（責務）・Area、その他のSemantic Responsibility（意味上の責務）を成立させない。

`application-defaults.yaml` はFoundation Provider（基盤提供主体）に置く。`application.yaml` は各Consumer Repository（利用Repository）に置く。

File Formatは、いずれもYAMLとする。

### Reference Form（参照の形式）

Declarationは、Shared Foundation Asset・Convention（規約）・Ruleを次によって参照する。

| 参照 | 形式 |
| --- | --- |
| Asset Reference（資産参照） | 当該Shared Foundation Assetの、Foundation Provider（基盤提供主体）のRepository rootを基準とするRelative Path（相対Path） |
| Convention Reference（規約参照） | Asset Reference（資産参照）と同じ形式による、当該Convention Asset（規約資産）の参照 |
| Rule Reference（規則参照） | 既存のRule ID（規則ID）。例：`WRT-SF-001` |

Asset Reference（資産参照）およびConvention Reference（規約参照）は、現時点では、Provider内部のSource LocationをLocatorとして用いる。Source LocationはAsset Identity（資産同一性）ではない。

```text
Source Location
≠ Asset Identity
```

本文書はStable Asset ID体系を導入しない。

### Provider Declaration（提供側宣言）

`application-defaults.yaml` の意味構造は次である。

```yaml
defaults:
  <asset-reference>: applied | not-applied
```

### Consumer Declaration（利用側宣言）

`application.yaml` の意味構造は次である。

```yaml
baseline: shared-default

applications:
  <asset-reference>: applied | not-applied

targets:
  - path: <repository-relative-path>
    scope: subtree | file
    conventions:
      <convention-reference>:
        mode: independent | refine
        ...
```

`mode: independent` のConvention（規約）Declarationは、次のいずれか一方の形を取る。

```yaml
mode: independent
include:
  - <rule-id>
```

```yaml
mode: independent
exclude:
  - <rule-id>
```

`mode: refine` のConvention（規約）Declarationは、次の形を取る。

```yaml
mode: refine
add:
  - <rule-id>
remove:
  - <rule-id>
```

上記は、Semantic Contract（意味契約）を示す最小形である。本文書は、Current Need（現在の必要性）から導けないFieldを導入しない。

### Field Contract（Field契約）

| Declaration | Field | 必須性 | Allowed Value | 意味 |
| --- | --- | --- | --- | --- |
| Provider Declaration（提供側宣言） | `defaults` | 必須 | Asset Reference（資産参照）からApplication State（適用状態）へのMapping | Shared Application Default（共有適用既定） |
| Consumer Declaration（利用側宣言） | `baseline` | 必須 | `shared-default` | Shared Application Default（共有適用既定）のBaseline Adoption（基準採用） |
| Consumer Declaration（利用側宣言） | `applications` | 差分がある場合のみ | Asset Reference（資産参照）からApplication State（適用状態）へのMapping | Repository-level Application Difference（Repositoryレベル適用差分） |
| Consumer Declaration（利用側宣言） | `targets` | Target Declaration（対象宣言）がある場合のみ | Target Declaration（対象宣言）のList | Target-specific Applicability（対象固有適用範囲） |
| Target Declaration（対象宣言） | `path` | 必須 | Repository rootを基準とするRelative Path（相対Path） | Targetの所在 |
| Target Declaration（対象宣言） | `scope` | 必須 | `subtree` / `file` | Target Scope（対象範囲） |
| Target Declaration（対象宣言） | `conventions` | 必須 | Convention Reference（規約参照）からConvention Declaration（規約宣言）へのMapping | 当該TargetにおけるConvention（規約）ごとのComposition（合成） |
| Convention Declaration（規約宣言） | `mode` | 必須 | `independent` / `refine` | Composition Behavior（合成挙動） |
| Convention Declaration（規約宣言） | `include` | `independent` で `exclude` を持たない場合に必須 | Rule ID（規則ID）のList | 列挙したRuleのみをApplicable対象とする |
| Convention Declaration（規約宣言） | `exclude` | `independent` で `include` を持たない場合に必須 | Rule ID（規則ID）のList | 列挙したRuleを除くRuleをApplicable対象とする |
| Convention Declaration（規約宣言） | `add` | `refine` で任意 | Rule ID（規則ID）のList | Parent Resolved Applicability（親解決済み適用範囲）へ加えるRule |
| Convention Declaration（規約宣言） | `remove` | `refine` で任意 | Rule ID（規則ID）のList | Parent Resolved Applicability（親解決済み適用範囲）から除くRule |

### Validation Conditions（検証条件）

Declarationは、次のすべてを満たす場合に有効である。

Provider Declaration（提供側宣言）：

- `defaults` を持つ。
- `defaults` は、Foundation Provider（基盤提供主体）が提供するすべてのShared Foundation Assetを、Asset Reference（資産参照）として網羅する。
- `defaults` の各値は、`applied` または `not-applied` である。

Consumer Declaration（利用側宣言）：

- `baseline` を持ち、その値は `shared-default` である。
- `baseline`・`applications`・`targets` 以外のTop-level Fieldを持たない。
- `applications` の各Keyは、Provider Declaration（提供側宣言）の `defaults` に存在するAsset Reference（資産参照）である。
- `applications` の各値は、`applied` または `not-applied` であり、当該Shared Foundation AssetのShared Application Default（共有適用既定）と異なる。
- `applications` は、他のAuthoritative Declaration（正式宣言）からRepository-specific Application Decision（Repository固有適用判断）が一意に成立しているShared Foundation Assetを含まない。

Target Declaration（対象宣言）：

- `path` は、Repository rootを基準とし、`/` を区切りとするRelative Path（相対Path）である。先頭の `/` または `./`、末尾の `/`、および `.` / `..` のPath Segmentを含まない。
- `path` はRepository rootを示さない。
- `scope: subtree` の `path` はDirectoryを示し、`scope: file` の `path` はFileを示す。
- `conventions` の各Keyは、Provider Declaration（提供側宣言）の `defaults` に存在するConvention Reference（規約参照）であり、そのResolved Repository-level Application State（解決済みRepositoryレベル適用状態）は `applied` である。
- 同一の `path` と `scope` の組に対して、同一のConvention（規約）のDeclarationは1つに限られる。

Convention Declaration（規約宣言）：

- `mode` は `independent` または `refine` である。
- `mode: independent` は、`include` と `exclude` のいずれか一方のみを持ち、`add` および `remove` を持たない。
- `mode: refine` は、`include` および `exclude` を持たない。`add` と `remove` はいずれも任意である。
- 列挙する各Rule ID（規則ID）は、当該Convention Reference（規約参照）が示すConvention Asset（規約資産）が定めるRuleのRule ID（規則ID）である。
- 同一のList内で、同一のRule ID（規則ID）を重複させない。
- 同一のRule ID（規則ID）を `add` と `remove` の双方へ指定しない。

YAML上の同一Mapping内で、同一のKeyを重複させない。

`path` の形式に関する条件は、同一Targetが複数の表現で宣言されることを防ぎ、Declaration Chain（宣言連鎖）の照合を決定論的にするためのConcrete Contract（具体契約）である。Consumer Declaration（利用側宣言）のTop-level Fieldに関する条件は、本Contract（契約）が解釈しないFieldを黙って受理しないためのConcrete Contract（具体契約）であり、将来の拡張機構を先行して定めるものではない。

## Boundaries（境界）

### Boundary with AI Integration（AI連携との境界）

[AI Integration Architecture](../architecture/ai-integration.md)が定めるとおり、AI Integration（AI連携）は、Foundation ApplicationおよびTarget-specific Applicability（対象固有適用範囲）を決定・変更・上書きしない。AI Integration（AI連携）が扱うのは、本文書が定める解決によって成立したEffective Foundation State（有効基盤状態）の参照である。

```text
Foundation Application State
  determines
Effective Foundation State

AI Integration
  accesses
Effective Foundation State
```

`.foundation/application-defaults.yaml` および `.foundation/application.yaml` は、AI Integration Resource（AI連携資源）ではない。これらは、AI Integration（AI連携）の有無にかかわらず成立するFoundation Application State（基盤適用状態）のDeclarationである。

`.ai/foundation-resolution.md` は、[AI Context Resolution Specification](ai-context-resolution.md)が定めるResolution Information（解決情報）である。Foundation Application State（基盤適用状態）ではなく、その代替でもない。本文書は、同Specification（仕様）が定める次の境界を変更しない。

```text
listed in foundation-resolution.md
≠ applied to Consumer Repository

Definition Authority
≠ Foundation Application
≠ Task Relevance
```

Task Relevance（タスク関連性）は、Effective Foundation State（有効基盤状態）を変更しない。あるRuleがCurrent Task（現在タスク）にRelevantでないことは、そのRuleがApplicableでないことを意味しない。

### Boundary with Foundation Provider Location（基盤提供主体のLocationとの境界）

Declarationが保持するAsset Reference（資産参照）およびConvention Reference（規約参照）は、Foundation Provider（基盤提供主体）内部のSource Locationである。

Declarationは、Consumer Repository（利用Repository）の環境上でFoundation Provider（基盤提供主体）がどこに存在するか、すなわちFoundation ProviderのLocationを保持しない。Foundation ProviderのLocationとProvider内部のSource Locationの区別と合成は[AI Context Resolution Specification](ai-context-resolution.md)による。本文書はこれを再定義しない。

## Self Application（`.github`自身への適用）

`.github` も、本文書が定めるContract（契約）に従う。`.github` のためのModel上の例外を設けない。

`.github` は次の2つのRoleについて、それぞれ別のDeclarationを持つ。

| Role | Declaration |
| --- | --- |
| Foundation Provider（基盤提供主体） | `.github/.foundation/application-defaults.yaml` |
| Consumer Repository（利用Repository） | `.github/.foundation/application.yaml` |

`.github` のShared Application Default（共有適用既定）を、`.github` 自身のFoundation Application State（基盤適用状態）と同一視しない。`.github` 自身のFoundation Application State（基盤適用状態）は、他のConsumer Repository（利用Repository）と同じく、Shared Application Default（共有適用既定）のBaseline Adoption（基準採用）とRepository-specificな差分から解決する。

`.github` がConsumer Repository（利用Repository）である場合、Foundation Provider（基盤提供主体）は当該Repository自身であり、Asset Reference（資産参照）およびConvention Reference（規約参照）はRepository root相対Pathとしてそのまま解決される。

## Deferred to Downstream Design（後続設計へ委譲する事項）

本文書は次を定義しない。ここで示す事項は、本文書の現在の責務に基づいて、意図的に定義・解決の対象外としている事項である。

- `.foundation/application-defaults.yaml` および `.foundation/application.yaml` の実体作成と、Shared Foundation AssetのCurrent State（現在状態）の投入。→ 後続のPopulation Task（投入作業）へ委譲する。
- Effective Foundation State（有効基盤状態）のMaterialization / Cache（実体化／キャッシュ）の設計。
- Stable Asset ID体系、およびSource LocationからのAsset Identity（資産同一性）の分離方式。
- Foundation Provider（基盤提供主体）のLocationの決定方式、およびRemote Locationとしての解決方式。
- 本Contract（契約）に対するValidation Tool、Enforcement、およびCI。

これらが未確定であることは、本文書のDesign Gap（設計上の不足）ではない。
