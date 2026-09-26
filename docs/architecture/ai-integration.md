# AI Integration Architecture（AI連携アーキテクチャ）

## Purpose（目的）

本文書は、`noxris42` において**AI Integration（AI連携）** が何を成立させる責務体系であり、その責務がどのConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）の上で成立するのかを定義する上位Modelである。

本文書が扱う問いは次の4点である。

1. AI Integration（AI連携）は、何を成立させる責務体系なのか。
2. AI Integration（AI連携）のCore Responsibility（中核責務）として何が成立するのか。
3. Core Responsibility（中核責務）とは別に、AI Integration（AI連携）の成立に必要なBoundary Responsibility（境界責務）として何が成立するのか。
4. AI Integration（AI連携）は、Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）との間で、どのResponsibility Relationship（責務関係）とBoundary（境界）を持つのか。

本文書は上位Architectureとして自己完結する。具体的なEntry File、Navigation、Manifest、AI Tool Configuration（AI Tool設定）、およびVendor固有Mechanismの存在や内容を前提としない。

## Relationships（関係）

### Responsibility Boundary（責務境界）

本文書は、[Repository Governance](repository-governance.md)が定義するOwnership（所有責任）・Shared Scope・Foundation Applicationを再定義・上書きしない。また、[Documentation Structure Architecture](documentation-structure.md)および[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)が定義するDocumentation上の論理単位・Definition Authority（定義権限）の成立条件・Area Responsibility（領域責務）も再定義・上書きしない。

したがって次は本文書の責務ではない。

- ある定義・資産がShared Foundation Assetか、Repository-owned Assetかの判定。→ Repository Governanceの「Ownership Boundary（所有責任の境界）」による。
- あるShared Foundation Assetが特定Repositoryで有効になる関係、およびその判断。→ Repository GovernanceのFoundation Applicationによる。
- Documentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件。→ Documentation Structure Architectureによる。
- Convention（規約）の内部構造およびNormative Rule（規範的規則）の意味。→ [Convention Architecture](convention.md)による。

本文書が定義するのは、これらによってすでに成立しているDefinition（定義）とその適用結果を、AI Consumer（AI利用主体）が利用する際の責務体系のみである。

AI Integration Architecture（AI連携アーキテクチャ）自身のDefinition Authority（定義権限）は本文書が持つ。

### Position（設計上の位置づけ）

本文書は[Repository Governance](repository-governance.md)を上位Sourceとして参照する。

同文書は「AI Integrationの具体設計」および「`CLAUDE.md` / `AGENTS.md` / `.ai/` の具体仕様」をNon-goals（現在扱わない事項）としている。本文書は、その委譲先の一つとして、AI Integration（AI連携）のSemantic / Structural Modelを定義する。

Design Dependency（設計依存）は次の一方向とする。

```text
Repository Governance
        ▲
        │ refines
AI Integration Architecture
        ▲
        │ refines
後続のAI Integration設計
```

本文書は[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)が定義するArchitecture Area（アーキテクチャ領域）に属する通常のDocumentation Asset（文書資産）である。AI Integration（AI連携）というSubjectについて、その意味を成立させるSemantic / Structural Modelを定義する。

Current Repositoryに存在するAI向けのFile、Prototype、および過去のAI Integration実装は、本Modelに対するDefinition Authority（定義権限）を持たない。本文書は、それらの存在・内容・構成を前提とせず、それらから本Modelを導出しない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- AI Integration（AI連携）の意味と、それが成立させる責務体系
- AI Consumer（AI利用主体）の位置づけ
- AI Integration（AI連携）のCore Responsibility（中核責務）
- AI Integration（AI連携）のBoundary Responsibility（境界責務）
- AI Integration（AI連携）が所有しない責務の境界
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）
- Definition Authority（定義権限）・Foundation Application・Task Relevance（タスク関連性）の分離
- Foundation Definition（基盤定義）のResolution（解決）・Reference（参照）と、そのFoundation Definition（基盤定義）のDefinition Authority（定義権限）との境界
- Vendor IndependenceおよびMechanism Independence（機構非依存）の境界

### Out of Scope（本文書が定義しない範囲）

