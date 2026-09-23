# AI Context Resolution Specification（AI文脈解決仕様）

## Purpose（目的）

本文書は、`noxris42` において**Cross-agent Entry（Agent横断入口）以降、Effective Foundation State（有効基盤状態）とTask Context（タスク文脈）を前提として、Current Task（現在タスク）にRelevantなAuthoritative Foundation Source（正式基盤Source）へ到達するためのConcrete Contract（具体契約）を定義する**Specification Asset（仕様資産）である。

本文書が扱う問いは次の6点である。

1. Cross-agent Entry（Agent横断入口）以降のResolution（解決）は、どのConcrete Representation（具体表現）を前提として成立するのか。
2. そのConcrete Representation（具体表現）は、何を保持し、何を保持しないのか。
3. そこに保持されるResolution Information（解決情報）は、Task Relevance Resolution（タスク関連性解決）に対してどの位置を占めるのか。
4. Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）は、そのResolution Information（解決情報）についてどの責務を分担するのか。
5. 保持されたSource Locationから、実際に参照可能なLocationはどのように成立するのか。
6. Entry（入口）とResolution（解決）の境界、およびResolution（解決）とDefinition Authority（定義権限）の境界はどこにあるのか。

本文書が定義するのは、この6点に対するConcrete Contract（具体契約）に限られる。本文書は、AI Integration（AI連携）のSemantic / Structural Model（意味／構造モデル）を定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するSpecifications Area（仕様領域）に属する通常のDocumentation Asset（文書資産）である。AI Integration（AI連携）という特定Subjectについて、そのAuthoritative Foundation Resolution（正式基盤解決）を成立・実現可能にするConcrete Contract（具体契約）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

Cross-agent Entry（Agent横断入口）以降のResolution（解決）のConcrete Contract（具体契約）についてのDefinition Authority（定義権限）は本文書が持つ。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は上位設計にある。本文書はこれらを参照するのみで、再定義・上書きしない。

- AI Integration（AI連携）の意味、そのCore Responsibility（中核責務）およびBoundary Responsibility（境界責務）
- Authoritative Foundation Resolution（正式基盤解決）、Effective Foundation State Access（有効基盤状態参照）、Task Relevance Resolution（タスク関連性解決）
- AI Consumer（AI利用主体）、Foundation Definition（基盤定義）、Authoritative Source（正式Source）、Authoritative Foundation Definition（正式基盤定義）
- Effective Foundation State（有効基盤状態）、Task Context（タスク文脈）、Task Relevance（タスク関連性）
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）
- Resolution（解決）・Reference（参照）がDefinition Authority（定義権限）を成立させないこと
- Cross-agent Entry（Agent横断入口）の成立、およびそのEntry Responsibility（入口責務）
- Shared Development Foundation、Shared Foundation Asset、Ownership（所有責任）、Foundation Application
- Documentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件、およびArea Responsibility（領域責務）

したがって次は本文書の責務ではない。

- AI Integration（AI連携）が成立させる責務体系そのもの。→ [AI Integration Architecture](../architecture/ai-integration.md)による。
- Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約）。→ [Cross-agent Entry Specification](cross-agent-entry.md)による。
- あるShared Foundation Assetが特定Repositoryで有効になる関係、およびその判断。→ [Repository Governance](../architecture/repository-governance.md)のFoundation Applicationによる。
- 本文書が参照対象として扱う各Authoritative Foundation Source（正式基盤Source）の内容。→ 当該Source自身による。

本文書が定めるのは、これらによってすでに成立しているDefinition（定義）へ到達するための具体的な経路のみである。

### Position（設計上の位置づけ）

本文書は[AI Integration Architecture](../architecture/ai-integration.md)を上位Sourceとして参照する。

