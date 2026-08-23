# Convention Authoring Convention（規約記述規約）

## Purpose（目的）

本文書は、`noxris42` において
**Convention（規約）をどのように記述するか** を定める
Convention Asset（規約資産）である。

[Convention Architecture](../architecture/convention.md)
は、Convention（規約）とNormative Rule（規範的ルール）の意味、
Rule Model（ルールモデル）、Requirement Level（要求レベル）、
Rule Identity（ルール同一性）とその安定性を定義する。
ただし同Architectureは、
それらを **どのような表記へ落とすか** を意図的に定義しない。

本文書はその委譲先として、
Convention Architecture（規約アーキテクチャ）が定義する
Convention（規約）およびRule Model（ルールモデル）を、
Convention Asset（規約資産）上で
**明示的・一貫的・安定参照可能に表現するための
Reusable Normative Standard（再利用可能な規範標準）**
を定義する。

本文書は、Convention Architecture（規約アーキテクチャ）が定義する
Concept（概念）を再定義しない。
本文書が定めるのは表記および記述運用に限られる。

## Position（上位Architectureとの関係）

本文書は
[Convention Architecture](../architecture/convention.md)
を上位Source（上位の情報源）として参照する。

Design Dependency（設計依存）は
**Convention Architecture → 本文書**
の一方向とする。

```text
Convention Architecture（意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（記述表記）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は
Convention Architecture（規約アーキテクチャ）にある。
本文書はこれらを参照するのみで、再定義しない。

- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的ルール）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（ルールモデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（ルール同一性）の意味上の構成
- Definition Namespace（定義名前空間）の意味と、
  そこから関係を推論しないこと
- Rule Identity Stability（ルール同一性の安定性）の原則

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Convention Code（規約コード）のConcrete Representation（具体表現）
- Rule ID Format（規約ルールID形式）
- Namespace Code（名前空間コード）のConcrete Representation（具体表現）
- Rule Number（ルール番号）の表記と採番
- Rule Field（規則フィールド）の構成・順序・Markdown表現
- Rule Boundary（規則境界）の取り方
- Stability（安定性）のField表現とその遷移
- Rule ID Stability Operation（規約ルールID安定運用）
- Retired Rule ID（廃止済み規約ルールID）の記録方法
- 現在必要なConcrete Identifier Declaration（具体識別子宣言）

### Out of Scope（本文書が定義しない範囲）

- Convention（規約）そのものの意味、
  Normative Rule（規範的ルール）の意味、
  Requirement Level（要求レベル）の意味
- Rule Identity（ルール同一性）および
  Rule Identity Stability（ルール同一性の安定性）の
  Semantic Model（意味モデル）
- Definition Namespace（定義名前空間）の一般的な成立条件・付与方法
- Convention Application（規約適用）、
  Override（上書き）／Extension（拡張）等の
  Rule Relationship（ルール間関係）
- 一般的なMarkdown規約
- 一般的なDocumentation Section Structure（文書セクション構造）、
  およびHeading Level（見出しレベル）の固定
- Naming Convention（命名規約）一般
- Navigation / Index（案内・索引）および
  Convention Registry（規約登録簿）
- Metadata（構造化メタデータ）／Declaration Schema、
  JSON / YAML等のMachine-readable Structure（機械可読構造）
- Release Management（リリース管理）、Version表記、Tag運用
- Commit Convention（コミット規約）等、
  個別Convention（規約）固有のRule（規則）

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

Normative Rule（規範的ルール）が定めるのは
識別子の形式および使用条件であり、
どの値を割り当てるかは本節の宣言による。
両者を混同しない。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CVA
```

### Namespace Code Assignment（名前空間コード割当）

現在割り当てられているNamespace Code（名前空間コード）は次である。

```text
SF = Shared Foundation Namespace（共有基盤名前空間）
```

現時点で割当済みのNamespace Code（名前空間コード）は `SF` のみである。
将来Namespace Code（名前空間コード）が追加され得るが、
どのような拡張単位が成立し、
Definition Namespace（定義名前空間）がどのように付与されるかは、
本文書では定義しない。

## Authoring Concepts（本文書が定義する記述上の概念）

本節は、本文書が所有する記述上のConcept（概念）を示す。
上位Architectureが定義するConcept（概念）を再定義するものではない。

### Rule ID（規約ルールID）

Rule ID（規約ルールID）は、
Convention Architecture（規約アーキテクチャ）が定義する
Rule Identity（ルール同一性）の
Concrete Representation（具体表現）である。

