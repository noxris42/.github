# Repository Orientation / Navigation Architecture（Repository方向付け／探索アーキテクチャ）

## Purpose（目的）

本文書は、`noxris42/.github` Repositoryについて、Repositoryを網羅的に物理探索することなく理解・探索可能にする**Repository Orientation / Navigation（Repository方向付け／探索）** が何を成立させる責務であり、その責務がどのResponsibility（責務）・Relationship・Boundary（境界）の上で成立するのかを定義するSemantic / Structural Modelである。

本文書が扱う問いは次の4点である。

1. Repository Orientation / Navigation（Repository方向付け／探索）は、何を成立させる責務なのか。
2. その責務は、どのResponsibility（責務）へ分解され、それぞれは何を担うのか。
3. Repository Orientation / Navigation（Repository方向付け／探索）は、Documentation Asset（文書資産）の組合せによってどのように成立し得るのか。
4. Repository Orientation / Navigation（Repository方向付け／探索）は、構造の俯瞰と網羅、Navigationと参照先のDefinition Authority（定義権限）、および人間による利用とAI Consumer（AI利用主体）による利用の間で、どのBoundary（境界）を持つのか。

本文書は、[Repository Governance](repository-governance.md)および[Documentation Structure Architecture](documentation-structure.md)のみを上位前提として自己完結する。`README.md`、Directory README、その他Repository Orientation / Navigation（Repository方向付け／探索）の成立に寄与し得る具体的なDocumentation Asset（文書資産）の存在・内容・Concrete Representation（具体表現）を前提としない。

## Relationships（関係）

### Responsibility Boundary（責務境界）

本文書は、[Repository Governance](repository-governance.md)が定義するOwnership（所有責任）・Shared Scope・Foundation Applicationを再定義・上書きしない。また、[Documentation Structure Architecture](documentation-structure.md)が定義するDocumentation Asset（文書資産）・Document Responsibility（文書責務）・Definition Authority（定義権限）の成立条件・Section・Responsibility Decomposition（責務分解）・Logical / Physical Boundaryも再定義・上書きしない。

したがって次は本文書の責務ではない。

- あるResourceがShared Foundation Assetか、Repository-owned Assetかの判定。→ Repository Governanceの「Ownership Boundary（所有責任の境界）」による。
- あるDocumentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件。→ Documentation Structure Architectureによる。
- Repository Orientation / Navigation（Repository方向付け／探索）が参照するResource・Subjectそれぞれの内容。→ 当該Subjectを所有するDefinition Authority（定義権限）による。
- AI Consumer（AI利用主体）によるAuthoritative Foundation Resolution（正式基盤解決）の責務体系。→ [AI Integration Architecture](ai-integration.md)による。

Repository Orientation / Navigation Architecture（Repository方向付け／探索アーキテクチャ）自身のDefinition Authority（定義権限）は本文書が持つ。

### Position（設計上の位置づけ）

本文書は[Repository Governance](repository-governance.md)および[Documentation Structure Architecture](documentation-structure.md)を上位Sourceとして参照する。

Documentation Structure Architectureは、Document Responsibility（文書責務）にNavigation等が含まれ得ることを示したうえで、Navigationを担う文書を必須Concept（概念）として導入せず、Navigationを必要性が確認された時点でDocument Responsibility（文書責務）の一種として設計できる補助的責務としている。本文書は、`.github` Repositoryについて確認されたSemantic Need（意味上の必要性）に基づき、Repository Orientation / Navigation（Repository方向付け／探索）のSemantic / Structural Modelを定義する。Document Responsibility（文書責務）とは別のStructural Roleを導入しない。

Repository Governanceは、`.github` もGovernanceの単位となる一つのRepositoryであると定義する。本文書が扱うのは、そのRepositoryとしての `.github` を理解・探索可能にすることである。

現在確認されているSemantic Need（意味上の必要性）は `.github` Repository固有である。本文書は、Repository Orientation / Navigation（Repository方向付け／探索）を全Repositoryへ共通適用するRule、およびShared Foundation Assetとしての位置づけを定義しない。共有責務が成立するかどうかは、Repository Governanceの「Shared Scope Principles」に従い、その必要性が実際に確認された時点で別途判断する。

Design Dependency（設計依存）は次の一方向とする。