同文書は、Authoritative Foundation Resolution（正式基盤解決）をCore Responsibility（中核責務）として定義する一方、Discovery / Routing / Navigationを含む具体Mechanism（具体機構）を意図的に固定せず、AI Context Resolution / Navigation Designへ委譲している。本文書は、その委譲先として、Resolution（解決）のConcrete Contract（具体契約）を定義する。

本文書は、[Cross-agent Entry Specification](cross-agent-entry.md)が意図的に定義しないnext-hopについて、その参照先となるConcrete Representation（具体表現）を定義する。両者は同一の上位Architectureを前提とする並列のSpecification Asset（仕様資産）であり、本文書はCross-agent Entry（Agent横断入口）のEntry Responsibility（入口責務）を変更・拡張しない。

Design Dependency（設計依存）は次の一方向とする。

```text
AI Integration Architecture
        ▲
        │ refines
AI Context Resolution Specification
```

本文書は、上位Architecture（アーキテクチャ）の意味を変更・補完しない。本文書が定めるConcrete Contract（具体契約）から、上位のConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）を導出・上書きしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Cross-agent Entry（Agent横断入口）以降のResolution（解決）が前提とするConcrete Representation（具体表現）
- 同Concrete Representation（具体表現）が担う責務、および担わない責務
- 同Concrete Representation（具体表現）が保持する最小のResolution Information（解決情報）
- Resolution Information（解決情報）とTask Relevance Resolution（タスク関連性解決）の境界
- Resolution Information（解決情報）とEffective Foundation State（有効基盤状態）の境界
- Resolution Information（解決情報）とDefinition Authority（定義権限）の境界
- Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）におけるResolution Information（解決情報）の責務分離
- 保持されたSource Locationから参照可能なLocationが成立する構成関係
- 同Concrete Representation（具体表現）が保持する内容の最小化、およびConvention（規約）の適用判断
- Cross-agent Entry（Agent横断入口）から同Concrete Representation（具体表現）へのnext-hop関係

### Out of Scope（本文書が定義しない範囲）

- AI Integration（AI連携）のCore Responsibility（中核責務）、およびそれを構成するConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）
- Cross-agent Entry（Agent横断入口）の成立、Entry Responsibility（入口責務）、およびそのConcrete Representation（具体表現）
- Task Context（タスク文脈）の内部要素、Schema、およびTask Model
- Task Relevance（タスク関連性）の判断基準、およびその判断結果の保持形式
- Effective Foundation State（有効基盤状態）の生成方式、Schema、Manifest等のConcrete Representation（具体表現）
- Foundation Applicationの判断、およびその適用方式
- Repository Orientation / Navigation（Repository方向付け／探索）、およびそのConcrete Representation（具体表現）。→ [Repository Orientation / Navigation Architecture](../architecture/repository-orientation-navigation.md)による。
- Foundation Provider（基盤提供主体）をRemote Locationとして解決する方式
- AI-consumedなResource一般のTaxonomy（分類体系）、Convention（規約）、およびSpecification（仕様）
- Task Procedure（タスク手順）およびSpecialized Capability（専門能力）のDefinition（定義）
- Skill・Subagent・Hook・Permission・Sandbox・CI・MCP等のMechanism（機構）
- Vendor固有のIntegration、およびそのAdapter
- `.github` 以外のRepositoryにおけるResolution（解決）の設置判断
- Resolution（解決）に対するValidation、Enforcement、およびTool要求

## Resolution Resource（解決資源）

### Concrete Representation（具体表現）

Cross-agent Entry（Agent横断入口）以降のResolution（解決）が前提とするConcrete Representation（具体表現）は、当該Repositoryの `.ai/foundation-resolution.md` である。

```text
Repository root
└─ .ai/
     └─ foundation-resolution.md
```

`.ai/` は、本Concrete Representation（具体表現）のPhysical Location（物理配置）である。本文書は `.ai/` に対して、Documentation Area（文書責務領域）その他のSemantic Responsibility（意味上の責務）を成立させない。

### Resource Responsibility（解決資源の責務）