- Effective Foundation State（有効基盤状態）の生成方式、Schema、Manifest等のConcrete Representation（具体表現）
- Task Context（タスク文脈）の内部要素、Schema、およびTask Model
- Foundation Applicationの判断基準、Application Mechanism（適用方式）、およびその分類体系
- Discovery / Routing / Navigation等、Authoritative Foundation Resolution（正式基盤解決）の具体Mechanism
- AI Consumer（AI利用主体）へのEntry、およびそのConcrete Representation（具体表現）
- Task Procedure（タスク手順）およびSpecialized Capability（専門能力）そのもののDefinition（定義）
- Hook・Permission・Sandbox・CI等のDeterministic Enforcement（決定論的強制）
- MCP等のExternal Capability Integration（外部能力連携）
- Vendor固有のIntegration、およびそのAdapter
- `AGENTS.md`・`CLAUDE.md`・`.ai/`・`.claude/`・`.codex/`・`.agents/`等の具体Representation（表現）

詳細は「Non-goals」に示す。

## Concept Model（概念モデル）

### AI Integration（AI連携）

AI Integration（AI連携）は、AI Consumer（AI利用主体）が、Consumer Repository（利用Repository）で有効なShared Development Foundationについて、次の3つを成立させる責務体系である。

- 必要なFoundation Definition（基盤定義）のAuthoritative Definition（正式定義）を解決すること
- Effective Foundation State（有効基盤状態）を参照すること
- Current Task Context（現在タスク文脈）に対してRelevantな内容を利用可能にすること

AI Integration（AI連携）が成立させるのは、この3つを担う責務の体系である。特定のAI Toolに対する設定の集合ではない。

```text
AI Integration ≠ AI Tool Configuration
```

### AI Consumer（AI利用主体）

AI Consumer（AI利用主体）は、AI Integration（AI連携）を通じて、Consumer Repository（利用Repository）で有効なShared Development Foundationを利用する主体である。

AI Consumer（AI利用主体）は、Foundation Applicationに対するDecision Authority（判断権限）を持たない。

本文書は、AI Consumer（AI利用主体）が具体的にどのProductまたはRuntimeであるかを定義しない。

### Foundation Definition（基盤定義）

Foundation Definition（基盤定義）は、Shared Foundation Assetとして成立しているDefinition（定義）のうち、AI Integration（AI連携）が解決・参照の対象とするものである。本文書がAI Integration（AI連携）のModelを成立させるために定義するConcept（概念）であり、[Repository Governance](repository-governance.md)が定義するConcept（概念）ではない。

Shared Foundation Assetとしての成立、そのOwnership（所有責任）、およびそれが特定Repositoryで有効になる関係は、いずれも[Repository Governance](repository-governance.md)が定める。Definition Authority（定義権限）の成立条件は[Documentation Structure Architecture](documentation-structure.md)が定める。本文書はいずれも再定義せず、Foundation Definition（基盤定義）についてOwnership（所有責任）に関するModelを新たに導入しない。

Repository-owned Assetは、Foundation Definition（基盤定義）に含まれない。本文書は、AI Integration（AI連携）におけるRepository-owned Assetの扱いを定義しない。

### Authoritative Source（正式Source）

Authoritative Source（正式Source）は、あるFoundation Definition（基盤定義）について、そのDefinition Authority（定義権限）を持つSourceである。

あるFoundation Definition（基盤定義）を解決した先がAuthoritative Source（正式Source）であるとき、そのFoundation Definition（基盤定義）をAuthoritative Foundation Definition（正式基盤定義）と呼ぶ。

### Effective Foundation State（有効基盤状態）

Effective Foundation State（有効基盤状態）は、Foundation Applicationの結果として、特定Repositoryで現在有効になっているShared Foundation（共通基盤）の状態である。

Effective Foundation State（有効基盤状態）は、次を含み得る。

- 当該Repositoryで有効なShared Foundation Asset、すなわち解決済みのFoundation Application
- 当該Repositoryで有効なConvention（規約）について成立しているTarget-specific Rule Selection（対象固有規則選択）、すなわち解決済みのTarget-specific Rule Selection（対象固有規則選択）

したがって、Target-specific Rule Selection（対象固有規則選択）は、Effective Foundation State（有効基盤状態）の一部として参照され得る。Foundation ApplicationおよびTarget-specific Rule Selection（対象固有規則選択）の意味と、両者およびRule Applicabilityとの境界は[Repository Governance](repository-governance.md)が定める。本文書はこれらを再定義しない。