意味上の構成要素との対応は次である。

| Rule Identityの構成要素 | Rule ID上のSegment（構成要素） |
| --- | --- |
| Convention Identity（規約同一性） | Convention Code（規約コード） |
| Definition Namespace（定義名前空間） | Namespace Code（名前空間コード） |
| Rule-local Identity（ルール内同一性） | Rule Number（ルール番号） |

### Stability（安定性）

Stability（安定性）は、
Convention Architecture（規約アーキテクチャ）が定める
Development Version（開発版）／Stable Version（安定版）の境界を、
個々のNormative Rule（規範的ルール）上で明示するための
Field（フィールド）である。

値は次の2つに限られる。

| 値 | 意味 |
| --- | --- |
| `Development` | Stable Release（安定版リリース）前であり、Rule ID（規約ルールID）を再編できる状態 |
| `Stable` | Stable Release（安定版リリース）済みであり、Rule ID（規約ルールID）が永続化された状態 |

遷移は一方向である。

```text
Development
    ↓ Stable Release（安定版リリース）
Stable
```

Release（リリース）の手続き、Version表記、Tag運用は本文書では定義しない。

### Retired Rule ID（廃止済み規約ルールID）

Retired Rule ID（廃止済み規約ルールID）は、
`Stable` となった後にCurrent Normative Rule（現在の規範的ルール）から
削除され、再利用不可となったRule ID（規約ルールID）を保持する
**Non-normative Record（非規範的記録）** である。

Retired Rule ID（廃止済み規約ルールID）は
`Stability` の値ではなく、
Rule Lifecycle State（ルールライフサイクル状態）でもない。
記録されるのはRule ID（規約ルールID）だけであり、
Rule（ルール）そのものはすでに存在しない。

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

各Rule（ルール）の見出しは
Rule Boundary（規則境界）とDocument Presentation（文書表現）のためにあり、
Rule Model（ルールモデル）のCanonical Representation（正規表現）ではない。
Rule（ルール）の内容は、
見出しではなくField（フィールド）によって確定する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Convention Identification（規約識別）

#### CVA-SF-001 — Convention Code Declaration

**Rule ID:** `CVA-SF-001`

**Rule Name:** Convention Code Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Convention Asset（規約資産）は、
自身を識別するConvention Code（規約コード）を1つ、
その資産上で明示的に宣言する。

**Reason:** Rule ID（規約ルールID）はConvention Code（規約コード）を
先頭Segment（構成要素）として含む。
Code（コード）がFile名やDocument Title（文書タイトル）からの推論に依存すると、
配置や題名の変更でRule ID（規約ルールID）の解釈が揺らぐ。
明示的宣言により、
Rule ID（規約ルールID）の解釈を資産自身の記述だけで確定させる。

#### CVA-SF-002 — Convention Code Format

**Rule ID:** `CVA-SF-002`

**Rule Name:** Convention Code Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Convention Code（規約コード）は、
ASCII大文字英字3文字で表現する。

**Reason:** 文字種と桁数を固定することで、
Rule ID（規約ルールID）のSegment（構成要素）を
表記だけで判別できる。
同一Convention（規約）に対して
長短の異なるCode（コード）表記が併存することも防ぐ。

#### CVA-SF-003 — Convention Code Stability

**Rule ID:** `CVA-SF-003`

**Rule Name:** Convention Code Stability

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Stable Rule ID（安定済み規約ルールID）の一部として使用された
Convention Code（規約コード）を変更してはならない。

**Reason:** Convention Code（規約コード）の変更は、
すでに永続化されたすべてのRule ID（規約ルールID）を一括で無効化する。
これはRule Identity（ルール同一性）を永続化する原則に反し、
既存の参照を失わせる。

### Rule Identifier（規約ルール識別子）

#### CVA-SF-004 — Rule ID Requirement

**Rule ID:** `CVA-SF-004`

**Rule Name:** Rule ID Requirement

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的ルール）は、
完全なRule ID（規約ルールID）を持たなければならない。

**Reason:** Rule Identity（ルール同一性）は
Normative Rule（規範的ルール）の必須要素である。
Rule ID（規約ルールID）を欠くRule（ルール）は
見出し・配置・Rule Name（ルール名）でしか参照できず、
Stable Reference（安定参照）が成立しない。

#### CVA-SF-005 — Rule ID Structure

**Rule ID:** `CVA-SF-005`

