# Repository Governance Architecture（Repository間の統治・責務Architecture）

## Purpose（目的）

本文書は、`noxris42` Organization配下の複数Repositoryにおける
**Ownership Boundary（所有責任の境界）** と、
**Shared Development Foundation（複数Repositoryで共有する開発基盤）** を
各Repositoryへ適用するための最上位Modelを定義する。

本文書が扱う問いは次の3点である。

1. ある定義・資産（Asset）を **誰が所有するのか（Ownership／所有責任）**。
2. Shared Development Foundation（複数Repositoryで共有する開発基盤）に
   **何を含めてよいのか（Shared Scope／共有範囲）**。
3. 共有された定義・資産が、どのようにして特定Repositoryで
   **有効になるのか（Foundation Application／共通開発基盤を対象Repositoryへ適用する関係）**。

本文書は上位Architectureとして自己完結する。
後続設計（具体的なConvention体系、Application Mechanism、Metadata Schema等）の
存在や内容を前提としない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- `noxris42/.github` Repositoryと個別Repositoryの間の責務関係
- Shared Development Foundation（複数Repositoryで共有する開発基盤）の位置づけ
- Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）と
  Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）の区別
- Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）の概念
- 共有基盤へ含めるか否かの判断原則（Shared Scope Principles／共有範囲の判断原則）
- `.github` 自身への適用（Self Application／`.github`自身への適用）

### Out of Scope（本文書が定義しない範囲）

- 個別RepositoryのDomain Model（題材領域のモデル）および
  System Architecture（システム構造）
- Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）の
  具体的なAsset Type（資産種別）の確定
- Application Mechanism（適用方式）の具体実装
- Documentation階層・Directory構造の正式確定
- Metadata（構造化メタデータ）やDeclaration（明示的宣言）の具体Schema

詳細は「Non-goals / Delegation（今回扱わず後続へ委譲する事項）」に示す。

## Concept Model（概念モデル）

### Repository（Repository）

Governance（統治・責務管理）の単位となる、独立したVersion管理境界。
各Repositoryは自身のDomain（題材領域）・System（システム構造）・
Repository-specific concern（個別Repository固有の関心事）を持つ。

`.github` も1つのRepositoryであり、この定義の例外ではない。

### Shared Development Foundation（複数Repositoryで共有する開発基盤）

複数Repositoryに共通する **開発上の責務** を、一元的に所有・維持するための基盤。
`noxris42/.github` はこのShared Development Foundation
（複数Repositoryで共有する開発基盤）を所有する。

重要な限定として、Shared Development Foundation（複数Repositoryで共有する開発基盤）は
**開発上の共通責務** を対象とする基盤であり、
各RepositoryのDomain（題材領域）やSystem Architecture（システム構造）を対象としない。

### Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）

Shared Development Foundation（複数Repositoryで共有する開発基盤）に属し、
複数Repository向けの共通内容を持つ定義または資産。

本文書では、Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）が
具体的にどのようなAsset Type（資産種別）を取るかを固定しない。
Asset Type（資産種別）は、実際のSemantic Need（意味上の必要性）が
生じた時点で個別に決定する。

### Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）

特定Repositoryが、自身のDomain（題材領域）・System（システム構造）・
Development（開発運用）上の必要から、内容を決定し所有する定義または資産。

Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）に
ついて、そのAssetが扱うRepository固有の内容の
最終的なDefinition Responsibility（定義責任）は、対象Repositoryが持つ。

ここでいうOwnership（所有責任）は、
**その内容を決定する責務が誰にあるか** を意味する。
Constraint-free（外部の共有規則から一切制約されないこと）を意味しない。
Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）で
あっても、Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
として適用されたConvention（規約）等から制約を受けることはあり得る。
制約の下で固有内容を決定する責務が対象Repositoryにあることと、
外部からの制約が存在しないこととは別の事柄である。

### Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）

Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）を、
特定Repositoryにおいて利用可能・有効な状態にする **関係** 。

Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）は
関係そのものであり、その実現手段
（Application Mechanism／適用方式）とは区別される。

### Concept間の関係

```text
Shared Development Foundation（複数Repositoryで共有する開発基盤）
  │
  └─ owns ─▶ Shared Foundation Asset
             （共通開発基盤が所有する共有定義・共有資産）
                  │
                  └─ Foundation Application
                     （共通開発基盤を対象Repositoryへ適用する関係）
                          │
                          ▼
                     Repository（適用先Repository）
                          │
                          └─ owns ─▶ Repository-owned Asset
                                     （対象Repository自身が内容を
                                       決定・所有する定義・資産）
```