Rule Applicability、すなわち各Normative Rule（規範的規則）が何に対してApplicableであるかは、[Convention Architecture](convention.md)が定めるとおり、そのRule Statement（規則文）が規定する対象・条件から定まる。Effective Foundation State（有効基盤状態）がTarget-specific Rule Selection（対象固有規則選択）を含むことは、Rule Applicabilityを含む・変更することではない。

Effective Foundation State（有効基盤状態）は、AI Integration（AI連携）にとって外部から与えられる入力である。本文書は、その生成方式、Schema、Manifest等のConcrete Representation（具体表現）を定義しない。

Effective Foundation State（有効基盤状態）を成立させるFoundation Application State（基盤適用状態）は、AI Integration（AI連携）の下位設計ではない。AI Integration（AI連携）がその結果であるEffective Foundation State（有効基盤状態）を消費する、隣接Subjectである。

```text
Foundation Application State
  = 隣接Subject
  ≠ AI Integrationの下位設計
```

### Task Context（タスク文脈）

Task Context（タスク文脈）は、Current Task（現在タスク）に対してRelevantなFoundation（関連基盤）を判断するために利用される文脈である。

Task Context（タスク文脈）はTask Relevance（タスク関連性）へ影響する。Foundation Applicationを決定しない。

本文書は、Task Context（タスク文脈）の内部要素、Schema、およびTask Modelを定義しない。

### Task Relevance（タスク関連性）

Task Relevance（タスク関連性）は、Effective Foundation State（有効基盤状態）に含まれるFoundation Definition（基盤定義）またはResourceが、Task Context（タスク文脈）に対して現在関連するという関係である。

Task Relevance（タスク関連性）はEffective Foundation State（有効基盤状態）およびRule Applicabilityを変更しない。すなわち、あるFoundation Definition（基盤定義）がRelevantであるか否かは、それが当該Repositoryで有効であるか否か、Target-specific Rule Selection（対象固有規則選択）の結果、およびRule Applicabilityを変えない。

### Referenced External Definitions（参照する外部定義）

次のConcept（概念）のDefinition Authority（定義権限）は本文書の外にある。本文書はこれらを参照するのみで、再定義しない。

| Concept（概念） | Definition Authority（定義権限）の所在 |
| --- | --- |
| Shared Development Foundation | [Repository Governance](repository-governance.md) |
| Shared Foundation Asset | [Repository Governance](repository-governance.md) |
| Foundation Application | [Repository Governance](repository-governance.md) |
| Target-specific Rule Selection（対象固有規則選択） | [Repository Governance](repository-governance.md) |
| Rule Applicability | 各Normative Rule（規範的規則）のRule Statement（規則文）。その意味は[Convention Architecture](convention.md) |
| Ownership（所有責任） | [Repository Governance](repository-governance.md) |
| Repository-specific State（Repository固有状態） | 当該Consumer Repository（利用Repository） |
| Definition Authority（定義権限）の成立条件 | [Documentation Structure Architecture](documentation-structure.md) |

Foundation Definition（基盤定義）は本文書が定義するConcept（概念）であり、上表には含まれない。Foundation Definition（基盤定義）がShared Foundation Assetとして成立する条件は[Repository Governance](repository-governance.md)の責務に属する。

### Concept Relationships（Concept間の関係）

```text
Foundation Provider
  provides
Foundation Definition

Consumer Repository
  determines
Foundation Application

Foundation Application
  establishes
Effective Foundation State

AI Integration
  accesses
Effective Foundation State

AI Integration
  resolves
Authoritative Foundation Definition

Task Context
  influences
Task Relevance Resolution

Task Context
  does not determine
Foundation Application

AI Consumer
  uses
AI Integration
```

上記はResponsibility Relationship（責務関係）であり、Runtimeにおける処理順序ではない。記載の並びから、実行順序、呼び出し関係、またはData Flowを導出しない。

## Responsibility Model（責務モデル）

### Core Responsibilities（中核責務）

AI Integration（AI連携）のCore Responsibility（中核責務）は次の3つである。

#### Authoritative Foundation Resolution（正式基盤解決）

必要なFoundation Definition（基盤定義）について、そのDefinition Authority（定義権限）を持つAuthoritative Source（正式Source）へ解決する責務である。

本文書は、Discovery / Routing / Navigation等、この解決を実現する具体Mechanismを固定しない。

#### Effective Foundation State Access（有効基盤状態参照）

Foundation Applicationによって決定済みのEffective Foundation State（有効基盤状態）を参照・利用する責務である。

