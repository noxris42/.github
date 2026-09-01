# Convention Authoring Convention（規約記述規約）

## Purpose（目的）

本文書は、`noxris42` において**Convention（規約）をどのように記述するか** を定めるConvention Asset（規約資産）である。

[Convention Architecture](../architecture/convention.md)は、Convention（規約）とNormative Rule（規範的規則）の意味、Rule Model（規則モデル）、Requirement Level（要求レベル）、Rule Identity（規則同一性）とその安定性を定義する。ただし同Architectureは、それらを **どのような表記へ落とすか** を意図的に定義しない。

本文書はその委譲先として、Convention Architectureが定義するConvention（規約）およびRule Model（規則モデル）を、Convention Asset（規約資産）上で**明示的・一貫的・安定参照可能に表現するためのReusable Normative Standard（再利用可能な規範標準）**を定義する。

本文書は、Convention Architectureが定義するConcept（概念）を再定義しない。本文書が定めるのは表記および記述運用に限られる。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するConventions Area（規約領域）に属する通常のDocumentation Asset（文書資産）である。Areaを代表・集約するAssetではない。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）はConvention Architectureにある。本文書はこれらを参照するのみで、再定義しない。

- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的規則）とNon-normative Content（非規範的内容）の区別
- Rule Model（規則モデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（規則同一性）の意味上の構成
- Definition Namespace（定義名前空間）の意味と、そこから関係を推論しないこと
- Rule Identity Stabilityの原則

### Position（設計上の位置づけ）

本文書は[Convention Architecture](../architecture/convention.md)を上位Sourceとして参照する。

Design Dependency（設計依存）は**Convention Architecture → 本文書**の一方向とする。

```text
Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
```

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Convention Code（規約コード）のConcrete Representation（具体表現）
- Rule ID Format（規則ID形式）
- Namespace Code（名前空間コード）のConcrete Representation（具体表現）
- Rule Numberの表記と採番
- Rule Field（規則フィールド）の構成・順序・Markdown表現
- Rule Boundary（規則境界）の取り方
- Rule Section Heading Representation（Rule Section見出し表現）
- StabilityのField表現とその遷移
- Rule ID Stability Operation
- Retired Rule ID（廃止済み規則ID）の記録方法
- 現在必要なConcrete Identifier Declaration

### Out of Scope（本文書が定義しない範囲）

- Convention（規約）そのものの意味、Normative Rule（規範的規則）の意味、Requirement Level（要求レベル）の意味
- Rule Identity（規則同一性）およびRule Identity StabilityのSemantic Model（意味モデル）
- Definition Namespace（定義名前空間）の一般的な成立条件・付与方法
- Convention Application（規約適用）、Override（上書き）／Extension等のRule Relationship（規則間関係）
- 一般的なMarkdown規約
- 一般的なDocumentation Section Structure、およびHeading Level（見出しレベル）の固定
- Naming Convention一般
- Navigation / IndexおよびConvention Registry
- Metadata／Declaration Schema、 JSON / YAML等のMachine-readable Structure
- Release Management、Version表記、Tag運用
- Commit Convention等、個別Convention（規約）固有のRule

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。**Normative Rule（規範的規則）ではない** 。

