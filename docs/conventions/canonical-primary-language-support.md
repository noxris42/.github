# Canonical Primary Language Support Convention（正規主要言語補助規約）

## Purpose（目的）

本文書は、`noxris42` において
**[Canonical Primary Language Support Architecture](../architecture/canonical-primary-language-support.md)
上で成立するCanonical Primary Language Support Association（正規主要言語補助対応）について、
Candidate Recommendation（候補提案）と
Canonical Declaration（正規宣言）を一貫して扱うための
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の3点である。

1. 成立したCanonical Primary Language Support Association（正規主要言語補助対応）は、
   どこに、どのようなConcrete Representation（具体表現）で
   Canonical Declaration（正規宣言）として保持されるのか。
2. Canonical Primary Language Support Association（正規主要言語補助対応）の
   Candidate Recommendation（候補提案）は、
   何を優先して行い、
   何を根拠として対象から除外しないのか。
3. Candidate Recommendation（候補提案）と
   Canonical Association Establishment（正規対応成立）は、
   どこで分かれるのか。

本文書が定義するのは、この3点に関するRuleに限られる。
本文書は、English Representation（英語表現）そのものの
Identity（同一性）・Meaning（意味）・Formal Status（正式地位）・
Category（分類）、および
Underlying Meaning（対象の意味）を対象としない。
Documentation Presentation（文書上の表示）、
Human Review Workflow、
Lifecycle等も対象としない。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は、次を上位Sourceとして参照する。