AI Integration（AI連携）自身は、Foundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityのいずれも決定・変更・上書きしない。Effective Foundation State（有効基盤状態）は、AI Integration（AI連携）にとって参照の対象であり、生成または改変の対象ではない。

#### Task Relevance Resolution（タスク関連性解決）

Effective Foundation State（有効基盤状態）の中から、Task Context（タスク文脈）に対して現在RelevantなFoundation Definition（基盤定義）またはResourceを特定する責務である。

この特定は、Task Relevance（タスク関連性）を確定させる。Foundation ApplicationおよびTarget-specific Rule Selection（対象固有規則選択）によって成立したEffective Foundation State（有効基盤状態）そのもの、ならびにRule Applicabilityは変更しない。

### Boundary Responsibilities（境界責務）

次の2つは、AI Integration（AI連携）に属する責務であるが、Core Responsibility（中核責務）ではない。Boundary Responsibility（境界責務）として扱う。

```text
Core Responsibility ≠ Boundary Responsibility
```

Core Responsibility（中核責務）が担うのは、Shared Development Foundationの解決・参照・関連性特定である。Boundary Responsibility（境界責務）が担うのは、その責務体系が外部と接する箇所の成立である。両者を同一の責務として扱わない。

#### Bootstrap Responsibility（初期接続責務）

AI Consumer（AI利用主体）がAI Integration（AI連携）の利用を開始できる状態を成立させる責務である。

本文書は、`AGENTS.md` 等、この責務を担う具体Representation（表現）を定義しない。

#### Delivery Adaptation Responsibility（提供適応責務）

Vendor-independentなAI Integration Semantics（AI連携意味モデル）を、Concrete AI Consumer（具体AI利用主体）が利用可能な形へ接続する責務である。

Vendor固有Mechanismは本文書では扱わず、後続設計へ委譲する。

### Responsibilities Not Owned（AI Integrationが所有しない責務）

#### Task Procedure / Specialized Capability（タスク手順／専門能力）

Task Procedure（タスク手順）およびSpecialized Capability（専門能力）が、AI Integration（AI連携）とは別に成立することを許容する。

AI Integration（AI連携）は、必要に応じてそれらへ接続・解決できる。ただし次を所有しない。

- Task Procedure（タスク手順）そのもののDefinition（定義）
- Specialized Capability（専門能力）そのもののDefinition（定義）

Skill・Subagent等は、これらが成立する場合のConcrete Mechanism Candidate（具体機構候補）である。本文書は、それらをArchitecture Concept（アーキテクチャ概念）として要求しない。

#### Deterministic Enforcement / External Capability（決定論的強制／外部能力）

AI Integration（AI連携）は次を所有しない。

- Hook
- Permission
- Sandbox
- CI等のDeterministic Enforcement（決定論的強制）
- MCP等のExternal Capability Integration（外部能力連携）

Instruction / ResolutionとDeterministic Enforcement（決定論的強制）は別の責務である。AI Integration（AI連携）が担うのは前者であり、後者の成立・実施をAI Integration（AI連携）の責務として扱わない。

```text
Instruction / Resolution ≠ Deterministic Enforcement
```

## Foundation Provider / Consumer Repository / AI Consumer Relationship（基盤提供主体・利用Repository・AI利用主体の関係）

### Foundation Provider（基盤提供主体）

`.github` を含むShared Development Foundation側は、Foundation Definition（基盤定義）を、AI Consumer（AI利用主体）から解決可能な形で提供する。

そのFoundation Definition（基盤定義）のOwnership（所有責任）は[Repository Governance](repository-governance.md)が定める。本文書はこれを再定義しない。

### Consumer Repository（利用Repository）

Consumer Repository（利用Repository）は、自身へのFoundation Applicationを判断し、Repository-specific State（Repository固有状態）を所有する。

Foundation Applicationの結果として、そのRepositoryにEffective Foundation State（有効基盤状態）が成立する。

### AI Consumer（AI利用主体）

AI Consumer（AI利用主体）は、Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）が成立させたDefinition（定義）およびStateを、AI Integration（AI連携）を通じて利用する。

AI Consumer（AI利用主体）およびAI Integration（AI連携）は、Foundation Applicationに対するDecision Authority（判断権限）を持たない。

```text
AI Consumer     → Foundation Applicationの判断主体ではない
AI Integration  → Foundation Applicationの判断主体ではない
```

### `.github` Handling（`.github`の扱い）

