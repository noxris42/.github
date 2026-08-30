# Convention Architecture（規約のArchitecture）

## Purpose（目的）

本文書は、`noxris42` において
**Convention（規約）** とは何であり、何を責務とし、
その内部でRuleがどのような意味構造を持つのかを定義する
上位Modelである。

本文書が扱う問いは次の4点である。

1. Convention（規約）は何を定義する存在なのか
   — Convention Responsibility（規約責務）。
2. Convention（規約）の中で、何が
   **規範として効力を持つ単位** なのか
   — Normative Rule（規範的ルール）。
3. Normative Rule（規範的ルール）は意味上どのような要素から成るのか
   — Rule Model（ルールモデル）。
4. Normative Rule（規範的ルール）はどのように
   **安定して参照され続けるのか**
   — Rule Identity（ルール同一性）。

本文書は上位Architectureとして自己完結する。
個別のConvention（規約）の内容、およびConvention（規約）の
具体的な記述方法（Convention Authoring Rule）の
存在や内容を前提としない。

## Position（設計上の位置づけ）

本文書は
[Repository Governance Architecture](repository-governance.md)
を
上位Sourceとして参照する。

Design Dependency（設計依存）は
**Repository Governance Architecture → 本文書 → 個別Convention（規約）**
の一方向とする。
本文書は、Repository Governance Architectureが定義する
Ownership（所有責任）・Foundation Application・Shared Scopeの判断を
再定義・上書きしない。

したがって次は本文書の責務ではない。

- あるConvention（規約）が
  Shared Foundation Assetか、
  Repository-owned Assetか
  の判定。
  → Repository Governance Architectureの
  「Ownership Boundary（所有責任の境界）」による。
- あるConvention（規約）が特定Repositoryで有効になる関係。
  → Repository Governance Architectureの
  Foundation Applicationによる。

本文書は、Convention（規約）が
**所有され適用される対象として、内部にどのような意味構造を持つか**
のみを定義する。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Convention（規約）の意味とConvention Responsibility（規約責務）
- Normative Rule（規範的ルール）の定義と、
  Convention（規約）内の非規範的内容との区別
- Rule Model（ルールモデル）：
  Normative Rule（規範的ルール）が意味上持つ要素
- Requirement Level（要求レベル）の共通語彙とその意味
- Rule Identity（ルール同一性）の意味上の構成
- Rule Identity Stabilityの原則

### Out of Scope（本文書が定義しない範囲）

- Rule Identity（ルール同一性）の具体的な表記Format、および採番方法
- Markdown等、特定の記述媒体上でのRuleの表現方法
- RuleのCategory（分類）やSection配置の方法
- 個別Convention（規約）の内容
- Convention（規約）を代表・集約する文書の要否と責務
- Convention Application（規約適用）の詳細、および
  Override（上書き）／Extend／Replace／Disable
- MetadataおよびDeclarationのSchema
- ReleaseおよびVersioning（版管理）の具体実装

詳細は「Non-goals」に示す。

## Concept Model（概念モデル）

### Convention（規約）

Convention（規約）は、Repository上の
**成果物または開発作業** に適用される
Normative Rule（規範的ルール）を定義するものである。

Convention（規約）は、Normative Rule（規範的ルール）に加えて、
説明・Example・背景・補足等の内容を含めてよい。
ただし、
**Convention（規約）内のすべての内容が
Normative Rule（規範的ルール）になるわけではない** 。

すなわちConvention（規約）は、
規範的内容と非規範的内容の双方を含み得る単位であり、
そのうち規範として効力を持つのは、
Normative Rule（規範的ルール）として明示された部分に限られる。

### Normative Rule（規範的ルール）

Normative Rule（規範的ルール）は、
Convention（規約）が対象に対して
**要求・禁止・推奨・許容する内容を明示する規範単位** である。

Convention（規約）の
Normative Effectは、
Normative Rule（規範的ルール）を通じて表現される。
すなわち、Convention（規約）が対象に対して持つ規範的な効力は、
Normative Rule（規範的ルール）として明示された内容に由来する。

### Non-normative Content（非規範的内容）

Convention（規約）に含まれる、
Normative Rule（規範的ルール）以外の内容。
説明・Example・背景・補足等がこれに当たる。

