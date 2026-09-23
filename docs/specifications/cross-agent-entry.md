# Cross-agent Entry Specification（Agent横断入口仕様）

## Purpose（目的）

本文書は、`noxris42` において**AI Integration（AI連携）のBootstrap Responsibility（初期接続責務）を成立させるCross-agent Entry（Agent横断入口）について、そのConcrete Contract（具体契約）を定義する**Specification Asset（仕様資産）である。

本文書が扱う問いは次の6点である。

1. Cross-agent Entry（Agent横断入口）は、どのConcrete Representation（具体表現）として成立するのか。
2. そのEntry（入口）は、Entry Responsibility（入口責務）として何を成立させ、何を成立させないのか。
3. そのConcrete Representation（具体表現）は、AI Consumer（AI利用主体）のContext（文脈）へ直接投入されるResourceとして、何を保持するのか。
4. Vendor-specific Entry（Vendor固有入口）は、どのように扱われるのか。
5. Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）において、Entry（入口）はどの関係で成立するのか。
6. Entry（入口）の成立と、Navigation / Resolution（Navigation／解決）の成立との境界はどこにあるのか。

本文書が定義するのは、この6点に対するConcrete Contract（具体契約）に限られる。本文書は、AI Integration（AI連携）のSemantic / Structural Modelを定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するSpecifications Area（仕様領域）に属する通常のDocumentation Asset（文書資産）である。AI Integration（AI連携）という特定Subjectについて、そのBootstrap Responsibility（初期接続責務）を成立・実現可能にするConcrete Contract（具体契約）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約）についてのDefinition Authority（定義権限）は本文書が持つ。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は上位設計にある。本文書はこれらを参照するのみで、再定義・上書きしない。

- AI Integration（AI連携）の意味、そのCore Responsibility（中核責務）およびBoundary Responsibility（境界責務）
- Bootstrap Responsibility（初期接続責務）およびDelivery Adaptation Responsibility（提供適応責務）
- AI Consumer（AI利用主体）、Foundation Definition（基盤定義）、Authoritative Source（正式Source）、Authoritative Foundation Definition（正式基盤定義）
- Effective Foundation State（有効基盤状態）、Task Context（タスク文脈）、Task Relevance（タスク関連性）
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）
- Resolution（解決）・Reference（参照）がDefinition Authority（定義権限）を成立させないこと
- Shared Development Foundation、Shared Foundation Asset、Ownership（所有責任）、Foundation Application
- Documentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件、およびArea Responsibility（領域責務）

したがって次は本文書の責務ではない。

- AI Integration（AI連携）が成立させる責務体系そのもの。→ [AI Integration Architecture](../architecture/ai-integration.md)による。
- あるShared Foundation Assetが特定Repositoryで有効になる関係、およびその判断。→ [Repository Governance](../architecture/repository-governance.md)のFoundation Applicationによる。
- Documentation Asset（文書資産）にDefinition Authority（定義権限）が成立する条件。→ [Documentation Structure Architecture](../architecture/documentation-structure.md)による。

本文書が定めるのは、これらによってすでに成立しているModelを前提として、Bootstrap Responsibility（初期接続責務）をRepository上でどのConcrete Representation（具体表現）として成立させるかである。

### Position（設計上の位置づけ）

本文書は[AI Integration Architecture](../architecture/ai-integration.md)を上位Sourceとして参照する。

同文書は、Bootstrap Responsibility（初期接続責務）をBoundary Responsibility（境界責務）として定義する一方、それを担うConcrete Representation（具体表現）を意図的に定義せず、Cross-agent Entry Designを後続設計へ委譲している。本文書は、その委譲先として、Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約）を定義する。

Design Dependency（設計依存）は次の一方向とする。

```text
AI Integration Architecture
        ▲
        │ refines
Cross-agent Entry Specification
```

本文書は、上位Architecture（アーキテクチャ）の意味を変更・補完しない。本文書が定めるConcrete Contract（具体契約）から、上位のConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）を導出・上書きしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Cross-agent Entry（Agent横断入口）の成立と、そのConcrete Representation（具体表現）
- Cross-agent Entry（Agent横断入口）のEntry Responsibility（入口責務）
- Cross-agent Entry（Agent横断入口）が保持しない権限および内容
- Cross-agent Entry（Agent横断入口）のConcrete Representation（具体表現）が、AI-consumedなResourceとして保持する内容の境界
- 同Concrete Representation（具体表現）のCurrent Language Decision（現在の言語判断）、およびConvention（規約）の適用判断
- Vendor-specific Entry（Vendor固有入口）の扱いと、その再評価が成立する条件
- Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）におけるEntry（入口）の関係
- Entry（入口）の成立とNavigation / Resolution（Navigation／解決）の成立のBoundary（境界）