`.ai/foundation-resolution.md` が成立させるのは次である。

```text
Foundation Provider内部に存在するAuthoritative Foundation Sourceについて、
それぞれが何を定義するSourceであり、
どのLocationに存在するのかを識別可能にする。
```

`.ai/foundation-resolution.md` が保持するのはResolution Information（解決情報）である。Resolution Information（解決情報）は、Effective Foundation State（有効基盤状態）およびTask Context（タスク文脈）とともにTask Relevance Resolution（タスク関連性解決）へ入力される。

`.ai/foundation-resolution.md` は、どのSourceがCurrent Task（現在タスク）にRelevantであるかを自ら確定させない。Relevanceの確定はTask Relevance Resolution（タスク関連性解決）が担う。

### Minimum Resolution Information（保持する最小の解決情報）

`.ai/foundation-resolution.md` は、掲載する各Authoritative Foundation Source（正式基盤Source）について、次の3つを識別可能にする。

| 保持する情報 | 成立させる内容 |
| --- | --- |
| Subject | どのSourceであるかの識別 |
| Responsibility（責務） | そのSourceが何を定義する責務を担うか |
| Source Location | そのSourceがProvider内部のどのLocationに存在するか |

Subjectは、当該SourceについてすでにDefinition Authority（定義権限）側で成立しているFormal Name（正式名称）によって識別する。本文書は、Entry Identifier（項目識別子）、Resource Type（資源種別）、Authority Flag等、これら3つ以外の要素を要求しない。

Responsibility（責務）として保持するのは、他のSourceとの区別に必要な範囲に限られる。当該SourceのDefinition（定義）内容の要約または複製ではない。

### Content Not Held（保持しない内容）

`.ai/foundation-resolution.md` は、次を保持しない。

- Architecture（アーキテクチャ）が定義するConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）
- Convention（規約）が定めるNormative Rule（規範的規則）
- Specification（仕様）が定めるConcrete Contract（具体契約）
- Task Procedure（タスク手順）
- Foundation Definition（基盤定義）
- Foundation Applicationの判断結果
- Task Relevance（タスク関連性）の判断結果
- 本文書が定めるContract（契約）自身の説明

`.ai/foundation-resolution.md` がこれらのSourceを参照する役割を持つことは、それらに対するDefinition Authority（定義権限）を成立させない。この境界は[AI Integration Architecture](../architecture/ai-integration.md)が定めるAuthoritative Documentation Boundary（正式文書の境界）による。

### Inclusion Criterion（掲載対象の判断基準）

`.ai/foundation-resolution.md` へ掲載するのは、AI Integration（AI連携）がFoundation Definition（基盤定義）を解決するとき、直接の参照対象となるAuthoritative Foundation Source（正式基盤Source）である。

掲載の可否は、この意味基準によって判断する。Asset Type（資産種別）は掲載の可否を決定しない。すなわち、Architecture Asset（アーキテクチャ資産）・Convention Asset（規約資産）・Specification Asset（仕様資産）・Concrete Declaration（具体宣言）を保持するAsset等の区別だけを根拠として、掲載対象から除外しない。

次は掲載対象ではない。

- Authoritative Foundation Source（正式基盤Source）の解決に必要でないSupporting Resource（補助資源）
- Repository内のFile一覧としての網羅

## AI-consumed Representation（AI読込としての表現）

本節が扱うのは、`.ai/foundation-resolution.md` に限られる。AI-consumedなResource一般については何も定めない。

### Consumption Characteristic（消費特性）

`.ai/foundation-resolution.md` はAI Integration Resource（AI連携資源）であり、その内容がAI Consumer（AI利用主体）のContext（文脈）へ直接投入されるAI-consumedなResourceである。

AI-consumedであることは、そのResourceのConsumption Characteristic（消費特性）である。新たなAsset Type（資産種別）またはDocumentation Area（文書責務領域）として扱わない。