Normative Rule（規範的規則）が定めるのは識別子の形式および使用条件であり、どの値を割り当てるかは本節の宣言による。両者を混同しない。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CVA
```

### Namespace Code Assignment（名前空間コード割当）

現在割り当てられているNamespace Code（名前空間コード）は次である。

```text
SF = Shared Foundation Namespace
```

現時点で割当済みのNamespace Code（名前空間コード）は `SF` のみである。将来Namespace Code（名前空間コード）が追加され得るが、どのような拡張単位が成立し、Definition Namespace（定義名前空間）がどのように付与されるかは、本文書では定義しない。

## Authoring Concepts（本文書が定義する記述上の概念）

本節は、本文書が所有する記述上のConcept（概念）を示す。上位Architectureが定義するConcept（概念）を再定義するものではない。

### Rule ID（規則ID）

Rule ID（規則ID）は、Convention Architectureが定義するRule Identity（規則同一性）のConcrete Representation（具体表現）である。

意味上の構成要素との対応は次である。

| Rule Identity（規則同一性）の構成要素 | Rule ID（規則ID）上のSegment |
| --- | --- |
| Convention Identity（規約同一性） | Convention Code（規約コード） |
| Definition Namespace（定義名前空間） | Namespace Code（名前空間コード） |
| Rule-local Identity | Rule Number |

### Stability（安定性）

Stabilityは、Convention Architectureが定めるDevelopment Version／Stable Versionの境界を、個々のNormative Rule（規範的規則）上で明示するためのFieldである。

値は次の2つに限られる。

| 値 | 意味 |
| --- | --- |
| `Development` | Stable Release前であり、Rule ID（規則ID）を再編できる状態 |
| `Stable` | Stable Release済みであり、Rule ID（規則ID）が永続化された状態 |

遷移は一方向である。

```text
Development
    ↓ Stable Release