```text
Repository Governance
        ▲
        │ refines
Repository Orientation / Navigation Architecture

Documentation Structure Architecture
        ▲
        │ refines
Repository Orientation / Navigation Architecture
```

本文書は[Repository Governance Documentation Framework](repository-governance-documentation-framework.md)が定義するArchitecture Area（アーキテクチャ領域）に属する通常のDocumentation Asset（文書資産）である。Repository Orientation / Navigation（Repository方向付け／探索）というSubjectについて、その意味を成立させるSemantic / Structural Modelを定義する。

本文書は、上位Architectureの意味を変更・補完しない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository Orientation / Navigation（Repository方向付け／探索）の意味と、それが成立させる責務
- Repository Orientation / Navigation（Repository方向付け／探索）を構成する4つのResponsibility（責務）と、それぞれの意味
- Major Resource Structure（主要資源構造）とComplete Resource Coverage（完全資源網羅）のBoundary（境界）
- Navigation Composition（Navigation構成）と、それを構成する各Documentation Asset（文書資産）のDocument Responsibility（文書責務）との関係
- Repository Orientation / Navigation（Repository方向付け／探索）と、参照先SubjectのDefinition Authority（定義権限）とのBoundary（境界）
- Primary Consumption（主たる利用）と、AI Consumer（AI利用主体）による利用とのBoundary（境界）

### Out of Scope（本文書が定義しない範囲）

- Navigation Composition（Navigation構成）を構成する具体的なDocumentation Asset（文書資産）の特定、その数、およびPhysical Location（物理配置）
- `README.md`、Directory READMEその他のConcrete Representation（具体表現）、およびそのSection構成・Table・Tree・Resource Group・Link形式
- Resourceの分類体系、およびMajor Resource Structure（主要資源構造）へ含めるResourceの選定基準
- 参照先Resource・Subjectそれぞれの内容、およびそのDefinition（定義）
- 全Repositoryへ適用するRule、およびShared Foundation Assetとしての位置づけ
- AI-specific Metadata / Manifest / Schema / Navigation Mechanism
- Authoritative Foundation Resolution（正式基盤解決）、Primary Resolution（主たる解決）、およびFallback Foundation-wide Navigation / Discovery
- Coverage（網羅）の検証方法、Validation、およびTool要求
- Navigation Composition（Navigation構成）を構成するDocumentation Asset（文書資産）の更新手順その他のDocumentation Lifecycle（文書の生涯管理）

## Responsibility Model（責務モデル）

### Repository Orientation / Navigation（Repository方向付け／探索）

Repository Orientation / Navigation（Repository方向付け／探索）は、読み手が、Repositoryを網羅的に物理探索することなく、Repositoryが何であるかを理解し、Repository内の必要なResourceへ到達できる状態を成立させる責務である。

Repository Orientation / Navigation（Repository方向付け／探索）は、次の4つのResponsibility（責務）へ分解される。

```text
Repository Orientation / Navigation
├─ Repository Identity / Responsibility
├─ Major Resource Structure
├─ Complete Resource Coverage
└─ Exploration Guidance
```

4つのResponsibility（責務）は、それぞれ別の事柄を成立させる。一方が成立していることをもって、他方が成立しているとは扱わない。

上図の列挙順は、Responsibility（責務）の優先順位・読解順序・Documentation上の配置順を示さない。また、各Responsibility（責務）がそれぞれ独立したSectionまたはDocumentation Asset（文書資産）として表現されることを要求しない。

### Repository Identity / Responsibility（Repository同一性／責務）

Repository Identity / Responsibility（Repository同一性／責務）は、Repositoryが何を表し、何を担うかを、読み手が理解可能にする責務である。

この責務が成立させるのは、以降のResourceを読み手がどの前提の下で理解すべきかという方向付けである。

Repositoryが何を担うかのDefinition（定義）は、この責務には属さない。`.github` の責務は[Repository Governance](repository-governance.md)が定義する。Repository Identity / Responsibility（Repository同一性／責務）は、そのDefinition（定義）を理解可能にするよう提示・要約するのであり、再定義しない（「Navigation and Definition Authority」を参照）。

### Major Resource Structure（主要資源構造）

Major Resource Structure（主要資源構造）は、Repository内の主要ResourceとPhysical Structure（物理構造）の関係を、全体を俯瞰できる粒度で理解可能にする責務である。

