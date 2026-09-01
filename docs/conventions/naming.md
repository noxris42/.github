# Naming Convention（命名規約）

## Purpose（目的）

本文書は、`noxris42` において
**Repository上で反復して使用されるPhysical Name（物理名称）について、
人間・AI・Toolが対象を一貫して識別・参照できる
安定したRepresentation（表現）を成立させる
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

加えて本文書は、
現在Semantic Need（意味上の必要性）が確認された
Symbolic Identifierの命名について、
必要な範囲で
Non-normative Naming Guidanceを提供し得る。

この2つは責務として分離される。

```text
Physical Name
    → Reusable Normative Standard

Symbolic Identifier
    → Non-normative Naming Guidance
```

現在、Symbolic Identifierについて本文書が保持するのは
「Convention Code Selection Guidance」のみであり、
これはNon-normative Content（非規範的内容）である。
本文書は
Symbolic Identifier Namingの
一般Ruleを定義しない。

本文書が扱う問いは次の3点である。

1. Repository側が綴りを選択できるNameは、
   どのような形式で表現されなければならないのか。
2. Physical Name（物理名称）は、
   対象を識別するために何を含んでいるべきなのか。
3. Concrete Spelling（具体表記）が
   External System等によって制約される場合、
   その適合はどう扱われるのか。

本文書はNamingのRepresentation（表現）のみを扱う。
本文書は
Logical Identity（論理的同一性）または
Responsibility（責務）の
Definition Authority（定義権限）を持たない。

次の境界を維持する。

```text
Physical Name  ≠ Logical Identity
Physical Name  ≠ Responsibility
Formal Name    ≠ Physical Name ≠ Identifier
```

Responsibility（責務）は
Naming Inputになり得るが、
Physical Name（物理名称）から
Responsibility（責務）を成立・推論させない。

## Relationships（関係）

本文書は、次を上位Sourceとして参照する。

- [Repository Governance](../architecture/repository-governance.md)
- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ refines
Naming Convention

Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Naming Convention
```

本文書は
[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Repository上で反復して成立するPhysical Name（物理名称）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Areaを代表・集約するAssetではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Logical Structure（論理構造）と
  Physical Representation（物理表現）の境界、
  および `Area ≠ Directory` ・ `Asset ≠ File`
- Logical Identity（論理的同一性）と、
  それをPhysical Location（物理配置）から導出しないこと
- Documentation Framework（文書体系）・
  Documentation Area（文書責務領域）・
  Documentation Asset（文書資産）と、
  それぞれのResponsibility（責務）
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的規則）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（規則モデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（規則同一性）とその安定性
- Rule ID Format（規則ID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  StabilityのField表現
- Namespace Code（名前空間コード）の割当

本文書は、これら上位設計が定義する
Logical Modelを再定義せず、
Physical Name（物理名称）側から
Logical Modelへ制約を課さない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository-controlled File Nameの
  Physical Naming Form
- Repository-controlled Directory Nameの
  Physical Naming Form
- Physical Name（物理名称）の識別性、および
  Path Contextにおける対象の区別
- Responsibility（責務）を
  Naming Inputとして利用する場合の境界
- External Naming Contractとの境界と、
  Repository-controlled Nameとの適用分離
- Name Selection Stability
- Existing Name Stability
- Convention Code Selectionに関する
  Non-normative Guidance

### Out of Scope（本文書が定義しない範囲）

- Logical Identity（論理的同一性）および
  Responsibility（責務）の成立条件
- Directory Structure、
  Repository Layout、
  およびLogical UnitとのMapping Rule（対応規則）
- File FormatおよびFile Extension Selection
- Formal Name（正式名称）のSemantic Model（意味モデル）
- Document Title（文書題名）、Heading Label（見出しラベル）等の
  Natural Language Representation（自然言語表現）、
  日英表記、文体、用語選択
- Programming Language固有のIdentifier（識別子）命名
- Branch / Tag / Version / Issue / Pull Request / Commitの命名
- Rule ID（規則ID）・Convention Code（規約コード）・
  Namespace Code（名前空間コード）のFormat
- Convention Code Uniquenessの量化範囲、
  およびConvention Registry
- Markdown Syntaxその他の記述媒体固有表現
- External Platformの
  予約名称・特別扱い名称の完全Catalog
- Validator / Linter / CI / Rename Automation

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: NAM
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Naming Concepts（本文書が用いる命名上の概念）

本節は、以降のNormative Rule（規範的規則）が
適用対象を区別するために用いる局所Concept（概念）を示す。
本節はNon-normative Content（非規範的内容）である。
ここで示すのは本文書が必要とする範囲の区別であり、
一般Naming Modelではない。

### Physical Name（物理名称）

Physical Name（物理名称）は、
Repository上でFile・Directory等の対象を
実際に指し示すために使用される
Concrete Spelling（具体表記）である。

Physical Name（物理名称）はRepresentation（表現）であり、
Logical Identity（論理的同一性）でも
Responsibility（責務）でもない。

### Repository-controlled Name（Repository管理名称）

Repository-controlled Nameは、
Concrete Spelling（具体表記）を
Repository側が選択できるPhysical Name（物理名称）である。

### Externally Constrained Name（外部制約名称）

Externally Constrained Name（外部制約名称）は、
External System、Platform、
Tool等が
Concrete Spelling（具体表記）へ
意味または制約を与えるPhysical Name（物理名称）である。

この場合、綴りの選択はRepository側の自由ではなく、
外部との契約に従属する。

### Application Separation in Physical Naming Form（Physical Naming Formにおける適用の分離）

Concrete Spelling（具体表記）をRepository側が決める名称と、
外部から制約される名称とでは、
Physical Naming Formの適用が分かれる。

```text
Repository-controlled File Name
    → NAM-SF-001