Owner（所有者）はShared Development Foundation（複数Repositoryで共有する開発基盤）側にあり、
どのShared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）を
自身へ適用するかの判断は、適用先Repository側にある。

## Responsibility Model（責務モデル）

### `.github` Repositoryの責務

`.github` は次の責務を持つ。

- Shared Development Foundation（複数Repositoryで共有する開発基盤）の
  Owner（所有者）として、
  Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）の
  **内容** を決定・維持する。
- Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）を、
  他Repositoryが適用可能な形でProvider（提供者）として提供する。
- 何がShared Development Foundation（複数Repositoryで共有する開発基盤）に
  属するか／属さないかを判断する。

`.github` は次の責務を **持たない** 。

- 他RepositoryのDomain Model（題材領域のモデル）を所有すること。
- 他RepositoryのSystem Architecture（システム構造）を所有・中央管理すること。
- 他Repositoryに対して、
  特定のShared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）の
  適用を機械的に決定すること。

### 個別Repositoryの責務

個別Repositoryは次の責務を持つ。

- 自身のDomain（題材領域）・System（システム構造）・
  Repository-specific concern（個別Repository固有の関心事）に関する
  Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）
  を所有する。
- どのShared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）を
  自身へ適用するかを判断する
  （Foundation Application／共通開発基盤を対象Repositoryへ適用する関係の決定）。
- 適用した結果として自Repositoryが満たすべき状態に責任を持つ。

個別Repositoryは、適用したからといって
Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
**そのもの** を所有することにはならない。
Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）そのものの
内容に対する変更要求は、
Shared Development Foundation（複数Repositoryで共有する開発基盤）の
Owner（所有者）である `.github` 側の判断を経る。

### Repository Autonomy（各Repositoryが自身の責務を保持する）

Shared Development Foundation（複数Repositoryで共有する開発基盤）が存在しても、
各Repositoryは自身のDomain（題材領域）・System（システム構造）・
Repository-specific concern（個別Repository固有の関心事）について
Ownership（所有責任）を保持する。

`.github` は他Repositoryの **上位Repository** ではない。
`.github` は **共有Subject（共有対象）のOwner（所有者）** であり、
その権限範囲はShared Development Foundation（複数Repositoryで共有する開発基盤）に
属する事項に限定される。

## Ownership Boundary（所有責任の境界）

### 境界はResponsibility（責務）で決まる

Ownership（所有責任）は、
**Physical Location（物理配置）から決定しない** 。

すなわち、次の推論は成立しない。

- 「あるRepositoryのFile Tree上に存在するから、そのRepositoryが所有する」
- 「`.github` に存在するから、
  Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）である」

Ownership（所有責任）は、
**その定義・資産の内容を決定し維持する責務が誰にあるか** によって決まる。

### 判定の基準

| 観点 | Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産） | Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産） |
| --- | --- | --- |
| 内容を決定する主体 | Shared Development Foundation（複数Repositoryで共有する開発基盤）＝`.github` | 当該Repository |
| 対象とする関心事 | 複数Repositoryに共通する開発上の責務 | Domain（題材領域）／System（システム構造）／Repository-specific concern（個別Repository固有の関心事） |
| 内容の影響範囲 | 複数Repositoryへ共有される内容であり、適用先Repositoryへ影響し得る | 原則として当該Repository固有 |
| Physical Location（物理配置） | 判定基準ではない | 判定基準ではない |

### 適用済みAssetの扱い

あるRepositoryのFile Tree上に、
Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）の結果として
Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）由来の内容が
存在し得る。

この状況について、本文書は次までを定義する。

- Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
  **そのもの** のOwnership（所有責任）は `.github` 側にある。
- ある内容がRepository-localに存在するという事実だけでは、
  Ownership（所有責任）は移転しない。
  **存在すること（Presence／物理的な存在）** と
  **所有すること（Ownership／所有責任）** は別の事柄である。
- Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）によって
  新たにRepository-localなAsset（資産）が成立する場合、
  そのAssetのOwnership（所有責任）を
  **本文書では一律に決定しない** 。

適用の結果として成立したAsset（資産）のOwnership（所有責任）は、
用いられたApplication Mechanism（適用方式）と、
そのAssetが何を決定する責務を持つかに応じて、後続設計で決定する。
したがって、適用の結果として成立したAsset（資産）が
Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）
となる可能性を、本文書は妨げない。

## Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）

### Applicationとは何か

Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）とは、
Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）を、
特定Repositoryにおいて利用可能・有効にする関係である。