`.github` 自身も[Repository Governance](repository-governance.md)が定義するModelに従う。したがって `.github` は、Foundation Provider（基盤提供主体）としての役割に加えて、必要に応じてConsumer Repository Role（利用Repository役割）を持つ。

この場合も、本文書が定めるResponsibility Relationship（責務関係）は変わらない。

## Definition Authority / Application / Relevance Separation（定義権限・適用・関連性の分離）

AI Integration（AI連携）が扱う3つの軸は、それぞれ別の事柄である。混同してはならない。

| 軸 | 何を確定させるか | 判断主体 |
| --- | --- | --- |
| Definition Authority（定義権限） | ある内容を最終的に定義する責務をどのSourceが持つか | 当該Definition（定義）を所有するDefinition Authority（定義権限） |
| Foundation Application | どのShared Foundation Assetが当該Repositoryで有効か | Consumer Repository（利用Repository） |
| Task Relevance（タスク関連性） | 有効な内容のうち、どれがCurrent Task（現在タスク）に関連するか | AI Integration（AI連携） |

### Definition Authority（定義権限）

AI Integration（AI連携）は、Foundation Definition（基盤定義）を利用する際、そのDefinition Authority（定義権限）を持つAuthoritative Source（正式Source）へ解決する。

解決先が確定していない内容を、Foundation Definition（基盤定義）として利用しない。

### Foundation Application（共通開発基盤資産の適用関係）

Foundation Applicationを決定するのはConsumer Repository（利用Repository）である。

AI Integration（AI連携）、AI Consumer（AI利用主体）、およびTask Context（タスク文脈）は、いずれもFoundation Applicationを決定しない。

### Task Relevance（タスク関連性）

Task Relevance（タスク関連性）は、Effective Foundation State（有効基盤状態）の内部で成立する関係である。

したがって次が成立する。

- あるFoundation Definition（基盤定義）がCurrent Task（現在タスク）にRelevantでないことは、それが当該Repositoryで有効でないことを意味しない。
- Task Context（タスク文脈）の変化は、Effective Foundation State（有効基盤状態）を変化させない。

### Authoritative Documentation Boundary（正式文書の境界）

AI-specific Context、Navigation、Procedure、Adapter等のAI Integration Resource（AI連携資源）は、Foundation Definition（基盤定義）を複製・再定義しない。担うのは、既存のAuthoritative Source（正式Source）へ解決することである。

あるFoundation Definition（基盤定義）をResolution（解決）・Reference（参照）する役割を持つことは、そのFoundation Definition（基盤定義）に対するDefinition Authority（定義権限）を成立させない。Resolution（解決）およびReference（参照）は、対象となるFoundation Definition（基盤定義）のDefinition Authority（定義権限）を新たに生成せず、そのAuthoritative Source（正式Source）から移転もしない。

```text
Resolution / Reference Role
  does not establish
Definition Authority over the resolved Foundation Definition
```

本境界が定めるのは、Resolution（解決）・Reference（参照）という役割と、その対象であるFoundation Definition（基盤定義）のDefinition Authority（定義権限）との関係のみである。次は本境界が定めるものではない。

- AI Integration Resource（AI連携資源）が、別のSubjectについてDefinition Responsibility（定義責務）を担うこと。本境界は、その可能性を否定しない。
- あるDocumentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件。Definition Authority（定義権限）はAsset Type（資産種別）ではなく、そのAssetが担うDefinition Responsibility（定義責務）によって成立する。その成立条件は[Documentation Structure Architecture](documentation-structure.md)が定める。本文書はこれを再定義しない。

## Independence（非依存）

### Vendor Independence（Vendor非依存）

AI Integration Semantics（AI連携意味モデル）は、Current Product（現在のProduct）から独立して成立させる。

すなわち、Claude Code・Codex・Antigravity等の具体Productが現在どのような機構を備えているかを根拠として、本ModelのConcept（概念）・Responsibility（責務）・Relationshipを導出しない。

Vendor-specific Need（Vendor固有必要性）が存在する場合、それはDelivery Adaptation Responsibility（提供適応責務）および後続のVendor-specific Integrationで扱う。Vendor固有Mechanismを、本ModelのArchitecture Requirement（アーキテクチャ要求）へ昇格させない。

### Mechanism Independence（機構非依存）

本文書は、次の具体Mechanism / Representation（表現）を確定しない。