### Context Minimization（文脈の最小化）

`.ai/foundation-resolution.md` は、「Minimum Resolution Information（保持する最小の解決情報）」が定める内容を成立させるために必要な範囲のみを保持する。

通常のAI利用において、本Resource（資源）はResolution（解決）に先立ってContext（文脈）へ投入され得る。Human-facingなDocumentation（文書）としての説明構造を保持することは、Resolution（解決）の成立に必要ではなく、Context Cost（文脈コスト）のみを増加させる。

### Convention Applicability（規約の適用範囲）

`.ai/foundation-resolution.md` がAI Integration Resource（AI連携資源）であることだけを根拠として、Current Documentation Convention（現在文書規約）を全面適用または全面除外しない。各Convention（規約）およびRule（規則）の適用は、そのApplicability（適用範囲）とCurrent Semantic Need（現在の意味上の必要性）から判断する。

現在維持するのは次である。

- Subjectとして使用するFormal Name（正式名称）についての、Definition Authority（定義権限）側で成立しているEnglish Representation（英語表現）
- Repository-controlled Nameとしての `.ai/foundation-resolution.md` のPhysical Name（物理名称）の形式

次は本Resource（資源）へ自動的には要求しない。

- Standard Section（標準Section）
- Human-facingなDocument Title（文書題名）のRepresentation（表現）
- Documentationとしての説明構造
- 同一のSemantic Content（意味内容）をEnglishとJapaneseで併記すること

### Language（言語）

`.ai/foundation-resolution.md` のCurrent Representation（現在表現）はJapanese onlyとする。

これはAI-consumed Resource Representation（AI読込資源の表現）についてのCurrent Decision（現在判断）であり、[Writing Convention](../conventions/writing.md)が定めるPrimary Language（主要言語）を適用した結果ではない。

## Path Composition（Pathの構成）

### Distinguished Elements（区別する要素）

次の3つは別の事柄である。

```text
Foundation Provider Identity
≠ Foundation ProviderのLocation
≠ Provider内部のSource Location
```

| 要素 | 何を示すか | 所有主体 |
| --- | --- | --- |
| Foundation Provider Identity | どのRepositoryがFoundation Provider（基盤提供主体）であるか | Foundation Provider（基盤提供主体） |
| Foundation ProviderのLocation | そのFoundation Provider（基盤提供主体）が、当該環境上のどこに存在するか | Consumer Repository（利用Repository） |
| Provider内部のSource Location | Foundation Provider（基盤提供主体）内部で、そのSourceがどこに存在するか | Foundation Provider（基盤提供主体） |

### Source Location Form（Source Locationの形式）

`.ai/foundation-resolution.md` が保持するSource Locationは、Foundation Provider（基盤提供主体）のRepository rootを基準とするRelative Path（相対Path）である。

`.ai/foundation-resolution.md` は、Foundation ProviderのLocationを保持しない。

### Composition（合成）

参照可能なLocationは、Foundation ProviderのLocationとProvider内部のSource Locationの合成として成立する。

```text
Foundation Provider Identity
= noxris42/.github

Foundation ProviderのLocation
= ../.github

Provider内部のSource Location
= docs/architecture/ai-integration.md

合成結果
= ../.github/docs/architecture/ai-integration.md
```

上記のFoundation ProviderのLocationは、合成の成立を示すための例示である。本文書は、Consumer Repository（利用Repository）におけるFoundation ProviderのLocationの値、およびその決定方式を定義しない。

`.github` 自身がConsumer Repository Role（利用Repository役割）を持つ場合、Foundation Provider（基盤提供主体）は当該Repository自身であり、Provider内部のSource LocationはRepository root相対Pathとしてそのまま解決される。

## Resolution Boundaries（解決の境界）

### Boundary with Task Relevance Resolution（タスク関連性解決との境界）