Repository-controlled Directory Name
    → NAM-SF-002

Externally Constrained Name
    → NAM-SF-004
```

`NAM-SF-004` は
`NAM-SF-001` ・ `NAM-SF-002` の
Exception Catalogではない。
両者は適用対象が異なる。

この図は、
Physical Naming Formに関する適用の分離を示すものであり、
本文書のすべてのRuleについての
Applicability Mapではない。
`NAM-SF-003` ・ `NAM-SF-005` ・ `NAM-SF-006` ・ `NAM-SF-007` の
適用対象は、各RuleのRule Statement（規則文）が定める。

## Convention Code Selection Guidance（規約コード選定の指針）

本節はNon-normative Content（非規範的内容）である。
Convention Code（規約コード）の
Format・使用条件・変更制約は
[Convention Authoring Convention](convention-authoring.md)
が所有する。
本節は新たなNormative Requirement（規範要求）を追加せず、
Convention Code Uniquenessに関する
Ruleも設けない。

Convention Code（規約コード）を選ぶ際、
現時点で有用と考えられる観点は次である。

- Formal Name（正式名称）の単純な頭字語である必要はない。
  CodeはFormal Name（正式名称）の短縮表記ではなく、
  Convention（規約）を識別するための値である。
- `Convention` 等のAsset Type（資産種別）を
  Codeへ必ず含める必要はない。
  Convention Asset（規約資産）であることは、
  Codeの桁を使わずとも既に確定している。
- SubjectまたはResponsibility（責務）を
  識別・想起しやすい3文字を優先する。
- 現在利用されているCodeと
  混同しにくい値を選ぶ。
- Formal Name（正式名称）が変更されたことだけを理由に
  Codeを自動的に変更しない。

Stable Rule IDで使用済みの
Convention Code（規約コード）に対する変更制約は、
[Convention Authoring Convention](convention-authoring.md)
のNormative Rule（規範的規則）による。
本節はそれを再定義しない。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規則ID）はCategory（分類）を表現しない。

### Physical Naming Form（物理命名形式）

#### NAM-SF-001 — File Name Form（File名の形式）

**Rule ID:** `NAM-SF-001`

**Rule Name:** File Name Form

**Stability:** Development

**Requirement:** MUST

**Rule:** Repository-controlled File Nameの
File Stemは、次を満たすように表現する。

- 英字を使用する場合は、小文字を使用する。
- 複数の語を区切る場合は、ハイフン `-` を使用する。

**Reason:** File Nameは、
Path・URL・CLI・Tool・AIといった異なる経路から
同一対象を参照するために使用される。
大文字・小文字の揺れや、
space・underscore・camelCase等の複数の表現方式が併存すると、
同じ対象に対する綴りが経路や記述者ごとに分岐し、
参照の一致判定と検索が成立しなくなる。
表記を1つに固定し、
単語境界をハイフンで明示することで、
どの経路からも同じ綴りで対象へ到達できる。

**Note:** 本Ruleが規定するのは、
Rule Statement（規則文）に挙げた2つの制約のみである。
`lowercase kebab-case` は、
その形を想起するためのNon-normative Labelとして
用いることができるが、
本RuleのNormative Meaning（規範的意味）は
その一般用語の解釈ではなく
Rule Statement（規則文）によって確定する。

次は本Ruleが定めない。

- 使用可能なCharacter Set、
  および言語・文字種の限定
- 数字その他の文字を使用してよいか
- File Extensionの種類および選択

Externally Constrained Name（外部制約名称）は
本Ruleの対象ではなく、
`NAM-SF-004` が扱う。

#### NAM-SF-002 — Directory Name Form（Directory名の形式）

**Rule ID:** `NAM-SF-002`

**Rule Name:** Directory Name Form

**Stability:** Development

**Requirement:** MUST

**Rule:** Repository-controlled Directory Nameは、
次を満たすように表現する。

- 英字を使用する場合は、小文字を使用する。
- 複数の語を区切る場合は、ハイフン `-` を使用する。

**Reason:** Directory NameはPathの構成要素として、
File Nameと同じ経路から参照される。
Path内で表記方式が要素ごとに異なると、
Path全体の綴りを記憶・再現できず、
File Name側で表記を固定した効果も失われる。
Path上のRepository-controlled Nameへ
同一の表記形式を適用することで、
Path全体が一貫した綴りとして扱える。

**Note:** 本Ruleが規定するのは、
Rule Statement（規則文）に挙げた2つの制約のみであり、
その内容は `NAM-SF-001` と同一のLexical Constraintである。
`lowercase kebab-case` は、
その形を想起するためのNon-normative Labelとして
用いることができるが、
本RuleのNormative Meaning（規範的意味）は
その一般用語の解釈ではなく
Rule Statement（規則文）によって確定する。

次は本Ruleが定めない。

- 使用可能なCharacter Set、
  および言語・文字種の限定
- 数字その他の文字を使用してよいか
- Directoryの責務、配置、
  およびDocumentation Area（文書責務領域）等の
  Logical UnitとのMapping

Externally Constrained Name（外部制約名称）は
本Ruleの対象ではなく、
`NAM-SF-004` が扱う。

### Name Identification（名称の識別性）

#### NAM-SF-003 — Responsibility-distinguishing Name（責務を区別する名称）

**Rule ID:** `NAM-SF-003`

**Rule Name:** Responsibility-distinguishing Name

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Repository-controlled Physical Nameは、
そのPath Contextにおいて
Subjectを示す語だけでは
異なるResponsibility（責務）を十分に区別できない場合、
区別に必要なResponsibility（責務）を表す語を含めるべきである。

**Reason:** Physical Name（物理名称）が果たすべきことは、
参照者が目的の対象へ到達できることである。
同一のSubjectについて
異なる責務を担う対象が複数成立し得る場合、
Subjectだけの名称では
どちらを指しているのかを名称から判別できず、
参照のたびに内容を開いて確かめることを要求する。
区別に必要な語を含めることで、
参照の時点で対象を特定できる。

**Note:** 本Ruleが求めるのは
識別に必要な区別であり、
Responsibility（責務）全体を名称へ符号化することではない。
Subjectだけで
そのPath Contextにおいて十分に識別できる場合、
追加の語は要求されない。

理解を助ける関係として、次が挙げられる。

```text
docs/conventions/commit.md
```

は、`commit` だけで現在の対象を十分に識別できる場合がある。
一方、

```text
documentation.md
```

より、

```text
documentation-structure.md
```

の方が、Documentationに関するどの責務を扱う対象なのかを
識別するために適切となり得る。
同様に、かつて

```text
docs/conventions/convention.md
```

であった資産について、その資産の責務が
Convention Authoringであることから、

```text
docs/conventions/convention-authoring.md
```

の方が識別上より適切であるという設計判断が成立した。
この資産のCurrent Physical Nameは後者であり、
前者は当該Rename以前の状態である。

本Ruleが扱う方向は次に限られる。

```text
Responsibility → Naming Input
Physical Name  → Representation