### Out of Scope（本文書が定義しない範囲）

- AI Integration（AI連携）のCore Responsibility（中核責務）、およびそれを構成するConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）
- Navigation / Resolution（Navigation／解決）のConcrete Mechanism（具体機構）、next-hopのDefinition（定義）、およびそのConcrete Representation（具体表現）
- AI-consumedなResource一般のTaxonomy（分類体系）、Convention（規約）、およびSpecification（仕様）
- Repository Documentation（Repository文書）全般に対する一般のLanguage Decision（言語判断）
- Effective Foundation State（有効基盤状態）の生成方式、Schema、Manifest等のConcrete Representation（具体表現）
- Foundation Applicationの判断、およびその適用方式
- Task Procedure（タスク手順）およびSpecialized Capability（専門能力）のDefinition（定義）
- Skill・Subagent・Hook・Permission・Sandbox・CI・MCP等のMechanism（機構）
- Vendor固有のIntegration、およびそのAdapter
- `.github` 以外のRepositoryにおけるEntry（入口）のConcrete Representation（具体表現）、およびその設置判断
- Entry（入口）に対するValidation、Enforcement、およびTool要求

## Cross-agent Entry（Agent横断入口）

### Cross-agent Entry Definition（Agent横断入口の定義）

Cross-agent Entry（Agent横断入口）は、あるRepositoryにおいて、AI Consumer（AI利用主体）がAI Integration（AI連携）の利用を開始する地点として成立する単一のRepresentation（表現）である。

Cross-agent Entry（Agent横断入口）は、[AI Integration Architecture](../architecture/ai-integration.md)が定義するBootstrap Responsibility（初期接続責務）を、当該Repository上で成立させる。

### Concrete Representation（具体表現）

Cross-agent Entry（Agent横断入口）のConcrete Representation（具体表現）は、当該Repository rootの `AGENTS.md` である。

```text
Repository root
└─ AGENTS.md
     = Cross-agent Entry
```

現在のAI Consumer（AI利用主体）である次の3つは、いずれもこのRepresentation（表現）を共通の開始地点として利用する。

```text
Claude Code
Codex
Antigravity
```

この選択は、Concrete AI Consumer（具体AI利用主体）がRepositoryから利用を開始できる形を成立させるためのものであり、AI Integration（AI連携）のSemantic Model（意味モデル）をConcrete Product（具体Product）から導出するものではない。[AI Integration Architecture](../architecture/ai-integration.md)が定めるVendor Independence（Vendor非依存）は、本Concrete Contract（具体契約）によって変更されない。

### Single Entry（単一の入口）

あるRepositoryにおいて、Cross-agent Entry（Agent横断入口）は1つだけ成立する。

同一Repository内へ、Cross-agent Entry（Agent横断入口）として機能する別のRepresentation（表現）を並置しない。

### Physical Name Handling（物理名称の扱い）

`AGENTS.md` は、Concrete AI Consumer（具体AI利用主体）側がConcrete Spelling（具体表記）を認識の条件とするExternally Constrained Name（外部制約名称）である。したがって、その綴りは[Naming Convention](../conventions/naming.md)が定めるExternal Naming Contract（外部命名契約）へ適合する形で保持する。Repository-controlled Nameに対するPhysical Naming Formを根拠として、この綴りを変更しない。

## Entry Responsibility（入口責務）

### Established Responsibility（成立させる責務）

Cross-agent Entry（Agent横断入口）が成立させるのは次である。

```text
当該Repositoryにおいて、
AI ConsumerがAI Integrationの利用を開始する地点を成立させる。
```

Entry Responsibility（入口責務）はこれに限られる。Entry（入口）以降の接続先、およびそこへの到達方法の成立は、Entry Responsibility（入口責務）に含まれない。

### Content Not Held（保持しない内容）

Cross-agent Entry（Agent横断入口）は、次をEntry（入口）へ複製しない。