Non-normative Content（非規範的内容）は理解を助けるが、
**それ自体では新たなNormative Requirement（規範要求）を追加しない** 。

したがって、説明・Example・背景・補足等は、
それ自体がRuleとして扱われることはない。
Exampleが示す形は、
Normative Rule（規範的ルール）の理解を助ける例示であって、
それ自体が要求・禁止を新たに生じさせるものではない。

### Concept（概念）間の関係

```text
Convention
  │
  ├─ defines ─▶ Normative Rule── Normative Effectを持つ
  │                  │
  │                  └─ identified by ─▶ Rule Identity
  │
  └─ may contain ─▶ Non-normative Content
```

## Rule Model（ルールモデル）

Normative Rule（規範的ルール）は意味上、次の要素を持つ。

ここで定義するのは
**意味上どの要素が必要か** であり、
それらをどのように記述・表示するかではない。

### Required Elements（必須要素）

| 要素 | 意味 |
| --- | --- |
| Rule Identity（ルール同一性） | そのRuleをStable Reference（安定参照）するための同一性 |
| Rule Name（ルール名） | そのRuleを人間が識別・想起するためのLabel |
| Requirement Level（要求レベル） | そのRuleが要求・禁止・推奨・許容のいずれであるかの水準 |
| Rule Statement（ルール文） | そのRuleが対象に対して規定する内容そのもの |
| Reason | そのRuleが必要である目的・問題・制約 |

### Optional Elements（任意要素）

| 要素 | 意味 |
| --- | --- |
| Supplementary Information | 理解を助ける説明・Example・注意点等 |

Supplementary Informationは
Non-normative Content（非規範的内容）であり、
それ自体では新たなNormative Requirement（規範要求）を追加しない。

### Reason（理由）の要件

Reasonは、Rule Statement（ルール文）の
**単なる言い換えであってはならない** 。

Reasonが説明するのは、
そのRuleが **なぜ必要なのか** 、
すなわち達成しようとする目的、回避しようとする問題、
前提となる制約である。

Reasonを必須とするのは、次のためである。

- Ruleの妥当性を、後から検証・再評価できるようにする。
- Requirement Level（要求レベル）が `SHOULD` / `SHOULD NOT` の場合に、
  例外を認めてよいかを判断できるようにする。
- Ruleの変更・廃止が妥当かを、目的に照らして判断できるようにする。

### Rule Name（ルール名）とRule Identity（ルール同一性）の区別

Rule Name（ルール名）は
**Human-readable Label** であり、
Rule Identity（ルール同一性）そのものではない。

したがって次が成立する。

- Rule Name（ルール名）は、
  Normative Meaning（規範的意味）を変えない範囲で改善・変更され得る。
- Rule Name（ルール名）の変更は、
  Rule Identity（ルール同一性）を変更しない。
- Ruleへの安定した参照は、
  Rule Name（ルール名）ではなく
  Rule Identity（ルール同一性）に対して行う。

## Requirement Levels（要求レベル）

Convention（規約）全体で用いる共通語彙として、
次のRequirement Level（要求レベル）を定義する。

| Level | 意味 |
| --- | --- |
| `MUST` | 適合のために要求される。 |
| `MUST NOT` | 適合のために禁止される。 |
| `SHOULD` | 原則として要求されるが、合理的な理由がある場合は例外を認める。 |
| `SHOULD NOT` | 原則として禁止されるが、合理的な理由がある場合は例外を認める。 |
| `MAY` | 許容されるが、実施は要求されない。 |

### Self-contained Semantics（意味をArchitecture内で自己完結させる）

これらのRequirement Level（要求レベル）の意味は、
**本文書の定義によって自己完結する** 。

外部のRFC等に対するNormative Dependencyは設けない。
すなわち、外部文書の改訂や解釈が
本文書のRequirement Level（要求レベル）の意味を変更することはない。

外部の慣行と語形が一致することは、
理解の助けとして有用であるが、意味の根拠ではない。

## Rule Identity（ルール同一性）

### Rule Identity（ルール同一性）とは何か

Normative Rule（規範的ルール）は、
**Stable Reference（安定参照）** のための
Rule Identity（ルール同一性）を持つ。

Rule Identity（ルール同一性）が満たすべきことは次である。

