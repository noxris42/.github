# Shared Development Foundation（共通開発基盤）

## Purpose（目的）

`noxris42/.github` は、複数Repositoryに共通する開発上の責務を一元的に所有・維持し、Shared Development Foundation（共通開発基盤）として他Repositoryが適用可能な形で提供するRepositoryである。

本READMEは、Repositoryの主要構造、現在Version管理されているFile、および目的に応じた探索開始地点を示す。Concept（概念）・Rule（規則）・Contract（契約）の正式なDefinition（定義）は、それぞれを定義する正式文書が保持する。本READMEはそれらを要約・案内するのみで、再定義しない。

Repository間のOwnership（所有責任）、Shared Scope、およびFoundation Application（共通開発基盤資産の適用関係）については、[Repository Governance（Repository間の統治・責務）](docs/architecture/repository-governance.md)を参照する。

## Repository Structure（Repository構造）

```text
.
├─ README.md
├─ AGENTS.md
├─ .ai/
│  └─ foundation-resolution.md
└─ docs/
   ├─ architecture/
   ├─ conventions/
   ├─ specifications/
   └─ canonical-primary-language-support.yaml
```

上図は、Repository全体を俯瞰するために主要なFileとDirectoryを選んで示したPhysical Structure（物理構造）であり、すべてのFileを示すものではない。Directoryの配置は、Documentation Area（文書責務領域）その他のLogical Structure（論理構造）を定義しない。現在Version管理されているすべてのFileは「Resources」に示す。

## Resources（資源）

本節は、現在Version管理されているすべてのFileを示す。

以下のGroupは、本README上で探索しやすくするための表示上のまとまりであり、Resourceの分類体系を定義しない。各Resourceの説明は識別・探索のための要約であり、正式な内容は各Resource自身が保持する。

### Repository Orientation / Navigation（Repository方向付け／探索）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| Shared Development Foundation（共通開発基盤） | `README.md` | Repository全体のRepository Orientation / Navigation（Repository方向付け／探索）を現在具体化する入口 |

### AI Integration（AI連携）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| [Cross-agent Entry](AGENTS.md) | `AGENTS.md` | AI Consumer（AI利用主体）がAI Integration（AI連携）へ入るCross-agent Entry（Agent横断入口） |
| [Foundation Resolution](.ai/foundation-resolution.md) | `.ai/foundation-resolution.md` | Current TaskにRelevantなAuthoritative Foundation Source（正式基盤Source）を解決するための解決情報 |

### Architecture（アーキテクチャ）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| [Repository Governance（Repository間の統治・責務）](docs/architecture/repository-governance.md) | `docs/architecture/repository-governance.md` | Repository間のOwnership Boundary（所有責任の境界）と、Shared Development Foundationの適用関係を定義する最上位Model |
| [Documentation Structure Architecture（文書構造アーキテクチャ）](docs/architecture/documentation-structure.md) | `docs/architecture/documentation-structure.md` | Documentation Structure（文書構造）を成立させる論理単位・責務・Logical / Physical Boundaryの一般Model |
| [Repository Governance Documentation Framework（Repository統治文書体系）](docs/architecture/repository-governance-documentation-framework.md) | `docs/architecture/repository-governance-documentation-framework.md` | 現在採用するDocumentation Framework（文書体系）と、各Documentation Area（文書責務領域）のArea Responsibility（領域責務） |
| [Convention Architecture（規約アーキテクチャ）](docs/architecture/convention.md) | `docs/architecture/convention.md` | Convention（規約）の意味と責務、およびその内部でRuleが持つSemantic Structure（意味構造） |
| [Canonical Primary Language Support Architecture（正規主要言語補助アーキテクチャ）](docs/architecture/canonical-primary-language-support.md) | `docs/architecture/canonical-primary-language-support.md` | English Representation（英語表現）とPrimary Language Representation（主要言語表現）の対応が成立するSemantic Model（意味モデル） |
| [AI Integration Architecture（AI連携アーキテクチャ）](docs/architecture/ai-integration.md) | `docs/architecture/ai-integration.md` | AI Integration（AI連携）が成立させる責務体系と、関係する主体間のResponsibility Relationship（責務関係） |
| [Repository Orientation / Navigation Architecture（Repository方向付け／探索アーキテクチャ）](docs/architecture/repository-orientation-navigation.md) | `docs/architecture/repository-orientation-navigation.md` | Repository Orientation / Navigation（Repository方向付け／探索）のSemantic / Structural ModelとResponsibility Boundary（責務境界） |