Physical Structure（物理構造）を示すことは、Logical Structure（論理構造）を定義することではない。たとえばあるDirectoryを示すことは、そこにDocumentation Area（文書責務領域）が成立することを意味しない。Logical Structure（論理構造）の成立は、[Documentation Structure Architecture](documentation-structure.md)およびそれを具体化するDocumentation Framework（文書体系）が定める。

### Complete Resource Coverage（完全資源網羅）

Complete Resource Coverage（完全資源網羅）は、Current RepositoryでVersion管理されているFileを、Navigation Composition（Navigation構成）全体から漏れなく識別・探索可能にする責務である。

対象はVersion管理されているFileに限られる。本文書は、Directory、Submodule、生成物その他のFile以外のResourceへ対象を広げない。

Navigation Composition（Navigation構成）を構成するDocumentation Asset（文書資産）自身がVersion管理されているFileである場合、他のFileと同様に対象から除外されない。

Complete Resource Coverage（完全資源網羅）は、Fileの存在を識別・探索可能にするのであり、そのOwnership（所有責任）を判定しない。Repository Governanceが定めるとおり、Repositoryに存在することと所有することは別の事柄である。

Complete Resource Coverage（完全資源網羅）は、一つのDocumentation Asset（文書資産）がすべてのFileを直接列挙することを意味しない。成立するかどうかはNavigation Composition（Navigation構成）全体として判断し、個々のDocumentation Asset（文書資産）が単独で全Fileを識別可能にすることは要求しない。

```text
Complete Resource Coverage
≠ 単一Documentation Assetによる全Fileの直接列挙
```

本文書は、個々のFileをどの粒度・形式で識別可能にするかを固定しない。ただし、いずれの形式を採る場合であっても、Navigation Composition（Navigation構成）全体から識別・探索できないVersion管理されているFileが残る状態を、Complete Resource Coverage（完全資源網羅）の成立として扱わない。

### Exploration Guidance（探索案内）

Exploration Guidance（探索案内）は、読み手の目的または知りたいSubjectから、適切なResourceまたは探索開始地点へ到達可能にする責務である。

Exploration Guidance（探索案内）が起点とするのは、読み手の目的またはSubjectである。Resourceの配置を起点とするMajor Resource Structure（主要資源構造）およびComplete Resource Coverage（完全資源網羅）とは、起点が異なる。

Exploration Guidance（探索案内）は、すべての目的・Subjectに対する経路を網羅することを要求しない。また、Exploration Guidance（探索案内）が案内しないFileがあることは、Complete Resource Coverage（完全資源網羅）が成立していないことを意味しない。

到達先は、Resourceそのものに限られない。読み手がそこから探索を続けられる探索開始地点であってもよい。

## Navigation Composition（Navigation構成）

Repository Orientation / Navigation（Repository方向付け／探索）は、一つまたは複数のDocumentation Asset（文書資産）の組合せによって成立し得る。本文書では、Repository Orientation / Navigation（Repository方向付け／探索）の成立に寄与するDocumentation Asset（文書資産）の組合せをNavigation Composition（Navigation構成）と呼ぶ。Navigation Composition（Navigation構成）は、本Modelを説明するための局所的なConcept（概念）である。

```text
Repository Orientation / Navigation
    ↓ collectively established by
Navigation Composition
    = 1..n Documentation Assets

each Documentation Asset
    → has its own Document Responsibility
```

Navigation Composition（Navigation構成）を構成する各Documentation Asset（文書資産）は、それぞれ自身のDocument Responsibility（文書責務）を担う。Repository Orientation / Navigation（Repository方向付け／探索）は、それらのDocument Responsibility（文書責務）の組合せによって成立する。一つのDocument Responsibility（文書責務）を複数のDocumentation Asset（文書資産）が共有するのではない。Documentation Structure ArchitectureがDocumentation Asset（文書資産）を一つのDocument Responsibility（文書責務）を担う論理的Assetとして定義することを、本文書は変更しない。

Navigation Composition（Navigation構成）は、4つのResponsibility（責務）の一部を、下位のDocumentation Asset（文書資産）が自身のDocument Responsibility（文書責務）として担うことを妨げない。一方で本文書は、次のいずれも要求しない。

- 複数のDocumentation Asset（文書資産）から構成すること
- Directory READMEその他、特定のConcrete Representation（具体表現）を用いること
- 4つのResponsibility（責務）を、それぞれ特定のDocumentation Asset（文書資産）へ一対一で割り当てること