- あるNormative Rule（規範的ルール）を、
  文書上の配置・順序・見出し・Rule Name（ルール名）に依存せず特定できる。
- 他のNormative Rule（規範的ルール）と一意に区別できる。

### 意味上の構成

Rule Identity（ルール同一性）は意味上、次から構成される。

| 構成要素 | 意味 |
| --- | --- |
| Convention Identity（規約同一性） | そのRuleがどのConvention（規約）に属するか |
| Definition Namespace（定義名前空間） | そのRuleがどの定義名前空間に属するか |
| Rule-local Identity | 同一のConvention Identity（規約同一性）・Definition Namespace（定義名前空間）の中で、そのRuleを一意に識別する同一性 |

本文書は、これらを
**どのような表記に落とすかを定義しない** 。
表記Formatおよび採番方法は後続設計へ委譲する。

### Definition Namespace（定義名前空間）の目的

Definition Namespace（定義名前空間）は、
将来のConvention Extensionを可能にするための
**Rule Identity（ルール同一性）上の区分** である。

Definition Namespace（定義名前空間）が果たす役割は次に限られる。

- Ruleが属する定義名前空間を識別する。
- 異なるDefinition Namespace（定義名前空間）に属する
  Rule Identity（ルール同一性）を、衝突なく識別できるようにする。

Convention Extensionにおいて
どのような拡張単位が存在するのか、
Definition Namespace（定義名前空間）が
どのように成立・付与されるのかは、
本文書では定義しない。

### Namespaceから関係を推論しない

Definition Namespace（定義名前空間）は
**識別のための区分であり、関係を表現しない** 。

したがって、Namespaceから次を推論してはならない。

- Override（上書き）
- Replacement
- Inheritance
- その他のRule Relationship（ルール間関係）

Rule間に何らかの関係が必要となる場合、
その関係はNamespaceから暗黙に導出されるのではなく、
後続設計において明示的に定義される。

## Rule Identity Stability（ルール同一性の安定性）

Rule Identity（ルール同一性）の安定性は、
**Development VersionとStable Versionの境界** で扱う。

本文書は境界の意味のみを定義し、
Development Version／Stable Versionの
具体的なRelease Management方法は定義しない。

### Development Version（開発版）における扱い

- Development Versionで新規に導入された
  Rule Identity（ルール同一性）は、
  Stable Release前であれば、
  設計変更に伴って再編できる。
- 過去のStable Versionですでに公開された
  Rule Identity（ルール同一性）は、
  Development Versionの途中であっても変更しない。

### Stable Version（安定版）における扱い

- Stable Releaseされた
  Rule Identity（ルール同一性）は永続化する。
- 永続化されたRule Identity（ルール同一性）は、
  そのRuleが削除された後も、
  **別のRuleへ再利用しない** 。

Identity（同一性）を再利用しないのは、
過去の参照が別の意味へ静かにすり替わることを防ぐためである。

### Identity（同一性）の維持と更新

| 変更の性質 | 扱い |
| --- | --- |
| Normative Meaning（規範的意味）が維持される変更（表現の改善、Rule Name（ルール名）の変更、Reasonや補足の拡充等） | 既存のRule Identity（ルール同一性）を維持する |
| Normative Meaning（規範的意味）が実質的に変わる変更 | 新しいRule Identity（ルール同一性）とする |
| SplitまたはMergeによって新しいNormative Rule（規範的ルール）が成立する場合 | 新しいRule Identity（ルール同一性）とする |

判断の基準は
**Normative Meaning（規範的意味）が実質的に変わったか** であり、
文面が変わったかではない。

## Design Principles（設計原則）

### 1. Normative Content is Explicit（規範的内容を明示する）

Convention（規約）内で規範として効力を持つ内容は、
Normative Rule（規範的ルール）として明示される。
文脈や語調から規範性を暗黙に推論しない。

### 2. Rule Carries Its Reason（Ruleは理由を伴う）

Normative Rule（規範的ルール）はReasonを必須要素として持つ。
理由を伴わないRuleは、検証も再評価もできない。

### 3. Identity over Label（Labelではなく同一性で参照する）

安定した参照はRule Identity（ルール同一性）に対して行う。
Rule Name（ルール名）・見出し・配置・順序は参照の基礎としない。