### Conventions（規約）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| [Canonical Primary Language Support Convention（正規主要言語補助規約）](docs/conventions/canonical-primary-language-support.md) | `docs/conventions/canonical-primary-language-support.md` | Canonical Primary Language Support Association（正規主要言語補助対応）のCandidate Recommendation（候補提案）とCanonical Declaration（正規宣言）の扱い |
| [Commit Convention（コミット規約）](docs/conventions/commit.md) | `docs/conventions/commit.md` | Commitの意味単位と、Commit Messageの記述 |
| [Convention Authoring Convention（規約記述規約）](docs/conventions/convention-authoring.md) | `docs/conventions/convention-authoring.md` | Convention（規約）そのものの記述方法 |
| [Documentation Structure Convention（文書構造規約）](docs/conventions/documentation-structure.md) | `docs/conventions/documentation-structure.md` | 文書のSection構成、Standard Section（標準Section）の機構、およびDocumentation全体に適用されるStandard Section（標準Section） |
| [Markdown Convention（Markdown規約）](docs/conventions/markdown.md) | `docs/conventions/markdown.md` | Markdown上のSyntaxおよびMarkupによる表現 |
| [Naming Convention（命名規約）](docs/conventions/naming.md) | `docs/conventions/naming.md` | File名・Directory名・Path等のPhysical Name（物理名称）の形式と選択 |
| [Repository Governance Documentation Structure Convention（Repository統治文書構造規約）](docs/conventions/repository-governance-documentation-structure.md) | `docs/conventions/repository-governance-documentation-structure.md` | Repository Governance Documentation Frameworkに固有のStandard Section（標準Section） |
| [Writing Convention（文章規約）](docs/conventions/writing.md) | `docs/conventions/writing.md` | Repository Documentation（Repository文書）の自然言語による文章表現 |

### Specifications（仕様）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| [Cross-agent Entry Specification（Agent横断入口仕様）](docs/specifications/cross-agent-entry.md) | `docs/specifications/cross-agent-entry.md` | Cross-agent Entry（Agent横断入口）のConcrete Contract（具体契約） |
| [AI Context Resolution Specification（AI文脈解決仕様）](docs/specifications/ai-context-resolution.md) | `docs/specifications/ai-context-resolution.md` | Cross-agent Entry（Agent横断入口）以降、RelevantなAuthoritative Foundation Source（正式基盤Source）を解決するConcrete Contract（具体契約） |

### Supporting Declaration（補助宣言）

| Resource | Location | Responsibility（責務） |
| --- | --- | --- |
| [Canonical Primary Language Support Registry](docs/canonical-primary-language-support.yaml) | `docs/canonical-primary-language-support.yaml` | Canonical Primary Language Support Association（正規主要言語補助対応）の具体値を保持するCentral Concrete Declaration Source（中央具体宣言情報源） |

## Exploration Guidance（探索案内）

代表的な目的から、探索開始地点を示す。すべての目的またはFileへの経路は示さない。個々のFileは「Resources」から探索する。

| 知りたいこと | 探索開始地点 |
| --- | --- |
| Repositoryの役割、Ownership（所有責任）、Shared Development Foundation（共通開発基盤）の位置づけ | [Repository Governance（Repository間の統治・責務）](docs/architecture/repository-governance.md) |
| Documentationの論理単位・責務・Logical / Physical Boundary | [Documentation Structure Architecture（文書構造アーキテクチャ）](docs/architecture/documentation-structure.md) |
| 現在のDocumentation Framework（文書体系）とArea Composition | [Repository Governance Documentation Framework（Repository統治文書体系）](docs/architecture/repository-governance-documentation-framework.md) |
| Repository Orientation / Navigation（Repository方向付け／探索）が成立するModel | [Repository Orientation / Navigation Architecture（Repository方向付け／探索アーキテクチャ）](docs/architecture/repository-orientation-navigation.md) |
| Convention（規約）とNormative Rule（規範的規則）の意味 | [Convention Architecture（規約アーキテクチャ）](docs/architecture/convention.md) |
| 適用する具体的なRule | 「Resources」のConventions（規約） |
| AI Integration（AI連携）の責務とConcrete Contract（具体契約） | [AI Integration Architecture（AI連携アーキテクチャ）](docs/architecture/ai-integration.md)から、「Resources」のSpecifications（仕様） |