**Rule Name:** Rule ID Structure

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規約ルールID）は、
`<Convention>`、`<Namespace>`、`<Number>` の3つのSegment（構成要素）を
ハイフンで連結した `<Convention>-<Namespace>-<Number>` の形式で表現する。

**Reason:** Rule Identity（ルール同一性）の意味上の構成要素である
Convention Identity（規約同一性）・Definition Namespace（定義名前空間）・
Rule-local Identity（ルール内同一性）を、
表記上も1対1で対応させる。
構造を固定することで、
Rule ID（規約ルールID）から所属Convention（規約）と
Namespace（名前空間）を判別できる。

**Note:** 具体形式は `CCC-NN-NNN` となる。
例：`CVA-SF-001`。

#### CVA-SF-006 — Convention Segment

**Rule ID:** `CVA-SF-006`

**Rule Name:** Convention Segment

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規約ルールID）の `<Convention>` には、
そのRule（ルール）が属するConvention Asset（規約資産）が
宣言したConvention Code（規約コード）を使用する。

**Reason:** 宣言された値以外を使用すると、
Rule ID（規約ルールID）が指すConvention（規約）を
資産の宣言から確定できなくなる。
宣言と使用を一致させることで、
Rule ID（規約ルールID）の解決先が一意に定まる。

#### CVA-SF-007 — Namespace Segment

**Rule ID:** `CVA-SF-007`

**Rule Name:** Namespace Segment

**Stability:** Development

**Requirement:** MUST

**Rule:** Namespace Code（名前空間コード）はASCII大文字英字2文字で表現し、
Rule ID（規約ルールID）の `<Namespace>` には、
そのRule（ルール）が属するDefinition Namespace（定義名前空間）へ
割り当てられたNamespace Code（名前空間コード）を使用する。

**Reason:** Definition Namespace（定義名前空間）は
Rule Identity（ルール同一性）の構成要素であり、
表記上も区別できなければRule ID（規約ルールID）が衝突し得る。
割当済みCode（コード）に限定するのは、
その場限りのCode（コード）が増えて識別性が失われることを防ぐためである。

**Note:** 現在割り当てられているNamespace Code（名前空間コード）は
「Namespace Code Assignment（名前空間コード割当）」に示す。

#### CVA-SF-008 — Rule Number Format

**Rule ID:** `CVA-SF-008`

**Rule Name:** Rule Number Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule ID（規約ルールID）の `<Number>` は、
同一の `Convention × Namespace` における
Rule-local Identity（ルール内同一性）として、
`001` から始まる3桁ゼロ埋めの十進数で表現する。

**Reason:** 桁数を固定しない番号は、
`1` と `01` のように同一Rule（ルール）へ複数の表記を生じさせ、
参照の一致判定を壊す。
開始値と桁数を固定することで、
Rule ID（規約ルールID）の表記が一意に定まる。

#### CVA-SF-009 — Opaque Rule Number

**Rule ID:** `CVA-SF-009`

**Rule Name:** Opaque Rule Number

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Rule Number（ルール番号）に、
Category（分類）、Document Order（文書順序）、
その他のSemantic Meaning（意味）を持たせてはならない。
Rule Number（ルール番号）は識別のみに用いる。

**Reason:** 番号へ意味を持たせると、
分類の見直しやSection（節）の並べ替えのたびに再採番の圧力が生じ、
Rule Identity（ルール同一性）の永続化と衝突する。
番号を識別専用に保つことで、
文書構成の変更がRule ID（規約ルールID）へ波及しない。

### Rule Presentation（規則記述形式）

#### CVA-SF-010 — Rule Section

**Rule ID:** `CVA-SF-010`

**Rule Name:** Rule Section

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的ルール）は、
独立したHeading Section（見出しセクション）として記述する。

**Reason:** Rule Boundary（規則境界）が曖昧だと、
どこまでが1つのNormative Rule（規範的ルール）かを判断できず、
規範的内容と非規範的内容の区別も失われる。
Section（節）単位に分けることで、境界が一意に定まる。

**Note:** Heading（見出し）はRule Boundary（規則境界）と
Document Presentation（文書表現）のためのものであり、
Rule Model（ルールモデル）のCanonical Representation（正規表現）ではない。
Heading Level（見出しレベル）およびHeading（見出し）の文字列形式は、
本Convention（規約）では固定しない。

#### CVA-SF-011 — Required Rule Fields

**Rule ID:** `CVA-SF-011`