Physical Name  ✕→ Responsibility Definition
```

すなわち、Responsibility（責務）は
名称選択の入力になり得るが、
Physical Name（物理名称）から
Responsibility（責務）を成立させたり推論したりしない。
名称に語が含まれていないことは、
その責務が存在しないことを意味しない。

### External Naming Contract（外部命名契約）

#### NAM-SF-004 — External Naming Contract（外部命名契約）

**Rule ID:** `NAM-SF-004`

**Rule Name:** External Naming Contract

**Stability:** Development

**Requirement:** MUST

**Rule:** Concrete Spelling（具体表記）が
External System、Platform、
Tool等とのContractによって制約される
Externally Constrained Name（外部制約名称）は、
そのExternal Contractへ適合しなければならない。

**Reason:** Externally Constrained Name（外部制約名称）では、
綴りそのものが外部による認識の条件になっている。
Repository内部の表記上の都合で綴りを変更すると、
外部はその対象を認識できなくなり、
名称が成立させるはずの参照そのものが失われる。
適合を要求することで、
Repository内部の表記方針が
外部との契約を破壊しないようにする。

**Note:** 本Ruleは
`NAM-SF-001` ・ `NAM-SF-002` の
Exception Catalogではない。
Repository-controlled Nameと
Externally Constrained Name（外部制約名称）は
適用対象として分離されている。

本Ruleは、
どのNameが
Externally Constrained Name（外部制約名称）に当たるかの
完全なCatalogを保持しない。
適合すべきContractの内容は
そのExternal System側にあり、
本文書がそれを複製・代理しない。

### Name Stability（名称の安定性）

#### NAM-SF-005 — Stable Name Selection（安定した名称の選択）

**Rule ID:** `NAM-SF-005`

**Rule Name:** Stable Name Selection

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Repository-controlled Nameは、
一時的な作業状態ではなく、
対象を継続的に識別できる比較的安定した特徴に基づいて
選択すべきである。

**Reason:** Physical Name（物理名称）は、
Path・Link・履歴・外部参照を通じて
選択の時点よりも長く使われ続ける。
選択の根拠が短期間で変化する特徴であれば、
名称は早期に対象を正しく識別しなくなり、
その時点で名称変更か、
実態と合わない名称の放置かのいずれかを強いる。
安定した特徴を根拠として選ぶことで、
その必要が初回のNamingの時点から生じにくくなる。

**Note:** 本Ruleは
初回のNamingにおける選択の根拠を対象とする。
既存名称を変更してよいかは `NAM-SF-006` が扱う。

#### NAM-SF-006 — Existing Name Stability（既存名称の安定性）

**Rule ID:** `NAM-SF-006`

**Rule Name:** Existing Name Stability

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 既存の参照で使用されている
Physical Name（物理名称）は、
その名称が現在の対象を十分に識別している限り、
明確な理由なく変更すべきではない。

**Reason:** Physical Name（物理名称）の変更は、
その名称を用いている既存の参照を同時に無効化する。
識別上の改善を伴わない変更は、
参照の破壊という費用だけを生じさせる。
変更に理由を求めることで、
名称の変更が識別性の改善と引き換えに行われるようにする。

**Note:** Name Stabilityは
Immutable Namingではない。
名称が現在の対象を十分に識別できない場合、
または対象を誤認させる場合は、
識別精度を改善するRenameが妥当になり得る。
本Ruleが抑止するのは、
識別上の理由を持たない変更である。

#### NAM-SF-007 — Temporary State Naming（一時的な作業状態の命名）

**Rule ID:** `NAM-SF-007`

**Rule Name:** Temporary State Naming

**Stability:** Development

**Requirement:** SHOULD NOT

**Rule:** 一時的な作業状態だけを区別する目的で、
その状態を
Repository-controlled Nameへ
埋め込むべきではない。

**Reason:** 作業状態は作業の進行によって変化するが、
名称へ埋め込まれた状態は変化しない。
その結果、名称は現在の状態を誤って示すか、
状態が変わるたびに名称変更を要求するかのいずれかになり、
どちらの場合も名称が対象を識別する働きを損なう。
状態は名称ではなく、
状態を保持できる手段によって区別されるべきである。

**Note:** 本Ruleが対象とするのは
Naming Reasonであり、
特定の語ではない。
本Ruleは
Prohibited Word Catalogを定義しない。

したがって、ある語が
一時的な作業状態ではなく
Subject Identityの一部として成立している場合、
その語を名称へ含めることは本Ruleの対象ではない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRuleに従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が
  `NAM-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）が、
  必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書自身のPhysical Name（物理名称）は、
本文書が定めるRuleに従っている。

- File Stemは
  英字をすべて小文字で表記している。
- 現在のPath Contextにおいて、
  `naming` はその対象を十分に識別している。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