Navigation Composition（Navigation構成）が複数のDocumentation Asset（文書資産）から成る場合、それらのDocumentation Asset（文書資産）そのものへ読み手が到達可能であることが、Navigation Composition（Navigation構成）全体として責務が成立する前提となる。本文書はその到達経路のConcrete Representation（具体表現）を定めない。

Navigation Composition（Navigation構成）は、Documentation Structure Architectureが導入しない「Navigation Document」を、特別な構造上のConcept（概念）・Asset Type（資産種別）・Structural Roleとして導入するものではない。

## Responsibility Boundaries（本Model内の責務境界）

### Structure and Coverage（構造と網羅）

Major Resource Structure（主要資源構造）とComplete Resource Coverage（完全資源網羅）は、別のResponsibility（責務）である。

```text
Major Resource Structure
→ overview-oriented
→ representation may be selective

Complete Resource Coverage
→ completeness-oriented
→ managed files must not be omitted
```

したがって次が成立する。

- Major Resource Structure（主要資源構造）に現れないResourceがあることは、そのResourceが存在しないこと、または重要でないことを意味しない。
- Major Resource Structure（主要資源構造）が選択的であることは、Complete Resource Coverage（完全資源網羅）における省略を正当化しない。
- Complete Resource Coverage（完全資源網羅）が完全であることは、Major Resource Structure（主要資源構造）へすべてのFileを含めることを要求しない。

両者が同一のDocumentation Asset（文書資産）またはRepresentation（表現）によって同時に担われることは妨げない。その場合も、俯瞰のための選択と網羅のための完全性を、同一の要求として扱わない。

### Navigation and Definition Authority（Navigationと定義権限）

Navigation Composition（Navigation構成）を構成するDocumentation Asset（文書資産）は、Resourceをidentify・orient・summarize・locate・routeしてよい。ただし、そのことによって参照先SubjectのDefinition Authority（定義権限）を取得しない。

```text
identify / orient / summarize / locate / route
  does not establish
Definition Authority over the referenced Subject
```

したがって次が成立する。

- 参照先SubjectのDefinition（定義）は、そのSubjectを所有するDefinition Authority（定義権限）側にある。Navigationによる説明・要約が参照先のDefinition（定義）と異なる場合、Navigation側の説明・要約はそのDefinition（定義）を変更しない。
- Navigationによる要約を、参照先のDefinition（定義）の代替として扱わない。
- あるResourceがNavigationに現れること、または現れないことは、そのResourceの意味・Ownership（所有責任）・Foundation Applicationを変更しない。

本境界が定めるのは、Navigationという役割と、その参照先SubjectのDefinition Authority（定義権限）との関係のみである。Navigation Composition（Navigation構成）を構成するDocumentation Asset（文書資産）が、別のSubjectについてDefinition Responsibility（定義責務）を担う可能性を、本境界は否定しない。Definition Authority（定義権限）の成立条件は[Documentation Structure Architecture](documentation-structure.md)が定める。

### Human and AI Consumption（人間とAIによる利用）

Repository Orientation / Navigation（Repository方向付け／探索）のPrimary Consumption（主たる利用）は、Human-facingである。

AI Consumer（AI利用主体）が、Navigation Composition（Navigation構成）を構成する同じDocumentation Asset（文書資産）を利用することは許容する。ただし、AI Consumer（AI利用主体）による利用はSecondaryであり、それを理由として次を本Modelへ導入しない。

- AI-specific Metadata / Manifest / Schema
- AI-specific Navigation Mechanism
- Authoritative Foundation Resolution（正式基盤解決）

```text
Primary Consumption   → Human-facing
AI Consumer Usage     → permitted, secondary
AI Consumer Usage     ≠ AI-specific Requirement
```

Authoritative Foundation Resolution（正式基盤解決）は[AI Integration Architecture](ai-integration.md)が定義する責務であり、その経路は同Architectureを具体化する後続設計が定める。本Modelは、その経路、Primary Resolution（主たる解決）、およびPrimary Resolution（主たる解決）が成立しない場合のFallback Foundation-wide Navigation / Discoveryを定義・変更せず、それらの代替としても位置づけない。

とくに、Complete Resource Coverage（完全資源網羅）がVersion管理されているFileを網羅することは、それがFallback Foundation-wide Navigation / Discoveryとして成立することを意味しない。