`.ai/foundation-resolution.md` への掲載は、そのSourceがCurrent Task（現在タスク）にRelevantであることを意味しない。

```text
listed in foundation-resolution.md
≠ relevant to Current Task
```

Task Relevance（タスク関連性）は、Task Context（タスク文脈）を前提としてTask Relevance Resolution（タスク関連性解決）が確定させる。`.ai/foundation-resolution.md` はその入力の一部を提供するのみであり、選択そのものを保持・決定しない。

### Boundary with Effective Foundation State（有効基盤状態との境界）

`.ai/foundation-resolution.md` への掲載は、そのSourceがConsumer Repository（利用Repository）へ適用されていることを意味しない。

```text
listed in foundation-resolution.md
≠ applied to Consumer Repository
```

Foundation Applicationを決定するのはConsumer Repository（利用Repository）であり、その結果としてEffective Foundation State（有効基盤状態）が成立する。`.ai/foundation-resolution.md` はEffective Foundation State（有効基盤状態）を保持せず、変更せず、代替しない。

### Boundary with Definition Authority（定義権限との境界）

`.ai/foundation-resolution.md` は、掲載するSourceに対するDefinition Authority（定義権限）を持たない。

```text
Definition Authority
≠ Foundation Application
≠ Task Relevance
```

掲載されたResponsibility（責務）の記述と、当該SourceのDefinition（定義）とが一致しない場合、成立している内容は当該Source側である。

## Provider / Consumer Repository Responsibility（基盤提供主体・利用Repositoryの責務）

### Foundation Provider Responsibility（基盤提供主体の責務）

Foundation Provider（基盤提供主体）は、自身の内部に存在するAuthoritative Foundation Source（正式基盤Source）についてのResolution Information（解決情報）を所有する。

`.github` におけるその保持先が `.ai/foundation-resolution.md` である。

### Consumer Repository Responsibility（利用Repositoryの責務）

Consumer Repository（利用Repository）は、Foundation ProviderのLocationとRepository-specific State（Repository固有状態）を所有する。

Foundation Provider（基盤提供主体）が所有するResolution Information（解決情報）を、Consumer Repository（利用Repository）側へ複製しない。複製は、Definition（定義）の所在とResolution Information（解決情報）の所在を分岐させ、Foundation Provider（基盤提供主体）側の変更が反映されない状態を生じさせる。

## Entry / Resolution Relationship（入口と解決の関係）

[Cross-agent Entry Specification](cross-agent-entry.md)が定めるとおり、Entry（入口）の成立とResolution（解決）の成立は別のResponsibility（責務）である。本文書は、そのうちResolution（解決）側を担う。

Cross-agent Entry（Agent横断入口）から成立する経路は次である。

```text
AGENTS.md
→ .ai/foundation-resolution.md
→ RelevantなAuthoritative Foundation Source
```

Cross-agent Entry（Agent横断入口）が保持するのは、本Concrete Representation（具体表現）への参照までである。Resolution Information（解決情報）そのものをEntry（入口）へ複製しない。

`.github` において、Cross-agent Entry（Agent横断入口）が参照するのは同一Repository内の `.ai/foundation-resolution.md` である。

## Deferred to Downstream Design（後続設計へ委譲する事項）

本文書は次を定義しない。ここで示す事項は、本文書の現在の責務に基づいて、意図的に定義・解決の対象外としている事項である。

- Foundation Provider（基盤提供主体）をRemote Locationとして解決する方式。
- Effective Foundation State（有効基盤状態）のConcrete Representation（具体表現）。→ Foundation Application State Designへ委譲する。
- Consumer Repository（利用Repository）におけるFoundation ProviderのLocationの決定方式。→ 当該RepositoryへのFoundation Applicationへ委譲する。
- Vendor固有のResource（資源）およびAdapter。→ Vendor-specific Integrationへ委譲する。

これらが未確定であることは、本文書のDesign Gap（設計上の不足）ではない。