- Architecture（アーキテクチャ）が定義するConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）
- Convention（規約）が定めるNormative Rule（規範的規則）
- Task Procedure（タスク手順）
- Foundation Definition（基盤定義）

Entry（入口）がこれらを参照する役割を持つことは、それらに対するDefinition Authority（定義権限）を成立させない。この境界は[AI Integration Architecture](../architecture/ai-integration.md)が定めるAuthoritative Documentation Boundary（正式文書の境界）による。

本項が定めるのは、Entry（入口）が保持する内容に対する境界である。Entry（入口）自身へ、この境界の説明を保持することを要求しない。

### Vendor-neutral Content（Vendor中立な内容）

Cross-agent Entry（Agent横断入口）は、特定のConcrete AI Consumer（具体AI利用主体）だけへ向けたInstruction（指示）を保持しない。

Vendor固有の必要性は、Entry（入口）の内容としてではなく、Delivery Adaptation Responsibility（提供適応責務）として扱う。

## AI-consumed Representation（AI読込としての表現）

本節が扱うのは、Cross-agent Entry（Agent横断入口）のConcrete Representation（具体表現）である `AGENTS.md` に限られる。AI-consumedなResource一般については何も定めない。

### Consumption Characteristic（消費特性）

`AGENTS.md` はAI Integration Resource（AI連携資源）であり、その内容がAI Consumer（AI利用主体）のContext（文脈）へ直接投入されるAI-consumedなResourceである。

AI-consumedであることは、そのResourceのConsumption Characteristic（消費特性）である。新たなAsset Type（資産種別）またはDocumentation Area（文書責務領域）として扱わない。

### Minimum Semantic Content（最小意味内容）

`AGENTS.md` は、Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約）を成立させるために必要な最小Semantic Content（最小意味内容）のみを保持する。

他のAuthoritative Source（正式Source）または後続Resourceが所有する説明・定義・Navigationを、Persistent Context（永続文脈）へ複製しない。利便性のみを根拠とする複製は、保持の根拠として成立しない。

本項は分量に関するRule（規則）を定めない。Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約）の成立に必要なSemantic Content（意味内容）は削らない。

### Language（言語）

`AGENTS.md` のCurrent Representation（現在表現）はJapanese onlyとする。

これはAI-consumed Resource Representation（AI読込資源の表現）についてのCurrent Decision（現在判断）であり、[Writing Convention](../conventions/writing.md)が定めるPrimary Language（主要言語）を適用した結果ではない。

同一のSemantic Content（意味内容）をEnglishとJapaneseで併記しない。

English onlyへ固定する根拠は現在不足している。必要性または実証結果が得られた場合に再評価する。

### Convention Applicability（規約の適用範囲）

`AGENTS.md` がAI Integration Resource（AI連携資源）であることだけを根拠として、Current Documentation Convention（現在文書規約）を全面適用または全面除外しない。各Convention（規約）およびRule（規則）の適用は、そのApplicability（適用範囲）とCurrent Semantic Need（現在の意味上の必要性）から判断する。

現在維持するのは次である。

- `AGENTS.md` というPhysical Name（物理名称）に対するExternal Naming Contract（外部命名契約）

次は`AGENTS.md` へ自動的には要求しない。

- [Writing Convention](../conventions/writing.md)に由来する日英併記
- Standard Section（標準Section）
- Human-facingなDocument Title（文書題名）のRepresentation（表現）
- Documentationとしての説明構造

Repository内にMarkdown Fileとして存在することだけを根拠として、[Markdown Convention](../conventions/markdown.md)を全面適用しない。

## Vendor-specific Entry（Vendor固有入口）

### Handling（扱い）

`CLAUDE.md` ・ `GEMINI.md` その他のVendor-specific Entry（Vendor固有入口）は、常設しない。

### Reevaluation Condition（再評価が成立する条件）

Vendor-specific Entry（Vendor固有入口）は、Cross-agent Entry（Agent横断入口）では満たせないCurrent Semantic Need（現在の意味上の必要性）が実際に発生した場合に限り、Delivery Adaptation Responsibility（提供適応責務）として再評価する。

次はいずれも、Vendor-specific Entry（Vendor固有入口）を導入する根拠として成立しない。

- Compatibility（互換性）
- 将来発生し得る必要性