- `AGENTS.md`
- `CLAUDE.md`
- `.ai/`
- Navigation File
- Manifest
- Skill / `SKILL.md`
- Subagent
- Hook
- MCP
- `.claude/`
- `.codex/`
- `.agents/`

これらが存在し得ることを本文書は妨げない。妨げないことと、本ModelがそれらをRequirementとして要求することとは別の事柄である。

## Design Principles（設計原則）

本節が示すのは、本文書が定義するModelを前提として成立するLocal Design Principle（局所設計原則）である。Philosophy Area（思想領域）が所有するFundamental Principle（根本原則）ではない。

### Authority before Use（利用に先立ち定義権限へ解決する）

Foundation Definition（基盤定義）を利用する際は、そのDefinition Authority（定義権限）を持つAuthoritative Source（正式Source）へ解決する。手元に存在する内容であることを、利用してよい根拠としない。

### Application and Relevance Separation（適用と関連性を分離する）

Foundation Applicationによって何が有効であるかと、Task Relevance（タスク関連性）によって何が現在関連するかを、別の判断として扱う。

### Relevance Does Not Alter Application（関連性は適用を変更しない）

Task Context（タスク文脈）に基づくSelectionは、Effective Foundation State（有効基盤状態）を変更しない。選ばれなかったことは、有効でないことを意味しない。

### Resolution Does Not Redefine（解決は再定義しない）

Foundation Definition（基盤定義）をResolution（解決）・Reference（参照）する役割は、そのFoundation Definition（基盤定義）を再定義せず、それに対するDefinition Authority（定義権限）も取得しない。担うのは、Authoritative Source（正式Source）への解決である。

### Vendor-independent Semantics（意味モデルをVendorから独立させる）

Semantic Model（意味モデル）を、特定Productの機構から導出しない。Vendor固有の必要性は、意味モデルではなく提供の側で扱う。

### Mechanism Independence（機構を上位で固定しない）

上位Architectureは責務と関係を定義し、具体的なEntry、Manifest、Skill、Agent等を先行して固定しない。

## Non-goals（現在扱わない事項）

本文書は次を定義しない。ここで示す事項はDesign Gapではない。本文書の現在の責務に基づいて、意図的に定義・解決・導入の対象外としている事項であり、必要なものは後続設計へ委譲する。

### Downstream Design（後続設計へ委譲する事項）

- Cross-agent Entry Design
- AI Context Resolution / Navigation Design
- Task Procedure Model
- Specialized Capability Model
- Vendor-specific Integration
- Enforcement Integration

### Concepts Not Introduced（導入しないConcept）

- **Output Stateの独立Concept（概念）化**

  Task Relevance Resolution（タスク関連性解決）の結果を、`Relevant Foundation Context` 等の独立したConcept（概念）またはAssetとして先行導入しない。現在のModelは、Task Relevance（タスク関連性）という関係で足りる。

- **Future Resolution Capability（将来の解決能力）**

  基盤側に置かれ得るResolver、Agent等のFuture Resolution Capability（将来の解決能力）を、Current Architectureへ導入しない。必要性が具体的に確認された時点で後続設計する。

### Declaration / Representation Format（宣言・記述形式に関する事項）

- Manifest Schema
- Effective Foundation State（有効基盤状態）の機械可読な表現形式
- Task Context（タスク文脈）のSchema

### Classification（分類に関する事項）

- Foundation Applicationの分類体系
- AI Integration Resource（AI連携資源）の分類体系
- AI Consumer（AI利用主体）の分類体系

## Usage by Downstream Design（下位設計からの参照）

後続設計は、本文書を参照して次を前提にできる。これらを再定義する必要はない。

1. AI Integration（AI連携）が何を成立させる責務体系であるか。
2. Core Responsibility（中核責務）として何が成立し、Boundary Responsibility（境界責務）として何が成立するか。
3. AI Integration（AI連携）が所有しない責務の範囲。
4. Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）と、Foundation Applicationに対するDecision Authority（判断権限）の所在。
5. Definition Authority（定義権限）・Foundation Application・Task Relevance（タスク関連性）の分離。
6. Foundation Definition（基盤定義）をResolution（解決）・Reference（参照）する役割が、そのFoundation Definition（基盤定義）に対するDefinition Authority（定義権限）を成立させないこと。

本文書からは判断できないのは、これらの責務を**どのMechanismおよびRepresentation（表現）で実現するか** であり、これは後続設計の責務に属する。