**Rule Name:** Required Rule Fields

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Normative Rule（規範的ルール）は、
`Rule ID`、`Rule Name`、`Stability`、`Requirement`、`Rule`、`Reason`
の各Field（フィールド）を持つ。

**Reason:** Rule Model（ルールモデル）の必須要素を
文書上の明示的な記述単位へ対応させ、要素の欠落を検出可能にする。
Field（フィールド）として明示しない限り、
要求水準やReason（理由）は本文へ埋没し、
後からの検証・再評価ができなくなる。

#### CVA-SF-012 — Optional Note Field

**Rule ID:** `CVA-SF-012`

**Rule Name:** Optional Note Field

**Stability:** Development

**Requirement:** MUST

**Rule:** Normative Rule（規範的ルール）に
Supplementary Information（補足情報）を含める場合は、
`Note` Field（フィールド）として記述する。
`Note` Field（フィールド）は必須ではなく、
不要な場合はField（フィールド）自体を省略する。

**Reason:** 補足の置き場所を1つに定めることで、
非規範的内容がRule Statement（ルール文）やReason（理由）へ混入し、
規範的効力を持つ範囲が曖昧になることを防ぐ。
空のField（フィールド）を残さないのは、
補足の有無をField（フィールド）の有無で判別できるようにするためである。

#### CVA-SF-013 — Rule Field Order

**Rule ID:** `CVA-SF-013`

**Rule Name:** Rule Field Order

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule Field（規則フィールド）は、
`Rule ID` → `Rule Name` → `Stability` → `Requirement` →
`Rule` → `Reason` → `Note`
の順で記述する。

**Reason:** 順序を固定することで、
複数のConvention Asset（規約資産）を横断して読む場合でも
同じ位置に同じ要素が現れ、
欠落や誤配置を目視でも機械的にも検出できる。

#### CVA-SF-014 — Rule Field Presentation

**Rule ID:** `CVA-SF-014`

**Rule Name:** Rule Field Presentation

**Stability:** Development

**Requirement:** MUST

**Rule:** Rule Field（規則フィールド）は、
Field名を `**<Field名>:**` の形で行頭に置き、
その直後に値を記述する。
Field（フィールド）間には空行を置く。
`Rule ID` の値はInline Code（インラインコード）で表現する。

**Reason:** 表現を固定することで、
Field（フィールド）の開始位置と値の範囲が一意に定まり、
Heading（見出し）に依存せずRule（ルール）の内容を取り出せる。
Rule Model（ルールモデル）の要素と文書上の記述単位が対応するため、
将来Machine-readable Structure（機械可読構造）が必要になった場合も、
既存記述から変換可能な状態を保てる。

**Note:** 記述例は次である。

````text
**Rule ID:** `CVA-SF-001`

**Rule Name:** Convention Code Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** ...

**Reason:** ...

**Note:** ...
````

### Rule Stability（規則の安定性）

#### CVA-SF-015 — Initial Stability

**Rule ID:** `CVA-SF-015`

**Rule Name:** Initial Stability

**Stability:** Development

**Requirement:** MUST

**Rule:** 新規に追加するNormative Rule（規範的ルール）は、
`Stability: Development` として記述する。

**Reason:** Rule ID（規約ルールID）を再編してよいかは、
Stable Release（安定版リリース）の有無で決まる。
初期値を `Development` に固定することで、
未リリースのRule ID（規約ルールID）が
誤って永続化済みとして扱われることを防ぐ。

#### CVA-SF-016 — Stable Transition

**Rule ID:** `CVA-SF-016`

**Rule Name:** Stable Transition

**Stability:** Development

**Requirement:** MUST

**Rule:** Stable Release（安定版リリース）されたRule（ルール）は
`Stability: Stable` とし、以後 `Development` へ戻さない。

**Reason:** `Stable` は、そのRule ID（規約ルールID）が
すでに外部から参照され得ることを示す。
`Development` へ戻せてしまえば再採番の余地が復活し、
永続化されたはずのRule Identity（ルール同一性）の保証が失われる。

#### CVA-SF-017 — Development Rule ID Changes

**Rule ID:** `CVA-SF-017`

**Rule Name:** Development Rule ID Changes

**Stability:** Development

**Requirement:** MAY

**Rule:** `Stability: Development` のRule（ルール）の
Rule ID（規約ルールID）は、
Stable Release（安定版リリース）前であれば削除または再採番できる。
欠番を詰めることは要求しない。