Stable
```

Releaseの手続き、Version表記、Tag運用は本文書では定義しない。

### Retired Rule ID（廃止済み規則ID）

Retired Rule ID（廃止済み規則ID）は、`Stable` となった後にCurrent Normative Ruleから削除され、再利用不可となったRule ID（規則ID）を保持する**Non-normative Record** である。

Retired Rule ID（廃止済み規則ID）は`Stability` の値ではなく、Rule Lifecycle Stateでもない。記録されるのはRule ID（規則ID）だけであり、Ruleそのものはすでに存在しない。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

各Ruleの見出しはRule Boundary（規則境界）とDocument Presentationのためにあり、Rule Model（規則モデル）のCanonical Representationではない。Ruleの内容は、見出しではなくFieldによって確定する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、Rule ID（規則ID）はCategory（分類）を表現しない。

### Convention Identification（規約識別）

#### CVA-SF-001 — Convention Code Declaration（規約コードの宣言）

**Rule ID:** `CVA-SF-001`

**Rule Name:** Convention Code Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Convention Asset（規約資産）は、自身を識別するConvention Code（規約コード）を1つ、その資産上で明示的に宣言する。

**Reason:** Rule ID（規則ID）はConvention Code（規約コード）を先頭Segmentとして含む。CodeがFile名やDocument Title（文書題名）からの推論に依存すると、配置や題名の変更でRule ID（規則ID）の解釈が揺らぐ。明示的宣言により、Rule ID（規則ID）の解釈を資産自身の記述だけで確定させる。

#### CVA-SF-002 — Convention Code Format（規約コードの形式）

**Rule ID:** `CVA-SF-002`

**Rule Name:** Convention Code Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Convention Code（規約コード）は、ASCII大文字英字3文字で表現する。

**Reason:** 文字種と桁数を固定することで、Rule ID（規則ID）のSegmentを表記だけで判別できる。同一Convention（規約）に対して長短の異なるCode表記が併存することも防ぐ。

#### CVA-SF-003 — Convention Code Stability（規約コードの安定性）

**Rule ID:** `CVA-SF-003`

**Rule Name:** Convention Code Stability

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Stable Rule IDの一部として使用されたConvention Code（規約コード）を変更してはならない。

**Reason:** Convention Code（規約コード）の変更は、すでに永続化されたすべてのRule ID（規則ID）を一括で無効化する。これはRule Identity（規則同一性）を永続化する原則に反し、既存の参照を失わせる。

### Rule Identifier（規約ルール識別子）

#### CVA-SF-004 — Rule ID Requirement（規約ルールIDの必須性）

**Rule ID:** `CVA-SF-004`

**Rule Name:** Rule ID Requirement

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的規則）は、完全なRule ID（規則ID）を持たなければならない。

**Reason:** Rule Identity（規則同一性）はNormative Rule（規範的規則）の必須要素である。Rule ID（規則ID）を欠くRuleは見出し・配置・Rule Name（規則名）でしか参照できず、Stable Reference（安定参照）が成立しない。

#### CVA-SF-005 — Rule ID Structure（規約ルールIDの構造）

**Rule ID:** `CVA-SF-005`

**Rule Name:** Rule ID Structure

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規則ID）は、`<Convention>`、`<Namespace>`、`<Number>` の3つのSegmentをハイフンで連結した `<Convention>-<Namespace>-<Number>` の形式で表現する。

**Reason:** Rule Identity（規則同一性）の意味上の構成要素であるConvention Identity（規約同一性）・Definition Namespace（定義名前空間）・Rule-local Identityを、表記上も1対1で対応させる。構造を固定することで、Rule ID（規則ID）から所属Convention（規約）とNamespaceを判別できる。

**Note:** 具体形式は `CCC-NN-NNN` となる。例：`CVA-SF-001`。

#### CVA-SF-006 — Convention Segment（規約Segment）

**Rule ID:** `CVA-SF-006`

**Rule Name:** Convention Segment

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規則ID）の `<Convention>` には、そのRuleが属するConvention Asset（規約資産）が宣言したConvention Code（規約コード）を使用する。

**Reason:** 宣言された値以外を使用すると、Rule ID（規則ID）が指すConvention（規約）を資産の宣言から確定できなくなる。宣言と使用を一致させることで、Rule ID（規則ID）の解決先が一意に定まる。

#### CVA-SF-007 — Namespace Segment（名前空間Segment）

**Rule ID:** `CVA-SF-007`

**Rule Name:** Namespace Segment

**Stability:** Development

**Requirement:** MUST

**Rule:** Namespace Code（名前空間コード）はASCII大文字英字2文字で表現し、Rule ID（規則ID）の `<Namespace>` には、そのRuleが属するDefinition Namespace（定義名前空間）へ割り当てられたNamespace Code（名前空間コード）を使用する。

**Reason:** Definition Namespace（定義名前空間）はRule Identity（規則同一性）の構成要素であり、表記上も区別できなければRule ID（規則ID）が衝突し得る。割当済みCodeに限定するのは、その場限りのCodeが増えて識別性が失われることを防ぐためである。

**Note:** 現在割り当てられているNamespace Code（名前空間コード）は「Namespace Code Assignment」に示す。

#### CVA-SF-008 — Rule Number Format（Rule Numberの形式）

**Rule ID:** `CVA-SF-008`

**Rule Name:** Rule Number Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規則ID）の `<Number>` は、同一の `Convention × Namespace` におけるRule-local Identityとして、`001` から始まる3桁ゼロ埋めの十進数で表現する。

**Reason:** 桁数を固定しない番号は、`1` と `01` のように同一Ruleへ複数の表記を生じさせ、参照の一致判定を壊す。開始値と桁数を固定することで、Rule ID（規則ID）の表記が一意に定まる。

#### CVA-SF-009 — Opaque Rule Number（意味を持たないRule Number）

**Rule ID:** `CVA-SF-009`

**Rule Name:** Opaque Rule Number

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Rule Numberに、Category（分類）、Document Order、その他のSemantic Meaningを持たせてはならない。Rule Numberは識別のみに用いる。

**Reason:** 番号へ意味を持たせると、分類の見直しやSectionの並べ替えのたびに再採番の圧力が生じ、Rule Identity（規則同一性）の永続化と衝突する。番号を識別専用に保つことで、文書構成の変更がRule ID（規則ID）へ波及しない。

### Rule Presentation（規則記述形式）

#### CVA-SF-010 — Rule Section（ルールSection）

**Rule ID:** `CVA-SF-010`

**Rule Name:** Rule Section

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的規則）は、独立したHeading Sectionとして記述する。

**Reason:** Rule Boundary（規則境界）が曖昧だと、どこまでが1つのNormative Rule（規範的規則）かを判断できず、規範的内容と非規範的内容の区別も失われる。Section単位に分けることで、境界が一意に定まる。

**Note:** Heading（見出し）はRule Boundary（規則境界）とDocument Presentationのためのものであり、Rule Model（規則モデル）のCanonical Representationではない。Heading Level（見出しレベル）は、本Convention（規約）では固定しない。Heading（見出し）の文字列形式は`CVA-SF-023` が定める。本Ruleが定めるのは、1つのNormative Rule（規範的規則）が1つの独立したHeading Sectionとして記述されることに限られる。

#### CVA-SF-023 — Rule Section Heading Representation（Rule Section見出し表現）

**Rule ID:** `CVA-SF-023`

**Rule Name:** Rule Section Heading Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Normative Rule（規範的規則）のRule Section（ルールSection）のHeading（見出し）は、そのRuleのRule ID（規則ID）、Rule Name（規則名）、およびPrimary Language Heading Explanation（主要言語見出し説明）を、次の形式で表示する。

```text
Rule ID — Rule Name（Primary Language Heading Explanation）
```

Primary Language Heading Explanation（主要言語見出し説明）は、Rule Section Heading Presentation（Rule Section見出し表示）側で定義する。その値は、当該Rule Section（ルールSection）のRule Section Responsibility（Rule Section責務）をPrimary Languageで理解可能にするHuman-readable Representation（人間可読表現）である。

**Reason:** Rule Section Heading（Rule Section見出し）がRule ID（規則ID）とRule Name（規則名）だけで構成される場合、そのRule Section（ルールSection）が何を扱う責務なのかをHeading（見出し）からPrimary Languageで把握できない。Heading（見出し）へPrimary Languageによる理解補助を含めることで、読み手は本文を読む前に対象Ruleを絞り込める。Definition Responsibility（定義責務）をRule Section Heading Presentation（Rule Section見出し表示）側へ置くのは、このPrimary Languageによる値がHeading（見出し）という表示のために必要となる値であり、Rule Model（規則モデル）が保持すべきNormative Content（規範的内容）ではないためである。定義の所在を表示側に限定することで、Heading（見出し）の都合がRule Model（規則モデル）およびRule Identity（規則同一性）へ波及しない。

**Note:** Primary Language Heading Explanation（主要言語見出し説明）はRule Model（規則モデル）のFieldではなく、Rule Field（規則フィールド）として記述しない。Rule Name（規則名）のPrimary Language Rule Name Representation（主要言語Rule Name表現）でもない。

Primary Language Heading Explanation（主要言語見出し説明）がRule Name（規則名）の自然なPrimary Languageによる訳と同じ文字列になることは許容する。ただしその文字列一致から、Primary Language Rule Name（主要言語Rule Name）というSemantic Role（意味上の役割）は導出されない。

本Ruleは、Rule Identity（規則同一性）およびRule Name（規則名）へPrimary Language Representation（主要言語表現）を追加しない。

Primary Language Heading Explanation（主要言語見出し説明）としての値は、Rule Section Heading Presentation（Rule Section見出し表示）側で定義され、Canonical Primary Language Support（正規主要言語補助）によって定義または導出されない。

同じConcrete Primary Language String（具体主要言語文字列）が、別途Canonical Primary Language Support Representation（正規主要言語補助表現）として成立することは妨げない。ただしその文字列一致から、両者のSemantic Role（意味上の役割）またはDefinition Responsibility（定義責務）が同一であることは導出されない。

本Ruleが定めるのはHeading（見出し）の文字列形式に限られる。Heading Level（見出しレベル）は `CVA-SF-010` と同様、本Convention（規約）では固定しない。

記述例は次である。

```text
#### CVA-SF-001 — Convention Code Declaration（規約コードの宣言）
```

#### CVA-SF-011 — Required Rule Fields（必須ルールフィールド）

**Rule ID:** `CVA-SF-011`

**Rule Name:** Required Rule Fields

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的規則）は、`Rule ID`、`Rule Name`、`Stability`、`Requirement`、`Rule`、`Reason`の各Fieldを持つ。

**Reason:** Rule Model（規則モデル）の必須要素を文書上の明示的な記述単位へ対応させ、要素の欠落を検出可能にする。Fieldとして明示しない限り、要求水準やReasonは本文へ埋没し、後からの検証・再評価ができなくなる。

#### CVA-SF-012 — Optional Note Field（任意のNote Field）

**Rule ID:** `CVA-SF-012`

**Rule Name:** Optional Note Field

**Stability:** Development

**Requirement:** MUST

**Rule:** Normative Rule（規範的規則）にSupplementary Informationを含める場合は、`Note` Fieldとして記述する。`Note` Fieldは必須ではなく、不要な場合はField自体を省略する。

**Reason:** 補足の置き場所を1つに定めることで、非規範的内容がRule Statement（規則文）やReasonへ混入し、規範的効力を持つ範囲が曖昧になることを防ぐ。空のFieldを残さないのは、補足の有無をFieldの有無で判別できるようにするためである。

#### CVA-SF-013 — Rule Field Order（ルールフィールドの順序）

**Rule ID:** `CVA-SF-013`

**Rule Name:** Rule Field Order

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule Field（規則フィールド）は、`Rule ID` → `Rule Name` → `Stability` → `Requirement` → `Rule` → `Reason` → `Note`の順で記述する。

**Reason:** 順序を固定することで、複数のConvention Asset（規約資産）を横断して読む場合でも同じ位置に同じ要素が現れ、欠落や誤配置を目視でも機械的にも検出できる。

#### CVA-SF-014 — Rule Field Presentation（ルールフィールドの表示）

**Rule ID:** `CVA-SF-014`

**Rule Name:** Rule Field Presentation

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule Field（規則フィールド）は、Field名を `**<Field名>:**` の形で行頭に置き、その直後に値を記述する。Field間には空行を置く。`Rule ID` の値はInline Codeで表現する。

**Reason:** 表現を固定することで、Fieldの開始位置と値の範囲が一意に定まり、Heading（見出し）に依存せずRuleの内容を取り出せる。Rule Model（規則モデル）の要素と文書上の記述単位が対応するため、将来Machine-readable Structureが必要になった場合も、既存記述から変換可能な状態を保てる。

**Note:** 記述例は次である。

```text
**Rule ID:** `CVA-SF-001`