この扱いは、[Repository Governance](../architecture/repository-governance.md)が定めるSemantic Need over Reusability（再利用性ではなく意味上の必要性）の適用結果であり、新たな判断原則を導入するものではない。

## Provider / Consumer Repository Relationship（基盤提供主体・利用Repositoryにおける関係）

### `.github` Entry Handling（`.github`のEntryの扱い）

`.github` Repository rootの `AGENTS.md` は、`.github` Repository自身のCross-agent Entry（Agent横断入口）である。

```text
.github/AGENTS.md
= .github Repository自身のBootstrap Entry
```

`.github/AGENTS.md` は、他Repositoryの親Entry（入口）でも中央Entry（入口）でもない。

### Entry Responsibility Is Not Transferred（入口責務を引き受けない）

`.github` がShared Development FoundationのProvider（提供主体）であることは、他のConsumer Repository（利用Repository）のEntry Responsibility（入口責務）を`.github` が引き受けることを意味しない。

各Consumer Repository（利用Repository）におけるEntry（入口）は、そのRepository自身において成立する。そのRepositoryへ本Specification（仕様）を適用するかどうかは、[Repository Governance](../architecture/repository-governance.md)が定めるFoundation Applicationの判断に属し、本文書はこれを決定しない。

## Entry / Navigation Boundary（入口とNavigationの境界）

Entry（入口）の成立と、Entry（入口）以降の接続先・到達方法の成立は、別のResponsibility（責務）である。

```text
Entry
= AI Integrationの利用開始地点を成立させる

Navigation / Resolution
= Entry以降の接続先・Routing・Relevant / Authoritative Sourceへの到達を成立させる
```

したがって次が成立する。

```text
Cross-agent Entryの成立
≠
Navigation / Resolutionの成立
```

Cross-agent Entry（Agent横断入口）が成立するために、次の接続先が定義済みであることを要求しない。本文書は、具体的なnext-hopの内容を定義しない。

現在正式に成立している状態は次である。

```text
AGENTS.md
= Cross-agent Entry

Authoritative Foundation Resolution
→ .ai/foundation-resolution.md

Repository-level understanding / exploration
→ README.md
```

各Routeは、それぞれ必要な場合にのみ利用を開始する条件付きのnext-hopである。Entry（入口）は、いずれかのRoute先の常時読込を要求しない。

Authoritative Foundation Resolution（正式基盤解決）へのnext-hopのDefinition（定義）は[AI Context Resolution Specification](ai-context-resolution.md)が持つ。Repository-level understanding / explorationのRoute先が担うResponsibility（責務）は[Repository Orientation / Navigation Architecture](../architecture/repository-orientation-navigation.md)による。後者のRouteは、既存のHuman-facingなResource（資源）をAI Consumer（AI利用主体）へ接続するDelivery Adaptation（提供適応）である。本文書が扱うのは、Entry（入口）がこれらのRoute先を参照することまでであり、Navigation / Resolution（Navigation／解決）の内容は本文書の責務ではない。

RouteをEntry（入口）が保持することは、Entry Responsibility（入口責務）を拡張せず、Route先のResponsibility（責務）を所有することも、Route先が保持する内容に対するDefinition Authority（定義権限）を成立させることもない。

```text
RouteをAGENTS.mdが保持する
≠
Entry ResponsibilityがそのRoute先のResponsibilityを所有する
```

## Deferred to Downstream Design（後続設計へ委譲する事項）

本文書は次を定義しない。ここで示す事項は、本文書の現在の責務に基づいて、意図的に定義・解決の対象外としている事項である。

- Authoritative Foundation Resolution（正式基盤解決）へのnext-hopのDefinition（定義）、Resolution Mechanism（解決機構）の設計、およびそのConcrete Representation（具体表現）。→ [AI Context Resolution Specification](ai-context-resolution.md)へ委譲する。
- Effective Foundation State（有効基盤状態）のConcrete Representation（具体表現）。→ Foundation Application State Designへ委譲する。
- Vendor-specific Entry（Vendor固有入口）が必要となった場合のConcrete Representation（具体表現）。→ Vendor-specific Integrationへ委譲する。
- `.github` 以外のRepositoryにおけるEntry（入口）の設置。→ 当該RepositoryへのFoundation Applicationへ委譲する。

これらが未確定であることは、本文書のDesign Gap（設計上の不足）ではない。