**Reason:** 設計途上での再編を許容しなければ、
暫定的な番号割当が不必要に固定される。
一方で欠番の解消を義務づけると、
整理のたびに広範な書き換えが生じるため、許容に留める。

#### CVA-SF-018 — Stable Rule ID Preservation

**Rule ID:** `CVA-SF-018`

**Rule Name:** Stable Rule ID Preservation

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** `Stability: Stable` のRule ID（規約ルールID）を再採番してはならず、
他のRule（ルール）へ再利用してもならない。
新しいNormative Meaning（規範的意味）には、
新しいRule ID（規約ルールID）を割り当てる。

**Reason:** 永続化されたRule ID（規約ルールID）が別の意味へ振り替わると、
過去の参照が気づかれないまま異なる規範を指すようになる。
新しい意味へ新しいRule ID（規約ルールID）を割り当てることで、
参照先の意味が後から静かに変わることを防ぐ。

### Number Allocation（番号割当）

#### CVA-SF-019 — New Rule Number Allocation

**Rule ID:** `CVA-SF-019`

**Rule Name:** New Rule Number Allocation

**Stability:** Development

**Requirement:** MUST

**Rule:** 新規Rule（ルール）には、
同一の `Convention × Namespace` において
Current Rule ID（現在の規約ルールID）または
Retired Rule ID（廃止済み規約ルールID）として使用されている
最大のRule Number（ルール番号）の次の番号を割り当てる。

**Reason:** 割当元をCurrent（現在）とRetired（廃止済み）の双方から取ることで、
削除済みRule ID（規約ルールID）の再利用が
採番手順の側から生じないようにする。
最大値の次という一意の手順とすることで、
番号の選択に判断の余地を残さない。

**Note:** 本Rule（ルール）は通常の新規追加を対象とする。
`Stability: Development` のRule（ルール）に対する再採番・整理は、
これと区別する。

### Rule Retirement（規則の廃止）

#### CVA-SF-020 — Stable Rule Retirement

**Rule ID:** `CVA-SF-020`

**Rule Name:** Stable Rule Retirement

**Stability:** Development

**Requirement:** MUST

**Rule:** `Stability: Stable` のRule（ルール）を
Current Normative Rule（現在の規範的ルール）から削除する場合は、
そのRule（ルール）のSection（節）を削除したうえで、
Rule ID（規約ルールID）を
Retired Rule ID（廃止済み規約ルールID）として保持する。

**Reason:** Rule ID（規約ルールID）の記録が残らなければ、
その番号が過去に使用されたことを後から確認できず、再利用が起こり得る。
Rule（ルール）本体を残さないのは、
廃止された規範が現在の規範として読まれることを防ぐためである。

#### CVA-SF-021 — Retired Rule ID Record

**Rule ID:** `CVA-SF-021`

**Rule Name:** Retired Rule ID Record

**Stability:** Development

**Requirement:** MUST

**Rule:** Retired Rule ID（廃止済み規約ルールID）は、
`Retired Rule IDs` の記録にRule ID（規約ルールID）として保持する。
この記録は、
Retired Rule ID（廃止済み規約ルールID）が存在する場合にのみ設ける。
旧Rule Name（旧ルール名）、旧Rule Statement（旧ルール文）等の保持は
要求しない。

**Reason:** 記録場所を1箇所に定めることで、
採番時に参照すべき対象が明確になる。
保持対象をRule ID（規約ルールID）に限るのは、
この記録の目的が再利用の防止であり、
廃止された規範内容の保存ではないためである。

**Note:** 最小の記録形式は次である。

````text
## Retired Rule IDs

- `CVA-SF-003`
- `CVA-SF-006`
````

#### CVA-SF-022 — Development Rule Removal

**Rule ID:** `CVA-SF-022`

**Rule Name:** Development Rule Removal

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Stable Release（安定版リリース）前に
`Stability: Development` のRule（ルール）を削除した場合、
そのRule ID（規約ルールID）について
Retired Rule ID（廃止済み規約ルールID）を作成してはならない。

**Reason:** Stable Release（安定版リリース）前のRule ID（規約ルールID）は、
Stable Reference（安定参照）として永続化されていないため、
削除後のIdentity（同一性）を将来にわたって保持する必要がない。
これをRetired Rule ID（廃止済み規約ルールID）として記録すると、
永続化されていない番号までStable Rule ID（安定済み規約ルールID）と同様に
再利用不可となり、
Development Version（開発版）に認められた再編の自由を不要に失わせる。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
自身が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `CVA-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Field（フィールド）を規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