この関係は次を含意する。

- 適用元：Shared Development Foundation（複数Repositoryで共有する開発基盤）が
  所有するShared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
- 適用先：特定のRepository
- 適用の判断主体：適用先Repository

### OwnershipとApplicationの分離

Ownership（所有責任）とApplication（適用）は独立した概念であり、
混同してはならない。

- **Ownership（所有責任）**：内容を誰が決定・維持するか。
- **Application（適用）**：その内容が、どのRepositoryで有効になっているか。

したがって次が成立する。

- Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）が存在しても、
  あるRepositoryに適用されているとは限らない。
- あるRepositoryに適用されていても、
  そのことだけで、そのRepositoryが
  Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
  そのものの内容を所有することにはならない。
- 適用状態（Application State／適用状態）の変化は、
  Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）
  そのもののOwnership（所有責任）を移動させない。
  ただしこれは、適用の結果として成立したRepository-localなAsset（資産）の
  Ownership（所有責任）を本文書が決定することを意味しない
  （「適用済みAssetの扱い」を参照）。

### Application Mechanism Independence（適用方式を上位で固定しない）

Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）の
**具体方式（Application Mechanism／適用方式）は本文書で固定しない** 。

将来的に、例えば次のような方式があり得る。

- Direct Reference（直接参照）
- GitHub-native Reuse（GitHub標準機能による再利用）
- Repository-local Deployment（対象Repositoryへのローカル展開）
- その他、具体Requirement（具体的な要求）から必要になる方式

どの方式を用いるかは、Asset Type（資産種別）ごとの制約や
実際のRequirement（要求）に依存する。
したがって方式の選定は、
**必要なAsset（資産）ごとの後続設計へ委譲する** 。

本文書が要求するのは、
どの方式を採る場合でも
Ownership（所有責任）とApplication（適用）の分離が保たれることのみである。

## Shared Scope Principles（共有基盤へ含める範囲の判断原則）

### Responsibility-based Sharing（再利用性ではなく共有責務に基づいて共通化する）

Shared Development Foundation（複数Repositoryで共有する開発基盤）へ
含める根拠は、
**単に複数Repositoryで再利用可能であることではない** 。

含める根拠となるのは、
複数Repositoryに共通する開発上の責務として
**一元的に所有・維持すべきSemantic Need（意味上の必要性）** が
存在することである。

### 判断の指針

含める判断が成立するのは、次が言える場合である。

- その関心事が、複数Repositoryに共通する **開発上の責務** である。
- その内容が分散して個別に維持されると、
  Repository間で意図しない不整合が生じる、
  あるいは共通責務としての一貫性が失われる。
- 内容の決定主体を一箇所に置くことに、意味上の妥当性がある。

含めない判断が成立するのは、次のいずれかが言える場合である。

- その内容が特定Repository固有のDomain（題材領域）／System（システム構造）／
  Repository-specific concern（個別Repository固有の関心事）に属する。
- 現時点で共有責務が存在せず、
  **将来利用する可能性だけ** を根拠としている。
- 単に他Repositoryへ複製しても機能する、という
  技術的な再利用可能性のみが根拠となっている。

### 先行共通化（Anticipatory Sharing）を行わない

将来的に共有され得るという見込みだけを根拠として、
Shared Development Foundation（複数Repositoryで共有する開発基盤）へ
先行して内容を移動させない。

共有責務が実際に成立した時点で、
Ownership（所有責任）の移動として明示的に判断する。

## Self Application（`.github`自身への適用）

`.github` 自身も、本文書が定義する
Repository Governance Model（Repository間の統治・責務モデル）の対象である。
`.github` は例外的な上位存在ではない。

`.github` は次の2つのRole（役割）を同時に持つ。

1. **Owner / Provider Role（所有者・提供者としての役割）**
   Shared Development Foundation（複数Repositoryで共有する開発基盤）と
   Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）の
   所有者・提供者としての役割。

2. **Applied Repository Role（適用先Repositoryとしての役割）**
   自身へのFoundation Application
   （共通開発基盤を対象Repositoryへ適用する関係）を持つ、
   一適用先Repositoryとしての役割。

この2つのRole（役割）は区別される。
したがって、
**`.github` 自身に存在する適用済みAsset（適用の結果として存在する資産）を、
Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）そのものと
自動的に同一視しない** 。

`.github` にも、`.github` 自身の
Repository-specific concern（個別Repository固有の関心事）に属する
Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）が
存在し得る。
`.github` に存在するという事実だけでは、
その内容が共有対象であることを意味しない。