### 4. Identity Reflects Normative Meaning（同一性は規範的意味に対応する）

Rule Identity（ルール同一性）の維持・更新は、
表現の変化ではなくNormative Meaning（規範的意味）の変化に対応する。

### 5. Identity is Not Reused（同一性を再利用しない）

永続化されたRule Identity（ルール同一性）は、
削除後も別のRuleへ再割り当てしない。

### 6. Namespace Identifies, Not Relates（Namespaceは識別であって関係ではない）

Definition Namespace（定義名前空間）は識別のための区分であり、
Rule Relationship（ルール間関係）を含意しない。
関係が必要な場合は明示的に定義する。

### 7. Self-contained Normative Vocabulary（規範語彙を自己完結させる）

Requirement Level（要求レベル）等の規範語彙の意味は、
本Architecture内で自己完結させ、
外部文書へのNormative Dependencyを設けない。

### 8. Semantics before Notation（表記より意味を先に定める）

本Architectureは意味構造のみを定義し、
表記Format・記述形式・文書表現を先行して固定しない。

## Non-goals（現在扱わない事項）

本文書は次を定義しない。これらは後続設計へ委譲する。

### Authoring（記述）に関する事項

- Rule Identity（ルール同一性）の具体的な表記Format
- Rule Identity（ルール同一性）に含まれるNumberの桁数・採番方法
- Markdown上でのRuleの表現方法
  （見出しの取り方、Rule Name（ルール名）の併記形、項目名の並べ方等）
- Rule Model（ルールモデル）の各要素を文書上でどう記述単位へ対応させるか
- RuleのCategory（分類）およびSection配置の方法

### Conformance（適合）に関する事項

本文書は、Normative Rule（規範的ルール）のみが
Normative Effectを持つという境界のみを定めており、
次は定義しない。

- Convention（規約）全体としてのConformance Model
- 適合・不適合の判定方法
- `SHOULD` / `SHOULD NOT` における例外の扱い方および
  その正当化の手続き

### Convention Identity（規約同一性）に関する事項

本文書はConvention Identity（規約同一性）を
Rule Identity（ルール同一性）の意味上の構成要素として位置づけるが、
次は定義しない。

- Convention Identity（規約同一性）の具体的な識別方法
- Convention Identity（規約同一性）の表記方法
- Convention Identity（規約同一性）の安定性・変更規則

これはDesign Gapではなく、
現時点で確定していない事項を先行決定しないための
意図的な委譲である。

### Convention Extension（規約拡張）に関する事項

- Convention Extensionにおける拡張単位
- Definition Namespace（定義名前空間）の成立・付与の方法

### Convention（規約）体系に関する事項

- Convention（規約）を代表・集約する文書の要否と責務
- Convention（規約）の一覧・目録の構造

### Application（適用）に関する事項

- Convention Application（規約適用）の詳細
- Override（上書き）／Extend／Replace／Disable
- Rule Relationship（ルール間関係）の具体Model

Convention（規約）がRepositoryにおいて有効となる関係そのものは、
[Repository Governance Architecture](repository-governance.md)の
Foundation Applicationが扱う。

### 宣言・記述形式に関する事項

- MetadataおよびDeclarationのSchema
- Rule Identity（ルール同一性）の機械可読な表現形式

### Release / Versioning（版管理）に関する事項

- Development Version／Stable Versionの
  具体的なRelease Management方法
- Version表記およびVersioning（版管理）規則

## Usage by Downstream Design（下位設計からの参照）

個別のConvention（規約）および
Convention Authoring Ruleは、
本文書を参照して次を前提にできる。
これらを再定義する必要はない。

1. Convention（規約）が何を定義する存在であるか
   — Convention Responsibility（規約責務）。
2. Convention（規約）内で何が規範単位であるか
   — Normative Rule（規範的ルール）。
3. Normative Rule（規範的ルール）が意味上どの要素を持つか
   — Rule Model（ルールモデル）。
4. Requirement Level（要求レベル）の語彙とその意味。
5. Rule Identity（ルール同一性）が何を識別し、
   どの条件で維持・更新されるか。

本文書からは判断できないのは、
それらを **どのように表記・記述するか** 、
および個別Convention（規約）の内容そのものである。
これらは後続設計の責務に属する。