**Rule Name:** Convention Code Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** ...

**Reason:** ...

**Note:** ...
```

### Rule Stability（規則の安定性）

#### CVA-SF-015 — Initial Stability（初期のStability）

**Rule ID:** `CVA-SF-015`

**Rule Name:** Initial Stability

**Stability:** Development

**Requirement:** MUST

**Rule:** 新規に追加するNormative Rule（規範的規則）は、`Stability: Development` として記述する。

**Reason:** Rule ID（規則ID）を再編してよいかは、Stable Releaseの有無で決まる。初期値を `Development` に固定することで、未リリースのRule ID（規則ID）が誤って永続化済みとして扱われることを防ぐ。

#### CVA-SF-016 — Stable Transition（Stableへの遷移）

**Rule ID:** `CVA-SF-016`

**Rule Name:** Stable Transition

**Stability:** Development

**Requirement:** MUST

**Rule:** Stable ReleaseされたRuleは`Stability: Stable` とし、以後 `Development` へ戻さない。

**Reason:** `Stable` は、そのRule ID（規則ID）がすでに外部から参照され得ることを示す。`Development` へ戻せてしまえば再採番の余地が復活し、永続化されたはずのRule Identity（規則同一性）の保証が失われる。

#### CVA-SF-017 — Development Rule ID Changes（Development時の規約ルールID変更）

**Rule ID:** `CVA-SF-017`

**Rule Name:** Development Rule ID Changes

**Stability:** Development

**Requirement:** MAY

**Rule:** `Stability: Development` のRuleのRule ID（規則ID）は、Stable Release前であれば削除または再採番できる。欠番を詰めることは要求しない。

**Reason:** 設計途上での再編を許容しなければ、暫定的な番号割当が不必要に固定される。一方で欠番の解消を義務づけると、整理のたびに広範な書き換えが生じるため、許容に留める。

#### CVA-SF-018 — Stable Rule ID Preservation（Stableな規約ルールIDの保持）

**Rule ID:** `CVA-SF-018`

**Rule Name:** Stable Rule ID Preservation

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** `Stability: Stable` のRule ID（規則ID）を再採番してはならず、他のRuleへ再利用してもならない。新しいNormative Meaning（規範的意味）には、新しいRule ID（規則ID）を割り当てる。

**Reason:** 永続化されたRule ID（規則ID）が別の意味へ振り替わると、過去の参照が気づかれないまま異なる規範を指すようになる。新しい意味へ新しいRule ID（規則ID）を割り当てることで、参照先の意味が後から静かに変わることを防ぐ。

### Number Allocation（番号割当）

#### CVA-SF-019 — New Rule Number Allocation（新規Rule Numberの割当）

**Rule ID:** `CVA-SF-019`

**Rule Name:** New Rule Number Allocation

**Stability:** Development

**Requirement:** MUST

**Rule:** 新規Ruleには、同一の `Convention × Namespace` においてCurrent Rule IDまたはRetired Rule ID（廃止済み規則ID）として使用されている最大のRule Numberの次の番号を割り当てる。

**Reason:** 割当元をCurrentとRetiredの双方から取ることで、削除済みRule ID（規則ID）の再利用が採番手順の側から生じないようにする。最大値の次という一意の手順とすることで、番号の選択に判断の余地を残さない。

**Note:** 本Ruleは通常の新規追加を対象とする。`Stability: Development` のRuleに対する再採番・整理は、これと区別する。

### Rule Retirement（規則の廃止）

#### CVA-SF-020 — Stable Rule Retirement（Stableなルールの廃止）

**Rule ID:** `CVA-SF-020`

**Rule Name:** Stable Rule Retirement

**Stability:** Development

**Requirement:** MUST

**Rule:** `Stability: Stable` のRuleをCurrent Normative Ruleから削除する場合は、そのRuleのSectionを削除したうえで、Rule ID（規則ID）をRetired Rule ID（廃止済み規則ID）として保持する。

**Reason:** Rule ID（規則ID）の記録が残らなければ、その番号が過去に使用されたことを後から確認できず、再利用が起こり得る。Rule本体を残さないのは、廃止された規範が現在の規範として読まれることを防ぐためである。

#### CVA-SF-021 — Retired Rule ID Record（廃止済み規約ルールIDの記録）

**Rule ID:** `CVA-SF-021`

**Rule Name:** Retired Rule ID Record

**Stability:** Development

**Requirement:** MUST

**Rule:** Retired Rule ID（廃止済み規則ID）は、`Retired Rule IDs` の記録にRule ID（規則ID）として保持する。この記録は、Retired Rule ID（廃止済み規則ID）が存在する場合にのみ設ける。旧Rule Name（規則名）、旧Rule Statement（規則文）等の保持は要求しない。

**Reason:** 記録場所を1箇所に定めることで、採番時に参照すべき対象が明確になる。保持対象をRule ID（規則ID）に限るのは、この記録の目的が再利用の防止であり、廃止された規範内容の保存ではないためである。

**Note:** 最小の記録形式は次である。

```text
## Retired Rule IDs

- `CVA-SF-003`
- `CVA-SF-006`
```

#### CVA-SF-022 — Development Rule Removal（Development時のルール削除）

**Rule ID:** `CVA-SF-022`

**Rule Name:** Development Rule Removal

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Stable Release前に`Stability: Development` のRuleを削除した場合、そのRule ID（規則ID）についてRetired Rule ID（廃止済み規則ID）を作成してはならない。

**Reason:** Stable Release前のRule ID（規則ID）は、Stable Reference（安定参照）として永続化されていないため、削除後のIdentity（同一性）を将来にわたって保持する必要がない。これをRetired Rule ID（廃止済み規則ID）として記録すると、永続化されていない番号までStable Rule IDと同様に再利用不可となり、Development Versionに認められた再編の自由を不要に失わせる。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、自身が定めるRuleに従って記述されている。

- Convention Code（規約コード）を「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が`CVA-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）のRule Section（ルールSection）が、`Rule ID — Rule Name（Primary Language Heading Explanation）` の形式のHeading（見出し）を持つ。
- すべてのNormative Rule（規範的規則）が、必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が`Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、`Retired Rule IDs` の記録を設けていない。

本節はNon-normative Content（非規範的内容）であり、新たなNormative Requirement（規範要求）を追加しない。