- [Canonical Primary Language Support Architecture](../architecture/canonical-primary-language-support.md)
- [Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Canonical Primary Language Support Architecture
        ▲
        │ refines
Canonical Primary Language Support Convention

Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Canonical Primary Language Support Convention
```

本文書は
[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Canonical Primary Language Support Association（正規主要言語補助対応）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Areaを代表・集約するAssetではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- English Representation（英語表現）が
  本Modelにおいて対応元として扱われること、および
  そのIdentity（同一性）・Meaning（意味）を
  Canonical Primary Language Support（正規主要言語補助）が定義しないこと
- Canonical Primary Language Support Representation（正規主要言語補助表現）の意味
- Canonical Primary Language Support Association（正規主要言語補助対応）の意味、
  およびその成立
- 同Association（対応）のMultiplicity（多重度）
- Canonical Primary Language Support Association（正規主要言語補助対応）の成立と
  Documentation Presentation（文書上の表示）との
  Boundary（境界）
- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Definition Authority（定義権限）
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

### Responsibility Boundary（責務境界）

Canonical Primary Language Support（正規主要言語補助）に関する
Definition Authority（定義権限）は次のように分離される。
本文書は、上位および隣接する責務を補完しない。

```text
Canonical Primary Language Support Associationの
Semantic Model・Boundary
    → Canonical Primary Language Support Architecture

English Representationそのもの、および
Underlying Meaning
    → それぞれの対象を所有する既存のDefinition Authority

Canonical Declarationの保持と反復規則、
Candidate Recommendationの規則、および
Candidate Recommendationと
Canonical Decisionとの分離
    → 本文書

個々のCanonical Primary Language Support Associationの値
    → Central Concrete Declaration Source

Documentation Presentation
    → Presentation Ruleを所有するConvention
```

本文書が保持する境界は次である。

```text
Candidate Recommendation
≠ Canonical Association Establishment
≠ Documentation Presentation
```

Documentation Presentation（文書上の表示）は本文書の責務ではない。
Current Repositoryにおいて
Human-readable Natural Language Representation（人間可読な自然言語表現）を
対象とするのは
[Writing Convention](writing.md)
であり、本文書はそのRuleを前提とせず、
変更・再定義もしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 成立したCanonical Primary Language Support Association（正規主要言語補助対応）を
  Central Concrete Declaration Source（中央具体宣言情報源）へ
  Canonical Declaration（正規宣言）として保持すること
- 各Canonical Declaration（正規宣言）が表現する
  Semantic Content
- Canonical Declaration（正規宣言）の
  Concrete Representation（具体表現）
- Candidate Recommendation（候補提案）において
  何を優先して提案するか
- Candidate Recommendation（候補提案）の対象から
  除外してはならない根拠
- Candidate Recommendation（候補提案）と
  Canonical Association Establishment（正規対応成立）との
  Boundary（境界）

### Out of Scope（本文書が定義しない範囲）

- English Representation（英語表現）のIdentity（同一性）、
  Meaning（意味）、Formal Status（正式地位）、Category（分類）
- English Representation（英語表現）が指す
  Underlying Meaning（対象の意味）
- Presentation Rule、および
  Title・Heading（見出し）・Body等における表示条件
- Registration Qualification、
  Occurrence Threshold、
  Candidate Score
- Candidate Recommendation（候補提案）を行う
  AI-specific Algorithm
- Human Review Workflow、
  Actor Model、
  Approval / Rejection State、
  Rejected Candidate History、
  Permanent Exclusion
- Stable Identifier、
  Alias / Synonym
- Lifecycle、Versioning（版管理）
- 本文書が定めるもの以外の
  Additional YAML Field
- 一般的なYAML記述規約、
  およびYAML機能全般に対する禁止／許可Catalog
- Validator・Linter・CLI・CI等のTool要求
- Central Concrete Declaration Source（中央具体宣言情報源）の
  Asset Name・Path・
  Asset Type（資産種別）に関する一般Rule

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CPL
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

### Central Concrete Declaration Source（中央具体宣言情報源）

Current Repositoryにおいて
`CPL-SF-001` が要求する
Central Concrete Declaration Source（中央具体宣言情報源）の役割を
担うAssetは次である。

```text
docs/canonical-primary-language-support.yaml
```

本宣言はCurrent Repositoryにおける
Concrete Source Assignmentの値のみを示す。
Central Concrete Declaration Source（中央具体宣言情報源）に関する
Naming Rule（命名規則）・Path Rule・
Asset Type Rule等の一般Ruleは、
本宣言によって成立しない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的規則）が
対象を指すために用いる局所的な区別を示す。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。

本節は新たなArchitecture-level Conceptを
定義しない。

### Central Concrete Declaration Source（中央具体宣言情報源）

Central Concrete Declaration Source（中央具体宣言情報源）は、
成立したCanonical Primary Language Support Association（正規主要言語補助対応）の
Canonical Declaration（正規宣言）を
Repository内で中央に保持する
Central Locationである。

本文書は、この保持場所の
Asset NameおよびPathに関する
一般Ruleを定めない。
Current Repositoryにおいて
この役割を担うAssetの具体値は、
「Concrete Declarations」が宣言する。

### Canonical Declaration（正規宣言）

Canonical Declaration（正規宣言）は、
Central Concrete Declaration Source（中央具体宣言情報源）において
1つのCanonical Primary Language Support Association（正規主要言語補助対応）について
記述される保持の単位である。

### Candidate Recommendation（候補提案）

Candidate Recommendation（候補提案）は、
あるEnglish Representation（英語表現）について
Canonical Primary Language Support Association（正規主要言語補助対応）を
成立させることを提案する行為である。

Candidate Recommendation（候補提案）は
Canonical Association Establishment（正規対応成立）への
Inputであり、
それ自体はCanonical Decision（正規判断）ではない。

この位置づけから、Candidate Recommendation（候補提案）が果たすのは、
判断の対象となり得るEnglish Representation（英語表現）を
Canonical Decision（正規判断）の前に見えるようにすることである。
どれを成立させるかを選び分けることではない。

本文書は、この位置づけを
Architecture-level Conceptとして
新たに導入しない。

## Candidate Recommendation Guidance（候補提案指針）

本節はNon-normative Content（非規範的内容）であり、
`CPL-SF-004` および `CPL-SF-006` の解釈補助として置かれる。
本節は新たなNormative Requirement（規範要求）を追加せず、
Registration Qualificationも定めない。

### Candidate Pool Breadth（候補集合の広さ）

Candidate Recommendation（候補提案）が生む
Candidate Pool（候補集合）は、
Canonical Decision（正規判断）を受ける前の集合である。
したがって、そこへ現れることは
成立の見込みが高いことを意味しない。

`CPL-SF-004` が述べるのは提案の優先であり、
提案順序または提示上の強調として働く。
優先度が低いことは、
Candidate Pool（候補集合）へ現れないことを意味しない。
`CPL-SF-006` は、成立の見込みが低い・不明であることのみを根拠として
Candidate Pool（候補集合）から落とすことを禁じる。

```text
低い優先度
≠ Candidate Poolからの除外
```

これは、次のような
English Representation（英語表現）が
Canonical Decision（正規判断）を受けないまま
Candidate Pool（候補集合）から消えることを防ぐためのものである。

- 1つのDocumentation Asset（文書資産）にのみ現れる
- Out of Scopeの列挙等、
  対象外を示す文脈で現れる
- Repository横断の概念ではなく、
  局所的な区別として現れる
- Primary Languageによる補助を定める価値があるかどうかが判断しにくい

一方、Candidate Pool（候補集合）は
Repository Documentation（Repository文書）に現れる
英語表記の網羅一覧ではない。
`CPL-SF-006` はCompletenessを要求せず、
Primary Language Reading Supportの対象でないことが明らかな
Literal Representation（そのままの表記）まで
提案対象へ含めることも求めない。

### Potential Candidate Signals（候補になり得るSignal）

次は、Candidate Recommendation（候補提案）の優先を考える際に
現時点で有用と考えられる観点である。
いずれもRequirementではなく、
Candidate Pool（候補集合）へ入るための条件でもない。
ここに挙げた観点へ当てはまらないことは、
提案対象から外す根拠にならない。

- Concept（概念）・Responsibility（責務）・Role・
  Relationship・Principle等の理解に
  Primary Languageによる補助が有用である。
- Document Title（文書題名）およびHeading Label（見出しラベル）等、
  文書の理解上重要な位置で使用されている。
- Primary Language Representation（主要言語表現）が複数考えられ、
  1つのCanonical Primary Language Support Representation（正規主要言語補助表現）を
  定めることで表現の揺れを抑えられる。
- 複数のUsage Occurrenceがあり、
  一貫したPrimary Languageによる補助の価値が高い。

### Occurrence Count Handling（Occurrence Countの扱い）

Occurrence Count（出現回数）は
Candidate Qualificationではない。

```text
Occurrence Count
≠ Candidate Qualification
```

1回のみ登場するHeading Label（見出しラベル）であっても
候補になり得る。
例として `Design Principles` のような
Heading Label（見出しラベル）が挙げられる。

### Code Block Handling（Code Blockの扱い）

Code Block内に現れることは、
それだけで候補から除かれることを意味しない。

```text
Code Block placement
≠ automatic exclusion
```

一方、Code・Identifier（識別子）・Path等として機能する
Literal Representation（そのままの表記）は、
自然言語による理解を補助する対象でない場合、
通常はCandidate Recommendation（候補提案）の優先対象としない。

これはHard Exclusion Ruleではない。

この扱いが `CPL-SF-006` と衝突しないのは、
除外の根拠が成立の見込みではないためである。

```text
Primary Language Reading Supportの対象でない
→ CPL-SF-006が禁じる除外根拠ではない

成立の見込みが低い・不明である
→ CPL-SF-006が禁じる除外根拠である
```

同じSurface Formが、
ある箇所ではCode等として、
別の箇所では自然言語の一部として現れることがある。
その場合、後者の使用があることをもって
候補になり得る。

### Definition-owned Representation Handling（Definition-owned Representationの扱い）

あるHuman-readable Representation（人間可読表現）が、
別のSubjectについての
Definition Responsibility（定義責務）によって
すでに定義されていることがある。
そのような箇所は
Canonical Primary Language Support（正規主要言語補助）の
Definition Authority（定義権限）の外にある。

この境界は
[Canonical Primary Language Support Architecture](../architecture/canonical-primary-language-support.md)
が保持するものであり、
Candidate Recommendation（候補提案）の段階で
判断を先取りする根拠にはならない。

同じEnglish Representation（英語表現）が、
定義済み表現が現れる箇所と、
Natural Language Prose（自然言語本文）とで
ともに使用されていることがある。
前者に該当する箇所があることは、
そのEnglish Representation（英語表現）全体が
Candidate Pool（候補集合）から外れることを意味しない。

```text
定義済み表現が現れる箇所がある
≠ 当該English RepresentationがCandidate Poolから外れる
```

どこまでが定義責務側の表現であり、
どこからがCanonical Primary Language Support Association（正規主要言語補助対応）の
対象であるかは、
Canonical Decision（正規判断）の側で確定する。

### Repeat Recommendation Handling（再提案の扱い）

過去にCandidateが採用されなかったことを
Permanent Rejectionとして扱うMechanismは、
本文書に存在しない。
同じEnglish Representation（英語表現）について
改めてCandidate Recommendation（候補提案）を行うことは妨げられない。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規則ID）はCategory（分類）を表現しない。

### Canonical Declaration（正規宣言）

#### CPL-SF-001 — Central Canonical Declaration（中央での正規宣言）

**Rule ID:** `CPL-SF-001`

**Rule Name:** Central Canonical Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** [Canonical Primary Language Support Architecture](../architecture/canonical-primary-language-support.md)
上で成立したCanonical Primary Language Support Association（正規主要言語補助対応）は、
Repository内の
Central Concrete Declaration Source（中央具体宣言情報源）へ
Canonical Declaration（正規宣言）として保持する。

**Reason:** 成立したCanonical Decision（正規判断）が
中央に保持されていなければ、
どのPrimary Language Representation（主要言語表現）を用いるかを
使用箇所ごとに記述者が改めて判断することになり、
同一のEnglish Representation（英語表現）に対して
異なるPrimary Languageによる補助が併存する。
Canonical Declaration（正規宣言）を1箇所へ集約することで、
すでに成立している決定を検索して再利用でき、
使用箇所ごとの再判断が生じない。

**Note:** 本Ruleが定めるのは
Canonical Declaration（正規宣言）の保持先である。
Central Concrete Declaration Source（中央具体宣言情報源）の
Asset Name、Path、
および具体的なAsset Type（資産種別）に関する
一般Ruleは、本Ruleでは定めない。
Current Repositoryにおける
Concrete Source Assignmentは
「Concrete Declarations」が宣言する。
本RuleのRequirementは
その具体値に依存しない。

保持されていることと、
Usage Occurrenceにおける
Documentation Presentation（文書上の表示）とは別である。
表示は本Ruleの対象ではない。

#### CPL-SF-002 — Canonical Association Declaration（正規対応の宣言）

**Rule ID:** `CPL-SF-002`

**Rule Name:** Canonical Association Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Canonical Declaration（正規宣言）は、
対象となるEnglish Representation（英語表現）と
Canonical Primary Language Support Representation（正規主要言語補助表現）との
Canonical Primary Language Support Association（正規主要言語補助対応）を
表現する。

**Reason:** Canonical Declaration（正規宣言）が保持すべき意味は、
Canonical Primary Language Support Association（正規主要言語補助対応）そのものである。
対応元と対応先のいずれかを欠く宣言は、
どのEnglish Representation（英語表現）に対して
どのPrimary Language Representation（主要言語表現）を
一貫して再利用するのかを確定させず、
中央から検索して再利用するという目的を満たさない。

**Note:** 意味上必要なのは次のAssociation（対応）である。

```text
English Representation
+
Canonical Primary Language Support Representation
```

本Ruleは、これ以外の要素を
Canonical Declaration（正規宣言）へ導入しない。
Stable Identifier、Category（分類）、
Formal Status（正式地位）、
Presentation Parameter等は含めない。

#### CPL-SF-003 — YAML Scalar Mapping Representation（YAML Scalar Mappingによる表現）

**Rule ID:** `CPL-SF-003`

**Rule Name:** YAML Scalar Mapping Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Central Concrete Declaration Source（中央具体宣言情報源）は
YAMLで表現する。
各Canonical Declaration（正規宣言）は、
English Representation（英語表現）を
Mapping Keyとし、
Canonical Primary Language Support Representation（正規主要言語補助表現）を
Scalar Valueとする
Scalar Mappingとして表現する。
Mapping KeyとScalar Valueは、
双方ともDouble-quoted Stringで表記する。

**Reason:** `CPL-SF-002` が要求するSemantic Contentは、
English Representation（英語表現）から
Canonical Primary Language Support Representation（正規主要言語補助表現）への
単純なAssociation（対応）である。
Scalar Mappingは、この意味内容を
余分な構造を挟まずそのまま表す最も直接的な形であり、
English Representation（英語表現）から
対応する値を検索する現在の利用に追加の対応表を要しない。
Double Quoteを要求するのは、
KeyとValueを常にStringとして明示し、
YAMLのImplicit Typingや特殊文字によって
不要な表記判断と揺れが生じることを抑えるためである。

**Note:** Canonical Shapeは次である。

```yaml
"Design Principles": "設計原則"
"Design Dependency": "設計依存"
```

Record Mappingは採用しない。
次の形は本Ruleに適合しない。

```yaml
"Design Principles":
  japanese: "設計原則"
```

Double Quoteの要求は、
空白を含む表記への対処を目的とするものではない。

本Ruleが定めるのは、
Central Concrete Declaration Source（中央具体宣言情報源）における
Canonical Declaration（正規宣言）の表現に限られる。
一般的なYAML Style Guideは定めない。

### Candidate Recommendation（候補提案）

#### CPL-SF-004 — Candidate Recommendation（候補提案）

**Rule ID:** `CPL-SF-004`

**Rule Name:** Candidate Recommendation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Candidate Recommendation（候補提案）を行う場合は、
Canonical Primary Language Support Representation（正規主要言語補助表現）を
定めることが、
そのEnglish Representation（英語表現）の理解補助、または
Repository Documentation（Repository文書）における
Primary Language Support Representationの一貫性に対して
意味を持つと合理的に見込まれるものを優先して提案する。

**Reason:** Candidate Recommendation（候補提案）は
Canonical Association Establishment（正規対応成立）への
Inputである。
理解補助にも一貫性にも寄与しない提案が積み上がると、
判断すべき対象が増えるだけで
成立するCanonical Decision（正規判断）の価値は高まらず、
提案そのものが読み手の負担になる。
寄与が見込まれるものを優先することで、
提案の量ではなくその効果へ労力が向く。
`SHOULD` とするのは、
何が理解補助または一貫性へ寄与するかが
対象と文脈によって変わり、
合理的な理由があれば異なる判断が成立し得るためである。

**Note:** 本Ruleは
Registration Qualificationではない。
本Ruleが述べるのは提案の優先であり、
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立し得る対象を限定しない。

本Ruleが述べる優先は、
提案対象の順序または提示上の強調として働く。
優先されないことは、
Candidate Recommendation（候補提案）の対象から
除外されることを意味しない。
除外してはならない根拠は `CPL-SF-006` が定める。

本Ruleは、次のいずれも必要条件としない。

```text
Occurrence Count
Formal Status
専門用語であること
英語難易度
Category
TitleまたはHeadingであること
```

解釈補助は
「Candidate Recommendation Guidance」に示す。
同節はNon-normative Content（非規範的内容）である。

#### CPL-SF-005 — Recommendation Does Not Establish Canonicality（提案は正規性を成立させない）

**Rule ID:** `CPL-SF-005`

**Rule Name:** Recommendation Does Not Establish Canonicality

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Candidate Recommendation（候補提案）が行われたことのみを根拠として、
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立したものとして扱ってはならない。

**Reason:** Canonical Primary Language Support Association（正規主要言語補助対応）は、
Repositoryが一貫して再利用すると決定したときに成立する。
提案の存在を成立と同一視すると、
決定されていない対応がCanonicalとして
Central Concrete Declaration Source（中央具体宣言情報源）へ入り、
Canonical Declaration（正規宣言）が
成立済みの決定を表さなくなる。
提案と決定を分けることで、
中央に保持される内容が
成立したCanonical Decision（正規判断）に限られる。

**Note:** 本Ruleが禁じるのは、
Candidate Recommendation（候補提案）のみを根拠として
成立を認めることである。
Human Direct Decisionから
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立する経路は妨げない。

本Ruleは、
Human Review Workflow、
具体的なActor、
Approval / Rejection Stateを規定しない。

#### CPL-SF-006 — Recommendation Does Not Preempt Canonical Decision（提案は正規判断を先取りしない）

**Rule ID:** `CPL-SF-006`

**Rule Name:** Recommendation Does Not Preempt Canonical Decision

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** あるEnglish Representation（英語表現）について
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立する見込みが低いこと、または
成立するかどうかが不明であることのみを根拠として、
そのEnglish Representation（英語表現）を
Candidate Recommendation（候補提案）の対象から除外してはならない。

**Reason:** 成立するかどうかは
Canonical Association Establishment（正規対応成立）の側で決まる。
提案の段階でその見込みを先取りして対象を落とすと、
落とされたEnglish Representation（英語表現）については
成立させるか否かの判断自体が行われず、
判断されなかったことと
判断のうえ成立しなかったこととが区別できなくなる。
`CPL-SF-005` は、提案されたことを成立と扱うことを禁じて
提案と決定を分離している。
成立の見込みを提案の可否へ持ち込むことは、
同じ分離を逆向きに崩し、
決定の範囲を提案の側が先に確定させることになる。
見込みを除外根拠としないことで、
Canonical Decision（正規判断）が
提案の段階で先取りされない。

**Note:** 本Ruleが禁じるのは、
成立の見込みのみを根拠とする除外である。
他の根拠による除外は本Ruleの対象ではない。
Code・Identifier（識別子）・Path等として機能し、
Primary Language Reading Supportの対象でないことが
明らかなLiteral Representation（そのままの表記）を
提案対象としないことは、
成立の見込みを根拠とする除外ではない。

本Ruleは、
Repository Documentation（Repository文書）に現れる
English Representation（英語表現）の
Completenessを要求しない。
網羅一覧を作ることも、
提案数を増やすことも要求しない。

本Ruleは、
`CPL-SF-004` が述べる提案の優先を妨げない。
優先度の差は提案対象の順序または提示上の強調として働き、
除外としては働かない。

本Ruleは、
Rejected Candidate History、
Permanent Exclusion、
Human Review Workflow、
Approval / Rejection Stateを規定しない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRuleに従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations」で明示的に宣言している。
- Current Repositoryにおける
  Central Concrete Declaration Source（中央具体宣言情報源）の
  Concrete Source Assignmentを
  「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が
  `CPL-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）が、
  必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書自身のPhysical Name（物理名称）は、
[Naming Convention](naming.md)
が定めるRuleに従っている。

- File Stemは
  英字をすべて小文字で表記し、語をハイフンで区切っている。
- 現在のPath Contextにおいて、
  `canonical-primary-language-support` はその対象を十分に識別している。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
