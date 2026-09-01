# Writing Convention（文章規約）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Documentation（Repository文書）の
Human-readable Natural Language Representation（人間可読な自然言語表現）について、
Semantic Meaningを明確・一貫・安定して伝達するために
反復適用される
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の6点である。

1. Repository Documentation（Repository文書）の
   Natural Language Prose（自然言語本文）、
   Document Title（文書題名）、および
   Heading Label（見出しラベル）は、
   どの言語でMeaning（意味）を伝えるのか。
2. Canonical Primary Language Support Association（正規主要言語補助対応）が
   成立しているEnglish Representation（英語表現）は、
   Human-readable Natural Language Representation（人間可読な自然言語表現）において
   どのように表示されるのか。
3. あるSubject / Meaning（意味）について
   Definition Authority（定義権限）側で
   English Representation（英語表現）が成立している場合、
   その対象を参照する箇所では、どの表現を使用するのか。
4. 文章が伝えるSemantic Meaningは、
   何が満たされているとき明確に成立するのか。
5. Normative Rule（規範的規則）を記述する文章は、
   宣言されたRequirement Level（要求レベル）に対して
   どのような関係になければならないのか。
6. Human-readableなDocument Title（文書題名）は、
   何を表すのか。

本文書が対象とするのは
Natural Language Representation（自然言語表現）そのものである。
本文書は、文章術一般、
またはStyle Guide一般を目的としない。

本文書が担うのは
Presentation / Usage Responsibilityである。
本文書は、English Representation（英語表現）そのもの、および
Canonical Primary Language Support（正規主要言語補助）の
Canonicalityを定義しない。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は、次を上位Sourceとして参照する。

- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)
- [Canonical Primary Language Support Architecture](../architecture/canonical-primary-language-support.md)
- [Canonical Primary Language Support Convention](canonical-primary-language-support.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Writing Convention

Canonical Primary Language Support Architecture
        ▲
        │ presupposes
Writing Convention

Canonical Primary Language Support Convention
        ▲
        │ presupposes
Writing Convention
```

本文書は、Canonical Primary Language Support（正規主要言語補助）側の
RuleおよびCanonical Declaration（正規宣言）を
参照するのみであり、変更・再定義しない。

本文書は
[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Repository Documentation（Repository文書）上で反復して成立する
Natural Language Representation（自然言語表現）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Areaを代表・集約するAssetではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- SectionとSection Responsibility（Section責務）、
  および `Section ≠ Heading` をはじめとする
  Logical / Representation Boundary
- Documentation Framework（文書体系）と
  Documentation Area（文書責務領域）
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的規則）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（規則モデル）の必須要素・任意要素、
  およびRule Statement（規則文）・Reasonの位置づけ
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（規則同一性）とその安定性
- Rule ID Format（規則ID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  StabilityのField表現
- Namespace Code（名前空間コード）の割当
- English Representation（英語表現）のIdentity（同一性）および
  Meaning（意味）
- Canonical Primary Language Support Representation（正規主要言語補助表現）の意味
- Canonical Primary Language Support Association（正規主要言語補助対応）の意味、
  その成立、およびMultiplicity（多重度）
- 同Association（対応）の成立と
  Documentation Presentation（文書上の表示）との
  Boundary（境界）
- 個々のCanonical Primary Language Support Association（正規主要言語補助対応）の値、
  およびそのCanonical Declaration（正規宣言）としての保持

### Responsibility Boundary（責務境界）

本文書が担うのは
Human-readable Natural Language Representation（人間可読な自然言語表現）に
限られる。
隣接する責務との境界は次である。

```text
Semantic Structure
    → Documentation Structure Convention

Physical Name
    → Naming Convention

English Representationそのもの、および
それが指すUnderlying Meaning
    → それぞれの対象を所有するDefinition Authority

Canonical Primary Language Support Associationの
Semantic Modelとその成立
    → Canonical Primary Language Support Architecture

個々のCanonical Primary Language Support Associationの値と
そのCanonical Declaration
    → Canonical Primary Language Support Convention、および
      同規約が定める
      Central Concrete Declaration Source

Human-readable Natural Language Representationにおける
使用と表示
    → 本文書

Markdown Syntax / Markup Representation
    → 本文書の責務ではない
```

本文書は
Semantic Structure（意味構造）、
Physical Name（物理名称）、
Markdown Syntaxを定義しない。
本文書は、English Representation（英語表現）の
Definition Authority（定義権限）を取得せず、
Canonical Primary Language Support Association（正規主要言語補助対応）の
成立可否およびCanonicalityも定めない。
本文書は、Markdown Syntaxの責務を担う
Convention（規約）の存在や内容を前提とせず、
その責務を本文書側で新たに成立させることもしない。

Commit Messageの
Natural Language Representation（自然言語表現）は
[Commit Convention](commit.md)
が所有する。
本文書はこれを再定義しない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository Documentation（Repository文書）の
  Natural Language Prose（自然言語本文）、
  Document Title（文書題名）、および
  Heading Label（見出しラベル）における
  Primary Language
- Current Repositoryにおける
  Primary LanguageのConcrete Assignment（具体割当）
- Canonical Primary Language Support Association（正規主要言語補助対応）が
  成立しているEnglish Representation（英語表現）に対する
  Canonical Primary Language Support Representation（正規主要言語補助表現）の
  表示形式と、その適用対象
- Definition Authority（定義権限）側で成立している
  English Representation（英語表現）の、
  参照箇所における一貫した使用
- Subject・Responsibility Holder・
  Reference Target等に関する
  Semantic Reference Clarity
- Rule Statement（規則文）の
  Natural Language Representation（自然言語表現）と、
  宣言されたRequirement Level（要求レベル）との整合
- Normative Meaning（規範的意味）を左右する
  条件・例外・判断境界の記述
- Definition（定義）としてConcept（概念）を成立させる文章の記述
- Human-readableなDocument Title（文書題名）が表す
  Subject / Meaning（対象／意味）
- Repository README（Repository README）の
  Document Title（文書題名）が表す
  Subject / Meaning（対象／意味）

本文書が対象とする
Human-readable Natural Language Representation（人間可読な自然言語表現）には、
Natural Language Prose（自然言語本文）に加えて、
Human-readableな
Document Title（文書題名）およびHeading Label（見出しラベル）の
Natural Language Representation（自然言語表現）が含まれる。

Document Title（文書題名）およびHeading Label（見出しラベル）に対しては、
Primary Languageを定める `WRT-SF-001` 、
Canonical Primary Language Support Representation（正規主要言語補助表現）の
表示を定める `WRT-SF-002` 、および
English Representation（英語表現）の一貫した使用を定める
`WRT-SF-003` が適用される。

Document Title（文書題名）に対しては、
これらに加えて、
Subject / Meaning（対象／意味）の表示を定める `WRT-SF-008` 、および
Repository README（Repository README）の
Document Title（文書題名）を定める `WRT-SF-009` が適用される。

その他のRuleの適用範囲は、
各RuleのRule Statement（規則文）が示す
Semantic Subjectによって定まる。
本文書は、すべてのRuleを
Document Title（文書題名）およびHeading Label（見出しラベル）へ
一律に適用しない。

各Ruleが個別に定める適用条件は、
当該RuleのRule Statement（規則文）が確定する。

### Out of Scope（本文書が定義しない範囲）

- Section・Section Responsibility（Section責務）・
  Standard Section（標準Section）等の
  Semantic Structure（意味構造）
- Section Identity（Section同一性）、
  Heading Level（見出しレベル）、
  Markdown Heading Marker（Markdown見出し記号）、
  およびSectionとHeading（見出し）の
  Mapping Rule（対応規則）
- 固定のHeading Catalog、および
  `Purpose → 目的` のような固定翻訳Catalog
- File名、Directory名、Path等の
  Physical Name（物理名称）
- Markdown Syntaxその他の記述媒体固有表現
- Commit Message等、
  Documentation Asset（文書資産）以外の成果物の
  Natural Language Representation（自然言語表現）
- English Representation（英語表現）のIdentity（同一性）、
  Meaning（意味）、Canonical Name、
  Formal Status（正式地位）、Category（分類）、
  およびName Status
- English Representation（英語表現）が指す
  Underlying Meaning（対象の意味）
- Canonical Primary Language Support Association（正規主要言語補助対応）の成立、
  そのMultiplicity（多重度）、および
  Canonical Primary Language Support Representation（正規主要言語補助表現）の値
- Canonical Declaration（正規宣言）の保持先、
  そのConcrete Representation（具体表現）、および
  Candidate Recommendation（候補提案）
- Definition Model、すなわち
  Definition（定義）が意味上どのような要素から成るかのModel
- 文末表現（`である調` / `です・ます調`）、Voice、
  一文あたりの情報量、文長、List化の要否
- 句読点、全角／半角、文字間空白、
  Colon / Slash等のTypography
- Prohibited Word Catalog、
  Preferred Word Catalog
- 略語の展開に関する一般Rule
- Validator / Linter / CI等のTool要求

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）および
Concrete Assignment（具体割当）の宣言である。
**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: WRT
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

### Primary Language（主要言語）

Current Repositoryにおいて
`WRT-SF-001` が対象とするPrimary Languageは次である。

```text
Primary Language = Japanese
```

本宣言はCurrent Repositoryにおける
Concrete Assignment（具体割当）の値のみを示す。
`Japanese` はPrimary LanguageそのもののDefinition（定義）ではない。
Primary Languageが何であるかは
`WRT-SF-001` が示し、
どの言語がそれに割り当てられているかを本宣言が示す。

本宣言によって、
Primary Languageの選定基準、
Repositoryごとの設定機構、
またはPrimary Language以外の言語に関する
一般Ruleは成立しない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的規則）が
適用対象を区別するために用いる局所的な区別を示す。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。
各Ruleの適用対象と内容は、
すべてNormative Rule（規範的規則）側で確定する。

ここで示すのは本文書が必要とする範囲の区別であり、
English Representation（英語表現）またはその表示について
分類体系を成立させるものではない。

### Natural Language Prose（自然言語本文）

Natural Language Prose（自然言語本文）は、
Documentation Asset（文書資産）のうち、
読み手へ意味を伝えるために自然言語で記述される部分である。

Code Block内のCode、
Identifier（識別子）、Path等の
Literal Representation（そのままの表記）は、
それ自体が自然言語として意味を伝える部分ではない。

Document Title（文書題名）およびHeading Label（見出しラベル）は、
Natural Language Prose（自然言語本文）とは別に、
各RuleのRule Statement（規則文）が
対象として名指す。
Rule Statement（規則文）が
Natural Language Prose（自然言語本文）のみを対象とする場合、
その適用は本文に限られる。

### Relationship with Canonical Primary Language Support Establishment（Canonical Primary Language Support側の成立との関係）

本文書は、あるEnglish Representation（英語表現）について
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立しているかどうか、および
Canonical Primary Language Support Representation（正規主要言語補助表現）の値を
自ら判断しない。
いずれも
[Canonical Primary Language Support Convention](canonical-primary-language-support.md)
が定めるCanonical Declaration（正規宣言）から得られる。

同様に、あるSubject / Meaning（意味）について
どのEnglish Representation（英語表現）が成立しているかは、
その対象を所有するDefinition Authority（定義権限）側で定まる。

本文書が扱うのは、これらがすでに成立している場合の
使用と表示のみである。

```text
Association / English Representationの成立
    → 本文書の外側

使用と表示
    → 本文書
```

### Normative Strength（規範強度）

Normative Strengthは、
Rule Statement（規則文）の
Natural Language Representation（自然言語表現）が
読み手に対して生じさせる要求・禁止の強さである。

Requirement Level（要求レベル）の意味は
[Convention Architecture](../architecture/convention.md)
が所有する。
本文書はこれを再定義せず、
宣言されたRequirement Level（要求レベル）と
Rule Statement（規則文）の表現との関係のみを扱う。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規則ID）はCategory（分類）を表現しない。

### Language（言語）

#### WRT-SF-001 — Primary Language（主要言語）

**Rule ID:** `WRT-SF-001`

**Rule Name:** Primary Language

**Stability:** Development

**Requirement:** MUST

**Rule:** Primary Languageは、
Repository Documentation（Repository文書）の
Human-readable Natural Language Representation（人間可読な自然言語表現）が
Meaning（意味）を伝える基準言語である。

Repository Documentation（Repository文書）の
Natural Language Prose（自然言語本文）、
Human-readableなDocument Title（文書題名）、および
Heading Label（見出しラベル）は、
そこで伝えるMeaning（意味）を
読み手がPrimary Languageで受け取れるように記述する。

本Ruleが要求するのは、
当該Human-readable Representation（人間可読表現）が伝える
Meaning（意味）がPrimary Languageで成立していることである。
表現全体をPrimary Languageのみで構成することではない。
English Representation（英語表現）その他
Primary Language以外の表記を含むことは、
それ自体では本Ruleに反しない。

次は本Ruleの対象ではなく、
Primary Languageによる表記を要求されない。

- CodeおよびIdentifier（識別子）
- File名、Directory名、Path
- External Product / Tool / Protocol等の正式名称
- External Contractによって表記が固定される文字列
- 原文を維持する必要がある引用

Current RepositoryにおけるPrimary Languageの
Concrete Assignment（具体割当）は
「Concrete Declarations」が宣言する。
本RuleのRequirementはその具体値に依存しない。

**Reason:** Primary Languageが定まっていなければ、
同一のRepository Documentation（Repository文書）内で
記述者ごとに言語が分岐し、
読み手はSemantic Meaningを受け取る前に
言語の切り替えを強いられる。
一方で、対象を識別する表記そのものを
Primary Languageへ置き換えると、
Code・Identifier（識別子）・
External Contractが指す対象と一致しなくなり、
参照が成立しなくなる。
Meaning（意味）の成立をPrimary Languageへ固定し、
識別を担う表記を対象外とすることで、
読解の前提を一定にしたまま参照の同一性を保つ。
要求を表現全体の構成ではなく
Meaning（意味）の成立に置くのは、
Definition Authority（定義権限）側で成立している
English Representation（英語表現）を
参照箇所で使用することが
`WRT-SF-003` によって要求されており、
構成をPrimary Languageのみへ限ると
その要求と両立しないためである。
Document Title（文書題名）およびHeading Label（見出しラベル）を
対象へ含めるのは、
これらが読み手にとって本文へ到達する前の自然言語表現であり、
本文と言語が分かれると、
同一のDocumentation Asset（文書資産）の中で
読解の前提が二分されるためである。

**Note:** 本Ruleが定めるのは、
対象とするHuman-readable Natural Language Representation（人間可読な自然言語表現）の
言語のみである。
文末表現、Voice、文長、Typographyは
本Ruleが定めない。

本Ruleが担うのはLanguage Responsibilityである。
Document Title（文書題名）が表す
Subject / Meaning（対象／意味）は本Ruleが定めない。
それらは `WRT-SF-008` および `WRT-SF-009` が定める。

Canonical Primary Language Support Representation（正規主要言語補助表現）の
表示形式は `WRT-SF-002` が定める。
本Ruleは表示形式を定めない。

`Japanese` はPrimary Languageの
Definition（定義）ではなく、
Current RepositoryにおけるConcrete Assignment（具体割当）である。
本Ruleは、その割当の変更手順、
Repositoryごとの設定機構、および
Primary Language以外の言語の扱いを定めない。

Document Title（文書題名）およびHeading Label（見出しラベル）を
対象とすることは、
Section Identity（Section同一性）、
Standard Section（標準Section）、
Heading Level（見出しレベル）、
Markdown Heading Marker（Markdown見出し記号）について
何も定めない。
本Ruleは、
固定のHeading Catalogおよび
固定翻訳Catalogを持たない。

Commit Messageの
Message Language（メッセージ言語）は
[Commit Convention](commit.md)
が所有する。

### English Representation and Primary Language Support（英語表現と主要言語補助）

#### WRT-SF-002 — Canonical Primary Language Support Presentation（正規主要言語補助の表示）

**Rule ID:** `WRT-SF-002`

**Rule Name:** Canonical Primary Language Support Presentation

**Stability:** Development

**Requirement:** MUST

**Rule:** Canonical Primary Language Support Association（正規主要言語補助対応）が
成立しているEnglish Representation（英語表現）を
Human-readable Natural Language Representation（人間可読な自然言語表現）で
使用する場合、次の形式で表示する。

```text
English Representation（Canonical Primary Language Support Representation）
```

本Ruleの適用対象は次の3つである。

- Natural Language Prose（自然言語本文）
- Human-readableなDocument Title（文書題名）
- Heading Label（見出しラベル）

この表示は初出箇所に限らず、
対象となる使用箇所へ適用する。

ただし、ある使用箇所の
Human-readable Representation（人間可読表現）が、
別のSubjectについての
Definition Responsibility（定義責務）によって
すでに定義されている場合、
その使用箇所は本Ruleの適用対象ではない。
その箇所では定義済みの
Human-readable Representation（人間可読表現）をそのまま使用し、
本Ruleの表示形式がそれを置換・上書きすることはない。

Canonical Primary Language Support Association（正規主要言語補助対応）の有無、
およびCanonical Primary Language Support Representation（正規主要言語補助表現）の値は
本Ruleが決定しない。
いずれも
[Canonical Primary Language Support Convention](canonical-primary-language-support.md)
が定めるCanonical Declaration（正規宣言）による。

**Reason:** Canonical Primary Language Support Association（正規主要言語補助対応）は、
そのEnglish Representation（英語表現）の理解補助として
Repositoryが一貫して再利用すると決定した
Primary Language Representation（主要言語表現）を保持している。
その決定が使用箇所へ現れなければ、
読み手は成立済みの理解補助を受け取れず、
決定が読み手に対して機能しない。
English Representation（英語表現）と
Canonical Primary Language Support Representation（正規主要言語補助表現）を
同じ箇所へ併記することで、
読み手は参照される表現とそのPrimary Languageによる補助を
対応付けたまま読み進められる。
初出箇所に限定しないのは、
Documentation Asset（文書資産）が
先頭から通読されるとは限らず、
Section単位または検索経由での参照において
初出箇所の表示が読み手へ届かないためである。
Association（対応）の有無と値を本Ruleが決定しないのは、
Canonicalityの成立が
Canonical Primary Language Support（正規主要言語補助）側の責務であり、
表示側でそれを再判断すると
中央で成立した決定と使用箇所の表示が分岐するためである。

定義済みのHuman-readable Representation（人間可読表現）を
適用対象から外すのは、
その箇所に現れる表現が、
English Representation（英語表現）の理解補助として選ばれた表現ではなく、
その対象を所有するDefinition Authority（定義権限）が定義した
Human-readable Representation（人間可読表現）そのものであるためである。
そこへ本Ruleの表示形式を適用すると、
表示側が定義済みの表現を置き換えることになり、
定義の所在と使用箇所の表現が分岐する。
定義済みの表現をそのまま現すことで、
定義側で成立した決定が使用箇所においても保たれる。

**Note:** 本Ruleは
Canonical Primary Language Support Association（正規主要言語補助対応）を
成立させず、
どのEnglish Representation（英語表現）について
対応を成立させるべきかも定めない。

Canonical Primary Language Support Association（正規主要言語補助対応）が
成立していないEnglish Representation（英語表現）の表示について、
本Ruleは何も定めない。

Code・Identifier（識別子）・Path等として機能する
Literal Representation（そのままの表記）は、
Human-readable Natural Language Representation（人間可読な自然言語表現）としての
使用ではなく、本Ruleの対象ではない。
Rule ID（規則ID）、Rule Name（規則名）等、
対象を識別するIdentifier（識別子）または
Labelとしての表記も同様である。

Document Title（文書題名）およびHeading Label（見出しラベル）について、
固定のHeading Catalogおよび
固定翻訳Catalogは本Ruleから成立しない。

本Ruleの適用境界は、
その使用箇所のHuman-readable Representation（人間可読表現）について
別のSubjectの
Definition Responsibility（定義責務）が成立しているかどうかによって定まる。
Document Title（文書題名）・Heading Label（見出しラベル）・
Natural Language Prose（自然言語本文）という
使用箇所の種別によっては定まらない。
定義済みのHuman-readable Representation（人間可読表現）を持たない
Document Title（文書題名）およびHeading Label（見出しラベル）は、
引き続き本Ruleの適用対象である。

たとえば、
Standard Section Heading Representation（標準Section見出し表現）が
定義されているStandard Section（標準Section）のHeading（見出し）は、
その定義済みRepresentation（表現）が現れる箇所であり、
本Ruleの適用対象ではない。
そのHeading（見出し）に含まれるEnglish Representation（英語表現）について
Canonical Primary Language Support Association（正規主要言語補助対応）が
成立していたとしても、
本Ruleを根拠として
そのHeading（見出し）を上記の表示形式へ置き換えることはない。
これは本Ruleの適用境界の一例であり、
Standard Section（標準Section）に固有の例外ではない。

本Ruleは、
どのSubjectについて
Human-readable Representation（人間可読表現）の
Definition Responsibility（定義責務）が成立するかを定めない。
いずれもその対象を所有する
Definition Authority（定義権限）側で成立する。

#### WRT-SF-003 — English Representation Consistency（英語表現の一貫性）

**Rule ID:** `WRT-SF-003`

**Rule Name:** English Representation Consistency

**Stability:** Development

**Requirement:** MUST

**Rule:** あるSubject / Meaning（意味）について、
そのDefinition Authority（定義権限）側で
English Representation（英語表現）が成立している場合、
その対象をRepository Documentation（Repository文書）上で参照するときは、
その定義済みEnglish Representation（英語表現）を一貫して使用する。

本Ruleは、
Natural Language Prose（自然言語本文）における参照に加えて、
Human-readableなDocument Title（文書題名）および
Heading Label（見出しラベル）における参照へ適用する。

**Reason:** Definition Authority（定義権限）側で成立している
English Representation（英語表現）は、
その対象を参照するための表現である。
参照箇所ごとに異なる表現が用いられると、
読み手はそれらが同じ対象を指すのか
別の対象を指すのかを判定できず、
表現の同一性による参照が成立しない。
また、使用箇所の表現が定義側の表現と一致しなければ、
読み手は使用箇所から定義へ到達できない。
定義済みの表現をそのまま使用することで、
参照の同一性と定義への到達可能性が保たれる。

**Note:** 本Ruleは、
English Representation（英語表現）のIdentity（同一性）、
Meaning（意味）、Canonical Name、
Formal Status（正式地位）、Category（分類）、
およびName Statusを定義しない。
いずれもその対象を所有する
Definition Authority（定義権限）側で成立する。

Canonical Primary Language Support Representation（正規主要言語補助表現）の一貫性は
本Ruleが扱わない。
Canonical Primary Language Support側の一貫性は、
`WRT-SF-002` と
[Canonical Primary Language Support Convention](canonical-primary-language-support.md)
が定めるCanonical Declaration（正規宣言）によって成立する。

本Ruleが要求するのは参照表現の一貫性であり、
文章全体で同じ単語を機械的に反復することではない。

```text
English Representation Consistency
≠ Mechanical Word Repetition
```

Definition Authority（定義権限）側で
English Representation（英語表現）が成立していない対象について、
本Ruleは使用する表現を定めない。
通常の説明文において、
読みやすさのために語や言い回しを変えることは
本Ruleが禁じるところではない。

### Semantic Clarity（意味の明確性）

#### WRT-SF-004 — Semantic Reference Clarity（意味上の参照の明確性）

**Rule ID:** `WRT-SF-004`

**Rule Name:** Semantic Reference Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Subject、Responsibility Holder、
Reference Target等について、
その文脈で複数の合理的解釈が成立する場合は、
対象を明示する。

**Reason:** これらは、文がどの対象について何を述べているかを
確定させる要素である。
複数の解釈が成立したまま残ると、
読み手ごとに異なる対象へ内容が適用され、
Documentation Asset（文書資産）が伝えるはずの
Semantic Meaningが読み手側で分岐する。
明示を求める条件を
複数の合理的解釈が成立する場合に限定するのは、
文脈から対象が一意に定まる箇所にまで
反復的な明示を強いないためである。

**Note:** 本Ruleが対象とするのは
解釈の分岐であり、特定の語や文型ではない。

「これ」「それ」「上記」等の指示語、および
日本語における主語の省略それ自体は、
本Ruleが禁じるところではない。
これらの表現が用いられている場合であっても、
対象が一意に定まるならば本Ruleは適用されない。

### Normative Writing（規範的記述）

#### WRT-SF-005 — Normative Strength Consistency（規範的強度の一貫性）

**Rule ID:** `WRT-SF-005`

**Rule Name:** Normative Strength Consistency

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Rule Statement（規則文）の
Natural Language Representation（自然言語表現）は、
そのNormative Rule（規範的規則）が宣言する
Requirement Level（要求レベル）と異なる
Normative Strengthを導入してはならない。

**Reason:** Requirement Level（要求レベル）は、
そのRuleが要求・禁止・推奨・許容のいずれであるかを
確定させる宣言である。
文章表現がそれと異なる強度を伝えると、
宣言された水準と読み取られる水準が食い違い、
どちらに従うべきかを読み手が判断できなくなる。
表現の強度を宣言へ一致させることで、
Requirement Level（要求レベル）が
適合判断の根拠として機能する。

**Note:** Requirement Level（要求レベル）の意味は
[Convention Architecture](../architecture/convention.md)
が所有する。
本Ruleはそれを再定義せず、
宣言と表現の一致のみを要求する。

本Ruleは、
Requirement Level（要求レベル）ごとに使用してよい
文末表現のCatalogを定めない。

#### WRT-SF-006 — Normative Condition Clarity（規範的条件の明確性）

**Rule ID:** `WRT-SF-006`

**Rule Name:** Normative Condition Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Normative Meaning（規範的意味）を左右する
条件・例外・判断境界は、
何が満たされるときにそれが成立するのかを
判断可能な形で示す。
「適切に」「必要に応じて」「原則として」等、
判断基準を伴わない表現だけに
Normative Meaning（規範的意味）を依存させない。

**Reason:** 条件・例外・判断境界は、
そのRuleが適用されるかどうかを分ける要素である。
判断基準を伴わない表現だけでそれが示されると、
適用の可否が読み手の裁量で決まり、
Ruleが対象へ及ぶ範囲が箇所ごとに変わる。
判断可能な形を要求することで、
適合の判定を記述内容から行える。

**Note:** 本Ruleが対象とするのは、
Normative Meaning（規範的意味）を左右する箇所である。
Non-normative Content（非規範的内容）における
同種の表現は本Ruleの対象ではない。

本Ruleは
Prohibited Word Catalogを定義しない。
挙げた表現は、
判断基準を伴わない記述の例示であり、
語そのものの使用可否を定めるものではない。

### Definition Writing（定義の記述）

#### WRT-SF-007 — Definition Clarity（定義の明確性）

**Rule ID:** `WRT-SF-007`

**Rule Name:** Definition Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Definition（定義）としてConcept（概念）を成立させる文章は、
Definition Targetを識別可能にし、
その対象が何であるかを肯定的に示す。
Negative Statement、
他のConcept（概念）との差分、
およびExampleは、
この肯定的な記述の代替として用いない。

**Reason:** Definition（定義）が果たすべきことは、
その対象が何であるかを確定させることである。
何でないか、何と異なるか、どのような場合があるかだけが示されると、
対象の輪郭は示された事項の外側として残るのみであり、
読み手ごとに異なる範囲で解釈される。
肯定的な記述を要求することで、
Concept（概念）の成立が
他の記述の有無や読み手の補完に依存しなくなる。

**Note:** 本Ruleは
Definition Model、すなわち
Definition（定義）が意味上どのような要素から成るかの
Modelを定義しない。
要求するのは、
Definition Targetの識別可能性と、
肯定的な記述の存在である。

Negative Statement、他のConcept（概念）との差分、
Exampleは、理解を助ける記述として有用である。
本Ruleが対象とするのは、
それらが肯定的な記述の位置を占める場合である。
肯定的な記述が成立したうえでこれらを併記することは、
本Ruleが禁じるところではない。

### Document Title（文書題名）

#### WRT-SF-008 — Document Title Meaning（文書題名の意味）

**Rule ID:** `WRT-SF-008`

**Rule Name:** Document Title Meaning

**Stability:** Development

**Requirement:** MUST

**Rule:** Human-readableな
Document Title（文書題名）は、
そのDocumentation Asset（文書資産）が主として扱う
Subject / Meaning（対象／意味）を明確に表す。

Documentation Area（文書責務領域）への所属、
Document Responsibility（文書責務）、
またはRepository由来を識別する目的だけを理由として、
Title Component（題名構成要素）を機械的に導出しない。

**Reason:** Document Title（文書題名）は、
読み手がそのDocumentation Asset（文書資産）へ到達する前に
受け取る唯一の自然言語表現であることが多い。
そこに扱われるSubject / Meaning（対象／意味）が現れなければ、
読み手は本文を読むまで
その文書が何についてのものかを判断できない。
一方、所属・責務・由来を識別する目的だけで
それらの語をTitle（題名）へ再提示すると、
Title（題名）は同じ語の反復によって占められ、
Subject / Meaning（対象／意味）の区別が読み手に届かなくなる。
表すべきものをSubject / Meaning（対象／意味）に定めることで、
Title（題名）が識別と理解の双方で機能する。

**Note:** 本Ruleは
Document Title（文書題名）の
固定Schema、Title Component（題名構成要素）の集合、
およびそれらの表記順序を定めない。

`Architecture`・`Convention`・`Framework` 等の語が
Title（題名）へ含まれること自体を、
本Ruleは禁じない。
これらの語が、そのDocumentation Asset（文書資産）が主として扱う
Subject / Meaning（対象／意味）そのものを構成する場合、
Title（題名）へ含まれる。

Documentation Asset（文書資産）のIdentity（同一性）、
Document Responsibility（文書責務）、
Documentation Area（文書責務領域）への所属、および
Document Title（文書題名）との境界は
[Documentation Structure Architecture](../architecture/documentation-structure.md)
が定義する。
本Ruleはこれを再定義しない。

File名、Directory名、Pathは
[Naming Convention](naming.md)
が所有する。
本Ruleはこれらを定めない。

#### WRT-SF-009 — Repository README Title（Repository READMEの題名）

**Rule ID:** `WRT-SF-009`

**Rule Name:** Repository README Title

**Stability:** Development

**Requirement:** MUST

**Rule:** Repository README（Repository README）の
Document Title（文書題名）は、
そのRepositoryが主として表す
Subject / Meaning（対象／意味）を、
読み手が識別・理解できるよう明確に表す。

**Reason:** Repository README（Repository README）は、
読み手がそのRepositoryで最初に到達する
Documentation Asset（文書資産）である。
そのDocument Title（文書題名）は、
Repositoryが主として表すSubject / Meaning（対象／意味）へ
読み手が到達する最初の自然言語表現になる。
そこにSubject / Meaning（対象／意味）が現れなければ、
読み手は本文を読むまで
そのRepositoryが何を表すのかを判断できない。
一方、Title（題名）へ含めるべき要素を固定すると、
一つの表現でSubject / Meaning（対象／意味）が
すでに十分に伝わる場合にも要素の追加を強いることになり、
Title（題名）の役割が
識別と理解から構成の充足へ置き換わる。
要求をSubject / Meaning（対象／意味）の明確さに置くことで、
構成の自由度を保ったままTitle（題名）が機能する。

**Note:** 本Ruleは、
Document Title（文書題名）の
Component Structure（構成）を固定しない。
Name（名称）とその説明を併記するかどうか、
それらを区切るSeparator（区切り文字）、
およびTitle（題名）のSyntaxは
本Ruleが定めない。

説明的な名称そのものが
Subject / Meaning（対象／意味）を十分に表す場合、
その表現だけで本Ruleは満たされる。

Repository Identifier（Repository識別子）、File名、Path等を
そのままDocument Title（文書題名）へ再提示することは、
それだけでは本Ruleを満たさない。
これらは、そのRepositoryが主として表す
Subject / Meaning（対象／意味）を表すとは限らないためである。

本Ruleは、あるRepositoryが
何を主として表すのかを定めない。
それは本文書の外側で成立する。

本Ruleは、Repository README（Repository README）以外の
Documentation Asset（文書資産）の
Document Title（文書題名）について何も定めない。
それらには `WRT-SF-008` が適用される。

本Ruleは `WRT-SF-008` を上書きしない。
Repository README（Repository README）の
Document Title（文書題名）にも `WRT-SF-008` が適用される。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRuleに従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations」で明示的に宣言している。
- Current RepositoryにおけるPrimary Languageの
  Concrete Assignment（具体割当）を
  「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が
  `WRT-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）が、
  必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書は、自身が定めるRuleにも従っている。

- Natural Language Prose（自然言語本文）、
  Document Title（文書題名）、および
  Heading Label（見出しラベル）が伝えるMeaning（意味）を、
  Current RepositoryのPrimary Languageである
  日本語で受け取れるように記述している。
- Document Title（文書題名）において、
  本文書が主として扱うSubject / Meaning（対象／意味）を表している。
- Canonical Primary Language Support Association（正規主要言語補助対応）が
  成立しているEnglish Representation（英語表現）を、
  Natural Language Prose（自然言語本文）、
  Document Title（文書題名）、およびHeading Label（見出しラベル）の
  いずれにおいても
  `English Representation（Canonical Primary Language Support Representation）`
  の形式で表示している。
- Definition Authority（定義権限）側で成立している
  English Representation（英語表現）を、
  参照箇所において一貫して使用している。
- 各Rule Statement（規則文）の表現を、
  宣言したRequirement Level（要求レベル）へ一致させている。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