## Design Principles（設計原則）

### 1. Responsibility over Location（配置ではなく責務で判断する）

Ownership（所有責任）および
Shared（共有）／Repository-specific（個別Repository固有）の区別は、
Physical Location（物理配置）ではなく
Responsibility（責務）によって説明される。

### 2. Separation of Ownership and Application（所有と適用を分離する）

内容を所有すること（Ownership／所有責任）と、
その内容が特定Repositoryで有効であること（Application／適用）を分離する。
一方の変化が他方を自動的に決定しない。

### 3. Mechanism Independence（方式を上位で固定しない）

上位Architectureは関係と責務を定義し、
その実現手段（Application Mechanism／適用方式）を先行して固定しない。

### 4. Semantic Need over Reusability（再利用性ではなく意味上の必要性）

共通化は、技術的な再利用可能性ではなく
Semantic Need（意味上の必要性）に基づいて判断する。

### 5. Repository Autonomy（Repositoryの自律性を保つ）

各Repositoryは自身のDomain（題材領域）・System（システム構造）・
Repository-specific concern（個別Repository固有の関心事）について
Ownership（所有責任）を保持する。
共有基盤の存在は、この自律性を縮小しない。

### 6. Uniform Model including Self（自身も同じModelで説明する）

`.github` を含め、すべてのRepositoryが
同一のRepository Governance Model（Repository間の統治・責務モデル）で説明される。
Modelの外側に立つRepositoryを設けない。

### 7. Explicit State over Complete Inference（完全な暗黙推論より必要な状態の明示を優先する）

ArchitectureやConvention（規約）を、
個々のAsset（資産）のOwnership（所有責任）や
Application State（適用状態）を
**完全に機械導出できるほど複雑化することを要求しない** 。

必要な具体状態は、後続設計において
Metadata（構造化メタデータ）やDeclaration（明示的宣言）として
明示的に表現できる。
本文書はその可能性を許容するのみであり、
表現形式を定義しない。

## Non-goals / Delegation（今回扱わず後続へ委譲する事項）

本文書は次を定義しない。これらは後続設計へ委譲する。

### 個別System / Domainに関する事項

- Symnous Architecture / Specification
- AI-CoS Architecture / Runtime
- AI Integration（AI連携構造）の具体設計
- `CLAUDE.md` / `AGENTS.md` / `.ai/` の具体仕様

これらは各Repositoryの
Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）
として扱われ得る領域であり、
本文書がShared Development Foundation（複数Repositoryで共有する開発基盤）の
所有対象として先行決定するものではない。

### 構造・規約に関する事項

- Documentation階層およびDirectory構造の正式確定
- Convention（規約）体系の詳細
- Base / Pattern / Repository / Effective Convention といった
  Convention（規約）の階層区分
- Override（上書き）／Extend（拡張）／Replace（置換）／Disable（無効化）等の
  拡張方式

### 適用方式に関する事項

- Application Mechanism（適用方式）の具体実装
- Asset Type（資産種別）ごとの適用手順

### 宣言・記述形式に関する事項

- Metadata File（メタデータFile）およびSchema
- Repository Manifestの具体Schema
- Ownership（所有責任）／Application State（適用状態）の
  機械可読な表現形式

### Authority Model（権威モデル）に関する事項

- Formal Asset / Formal Authority / Authority Domain 等の
  Generic Authority Model（一般化された権威モデル）

本文書はOwnership（所有責任）とApplication（適用）の関係のみを定義し、
一般化された権威体系を導入しない。

### 具体資産に関する事項

- Template（テンプレート）の具体仕様・実装
- Workflow（ワークフロー）の具体仕様・実装

## Usage by Downstream Design（下位設計からの参照）

後続設計は、本文書を参照して次を判断できる。

1. 対象とする定義・資産が
   Shared Foundation Asset（共通開発基盤が所有する共有定義・共有資産）か、
   Repository-owned Asset（対象Repository自身が内容を決定・所有する定義・資産）か。
   → 「Ownership Boundary（所有責任の境界）」の判定基準による。

2. Shared Development Foundation（複数Repositoryで共有する開発基盤）へ
   含めてよいか。
   → 「Shared Scope Principles（共有基盤へ含める範囲の判断原則）」による。

3. 適用に関する設計をどこで行うか。
   → Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）の
   具体方式は、各Asset（資産）単位の後続設計で決定する。

本文書からは判断できないのは、
個々のAsset Type（資産種別）の内容そのものと、その適用手順である。
これらは後続設計の責務に属する。
