# Writing Convention（文章規約）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Documentation（Repository文書）の
Human-readable Natural Language Representation（人間可読な自然言語表現）について、
Semantic Meaning（意味）を明確・一貫・安定して伝達するために
反復適用される
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の4点である。

1. Repository Documentation（Repository文書）の
   Natural Language Prose（自然言語本文）は、
   どの言語で記述されるのか。
2. Repository内で特定のConcept（概念）・Responsibility（責務）・
   Role（役割）等を識別するために使用される
   Formal English Term（正式英語用語）は、
   どのように表現され、どのように一貫させるのか。
3. 文章が伝えるSemantic Meaning（意味）は、
   何が満たされているとき明確に成立するのか。
4. Normative Rule（規範的ルール）を記述する文章は、
   宣言されたRequirement Level（要求レベル）に対して
   どのような関係になければならないのか。

本文書が対象とするのは
Natural Language Representation（自然言語表現）そのものである。
本文書は、文章術一般、
またはStyle Guide（文体指針）一般を目的としない。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Convention Architecture（規約の意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（規約記述表記）
        ▲
        │ conforms to（記述表記に従う）
Writing Convention（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Repository Documentation（Repository文書）上で反復して成立する
Natural Language Representation（自然言語表現）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Section（節）とSection Responsibility（Section責務）、
  および `Section ≠ Heading` をはじめとする
  Logical / Representation Boundary（論理／表現境界）
- Documentation Framework（文書体系）と
  Documentation Area（文書責務領域）
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的ルール）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（ルールモデル）の必須要素・任意要素、
  およびRule Statement（ルール文）・Reason（理由）の位置づけ
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（ルール同一性）とその安定性
- Rule ID Format（規約ルールID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  Stability（安定性）のField表現
- Namespace Code（名前空間コード）の割当

### Responsibility Boundary（責務境界）

本文書が担うのは
Human-readable Natural Language Representation（人間可読な自然言語表現）に
限られる。
隣接する責務との境界は次である。

```text
Semantic Structure（意味構造）
    → Documentation Structure Convention（文書構造規約）

Physical Name（物理名称）
    → Naming Convention（命名規約）

Human-readable Natural Language Representation（人間可読な自然言語表現）
    → 本文書

Markdown Syntax / Markup Representation（Markdown構文／マークアップ表現）
    → 本文書の責務ではない
```

本文書は
Semantic Structure（意味構造）、
Physical Name（物理名称）、
Markdown Syntax（Markdown構文）を定義しない。
本文書は、Markdown Syntax（Markdown構文）の責務を担う
Convention（規約）の存在や内容を前提とせず、
その責務を本文書側で新たに成立させることもしない。

Commit Message（コミットメッセージ）の
Natural Language Representation（自然言語表現）は
[Commit Convention](commit.md)
が所有する。
本文書はこれを再定義しない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Repository Documentation（Repository文書）の
  Natural Language Prose（自然言語本文）における
  Primary Language（主要言語）
- Formal English Term（正式英語用語）の
  Representation Form（表現形式）と、その適用対象
- 同一のFormal Concept（正式概念）を参照する場合の
  Formal Term Consistency（正式用語一貫性）
- Subject（主体）・Responsibility Holder（責務主体）・
  Reference Target（参照対象）等に関する
  Semantic Reference Clarity（意味上の参照明確性）
- Rule Statement（ルール文）の
  Natural Language Representation（自然言語表現）と、
  宣言されたRequirement Level（要求レベル）との整合
- Normative Meaning（規範的意味）を左右する
  条件・例外・判断境界の記述
- Definition（定義）としてConcept（概念）を成立させる文章の記述

本文書が対象とする
Human-readable Natural Language Representation（人間可読な自然言語表現）には、
Natural Language Prose（自然言語本文）に加えて、
Human-readable（人間可読）な
Document Title（文書題名）およびHeading Label（見出しラベル）の
Natural Language Representation（自然言語表現）が含まれる。

Document Title（文書題名）およびHeading Label（見出しラベル）に対しては、
Primary Language（主要言語）を定める `WRT-SF-001` と、
Formal English Term（正式英語用語）に関する
`WRT-SF-002` ・ `WRT-SF-003` が適用される。

その他のRule（規則）の適用範囲は、
各Rule（ルール）のRule Statement（ルール文）が示す
Semantic Subject（意味上の対象）によって定まる。
本文書は、すべてのRule（規則）を
Document Title（文書題名）およびHeading Label（見出しラベル）へ
一律に適用しない。

### Out of Scope（本文書が定義しない範囲）

- Section（節）・Section Responsibility（Section責務）・
  Standard Section（標準Section）等の
  Semantic Structure（意味構造）
- Section Identity（Section同一性）、
  Heading Level（見出しレベル）、
  Markdown Heading Marker（Markdown見出し記号）、
  およびSection（節）とHeading（見出し）の
  Mapping Rule（対応規則）
- 固定のHeading Catalog（見出し一覧）、および
  `Purpose → 目的` のような固定翻訳Catalog（翻訳一覧）
- File名、Directory名、Path等の
  Physical Name（物理名称）
- Markdown Syntaxその他の記述媒体固有表現
- Commit Message（コミットメッセージ）等、
  Documentation Asset（文書資産）以外の成果物の
  Natural Language Representation（自然言語表現）
- Formal Name（正式名称）の
  Semantic Model（意味モデル）、および
  Term Taxonomy（用語分類体系）
- Glossary（用語集）・Term Registry（用語登録簿）等の
  用語管理機構
- Definition Model（定義モデル）、すなわち
  Definition（定義）が意味上どのような要素から成るかのModel（モデル）
- 文末表現（`である調` / `です・ます調`）、Voice（態）、
  一文あたりの情報量、文長、List化の要否
- 句読点、全角／半角、文字間空白、
  Colon / Slash等のTypography（文字表現）
- Prohibited Word Catalog（禁止語一覧）、
  Preferred Word Catalog（推奨語一覧）
- 略語の展開に関する一般Rule（一般規則）
- Validator / Linter / CI等のTool（ツール）要求

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: WRT
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace／共有基盤名前空間）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的ルール）が
適用対象を区別するために用いる局所的な区別を示す。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。
各Rule（ルール）の適用対象と内容は、
すべてNormative Rule（規範的ルール）側で確定する。

ここで示すのは本文書が必要とする範囲の区別であり、
Term Taxonomy（用語分類体系）でも
Formal Name Semantic Model（正式名称意味モデル）でもない。

### Natural Language Prose（自然言語本文）

Natural Language Prose（自然言語本文）は、
Documentation Asset（文書資産）のうち、
読み手へ意味を伝えるために自然言語で記述される部分である。

Code Block（コードブロック）内のCode（コード）、
Identifier（識別子）、Path等の
Literal Representation（そのままの表記）は、
それ自体が自然言語として意味を伝える部分ではない。

Document Title（文書題名）およびHeading Label（見出しラベル）は、
Natural Language Prose（自然言語本文）とは別に、
各Rule（ルール）のRule Statement（ルール文）が
対象として名指す。
Rule Statement（ルール文）が
Natural Language Prose（自然言語本文）のみを対象とする場合、
その適用は本文に限られる。

### Formal English Term（正式英語用語）とOrdinary Technical Term（一般技術用語）

本文書が区別するのは次の2つである。

```text
Formal English Term（正式英語用語）
    = Repository内で特定のConcept（概念）・Responsibility（責務）・
      Role（役割）等を安定して識別するために使用される英語用語

Ordinary Technical Term（一般技術用語）
    = Repository固有の識別を担わず、
      一般に通用する意味で使用される技術用語
```

`Repository`・`Commit`・`Branch`・`File`・`API` のような
Ordinary Technical Term（一般技術用語）は、
Repository固有のConcept（概念）を識別するために
使用されているのではない。

本文書は、どの用語が
Formal English Term（正式英語用語）として成立するかの
Catalog（一覧）を保持しない。
成立の根拠は、
その用語が使用されている箇所において
Repository固有の識別を担っているかどうかにある。

### Normative Strength（規範強度）

Normative Strength（規範強度）は、
Rule Statement（ルール文）の
Natural Language Representation（自然言語表現）が
読み手に対して生じさせる要求・禁止の強さである。

Requirement Level（要求レベル）の意味は
[Convention Architecture](../architecture/convention.md)
が所有する。
本文書はこれを再定義せず、
宣言されたRequirement Level（要求レベル）と
Rule Statement（ルール文）の表現との関係のみを扱う。

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Language（言語）

#### WRT-SF-001 — Primary Language

**Rule ID:** `WRT-SF-001`

**Rule Name:** Primary Language

**Stability:** Development

**Requirement:** MUST

**Rule:** Repository Documentation（Repository文書）の
Natural Language Prose（自然言語本文）、
Human-readable（人間可読）なDocument Title（文書題名）、
およびHeading Label（見出しラベル）は、
Primary Language（主要言語）である日本語で記述する。

次は本Rule（ルール）の対象ではなく、
日本語化を要求されない。

- Code（コード）およびIdentifier（識別子）
- File名、Directory名、Path
- Formal English Term（正式英語用語）
- External Product / Tool / Protocol等の正式名称
- External Contract（外部契約）によって表記が固定される文字列
- 原文を維持する必要がある引用

**Reason:** Primary Language（主要言語）が定まっていなければ、
同一のRepository Documentation（Repository文書）内で
記述者ごとに言語が分岐し、
読み手はSemantic Meaning（意味）を受け取る前に
言語の切り替えを強いられる。
一方で、対象を識別する表記そのものを日本語へ置き換えると、
Code（コード）・Identifier（識別子）・
External Contract（外部契約）が指す対象と一致しなくなり、
参照が成立しなくなる。
対象となる自然言語表現を日本語へ固定し、
識別を担う表記を対象外とすることで、
読解の前提を一定にしたまま参照の同一性を保つ。
Document Title（文書題名）およびHeading Label（見出しラベル）を
対象へ含めるのは、
これらが読み手にとって本文へ到達する前の自然言語表現であり、
本文と言語が分かれると、
同一のDocumentation Asset（文書資産）の中で
読解の前提が二分されるためである。

**Note:** 本Rule（ルール）が定めるのは、
対象とする自然言語表現の言語のみである。
文末表現、Voice（態）、文長、Typography（文字表現）は
本Rule（ルール）が定めない。

Heading Label（見出しラベル）を対象とすることは、
Section Identity（Section同一性）、
Standard Section（標準Section）、
Heading Level（見出しレベル）、
Markdown Heading Marker（Markdown見出し記号）について
何も定めない。
本Rule（ルール）は、
固定のHeading Catalog（見出し一覧）および
固定翻訳Catalog（翻訳一覧）を持たない。

Commit Message（コミットメッセージ）の
Message Language（メッセージ言語）は
[Commit Convention](commit.md)
が所有する。

### Terminology（用語）

#### WRT-SF-002 — Formal English Term Representation

**Rule ID:** `WRT-SF-002`

**Rule Name:** Formal English Term Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Repository内で特定のConcept（概念）・Responsibility（責務）・
Role（役割）等を安定して識別するために使用する
Formal English Term（正式英語用語）は、
英語用語に日本語説明を併記した
`English Term（日本語説明）` の形式で表現する。

この形式は初出箇所に限らず、
その用語をFormal English Term（正式英語用語）として
使用する箇所へ適用する。
この箇所には、
Natural Language Prose（自然言語本文）に加えて、
Human-readable（人間可読）なDocument Title（文書題名）および
Heading Label（見出しラベル）が含まれる。

Repository固有の識別を担わず、
一般に通用する意味で使用される
Ordinary Technical Term（一般技術用語）は、
本Rule（ルール）の対象ではない。

**Reason:** Formal English Term（正式英語用語）は、
一般的な英単語と同じ語形を持ちながら、
Repository内では特定のConcept（概念）を指す。
日本語説明の併記がなければ、
読み手はその語が一般語として使われているのか
特定のConcept（概念）を指しているのかを判別できず、
Semantic Meaning（意味）が読み手ごとに分岐する。
初出箇所に限定しないのは、
Documentation Asset（文書資産）が
先頭から通読されるとは限らず、
Section（節）単位または検索経由での参照において
初出箇所の併記が読み手へ届かないためである。

**Note:** 本Rule（ルール）は、
どの用語がFormal English Term（正式英語用語）に当たるかの
Catalog（一覧）を保持せず、
Glossary（用語集）・Term Registry（用語登録簿）等の
用語管理機構を前提としない。

本Rule（ルール）は
Term Taxonomy（用語分類体系）を定義しない。
区別されるのは、
その箇所においてRepository固有の識別を担っているかどうかである。

日本語説明の文言そのものを固定するCatalog（一覧）は
本Rule（ルール）が定めない。
Document Title（文書題名）およびHeading Label（見出しラベル）についても、
固定のHeading Catalog（見出し一覧）および
固定翻訳Catalog（翻訳一覧）は成立しない。
同一のFormal Concept（正式概念）に対する
日本語説明の一貫性は `WRT-SF-003` が扱う。

Rule ID（規約ルールID）、Rule Name（ルール名）等、
対象を識別するIdentifier（識別子）または
Label（ラベル）としての表記は、
Formal English Term（正式英語用語）としての使用ではない。

#### WRT-SF-003 — Formal Term Consistency

**Rule ID:** `WRT-SF-003`

**Rule Name:** Formal Term Consistency

**Stability:** Development

**Requirement:** MUST

**Rule:** 同一のFormal Concept（正式概念）を参照する場合、
同じFormal English Term（正式英語用語）と、
それに対応する同じ日本語説明を使用する。

本Rule（ルール）は、
Natural Language Prose（自然言語本文）における参照に加えて、
Human-readable（人間可読）なDocument Title（文書題名）および
Heading Label（見出しラベル）における参照へ適用する。

本Rule（ルール）が対象とするのは
Formal Concept（正式概念）への参照であり、
Formal English Term（正式英語用語）として参照していない
通常の説明文における語の選択は対象ではない。

**Reason:** 同一のFormal Concept（正式概念）が
箇所ごとに異なる用語で現れると、
読み手はそれらが同じConcept（概念）を指すのか
別のConcept（概念）を指すのかを判定できず、
用語の同一性による参照が成立しなくなる。
対応する日本語説明まで含めて一貫させるのは、
説明側が揺れると、
同じ英語用語であってもConcept（概念）の範囲が
異なって読まれるためである。

**Note:** 本Rule（ルール）が要求するのは
Formal Term Consistency（正式用語一貫性）であり、
文章全体で同じ単語を機械的に反復することではない。

````text
Formal Term Consistency
≠ Mechanical Word Repetition
````

通常の説明文において、
読みやすさのために語や言い回しを変えることは
本Rule（ルール）が禁じるところではない。

### Semantic Clarity（意味の明確性）

#### WRT-SF-004 — Semantic Reference Clarity

**Rule ID:** `WRT-SF-004`

**Rule Name:** Semantic Reference Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Subject（主体）、Responsibility Holder（責務主体）、
Reference Target（参照対象）等について、
その文脈で複数の合理的解釈が成立する場合は、
対象を明示する。

**Reason:** これらは、文がどの対象について何を述べているかを
確定させる要素である。
複数の解釈が成立したまま残ると、
読み手ごとに異なる対象へ内容が適用され、
Documentation Asset（文書資産）が伝えるはずの
Semantic Meaning（意味）が読み手側で分岐する。
明示を求める条件を
複数の合理的解釈が成立する場合に限定するのは、
文脈から対象が一意に定まる箇所にまで
反復的な明示を強いないためである。

**Note:** 本Rule（ルール）が対象とするのは
解釈の分岐であり、特定の語や文型ではない。

「これ」「それ」「上記」等の指示語、および
日本語における主語の省略それ自体は、
本Rule（ルール）が禁じるところではない。
これらの表現が用いられている場合であっても、
対象が一意に定まるならば本Rule（ルール）は適用されない。

### Normative Writing（規範的記述）

#### WRT-SF-005 — Normative Strength Consistency

**Rule ID:** `WRT-SF-005`

**Rule Name:** Normative Strength Consistency

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Rule Statement（ルール文）の
Natural Language Representation（自然言語表現）は、
そのNormative Rule（規範的ルール）が宣言する
Requirement Level（要求レベル）と異なる
Normative Strength（規範強度）を導入してはならない。

**Reason:** Requirement Level（要求レベル）は、
そのRule（ルール）が要求・禁止・推奨・許容のいずれであるかを
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
本Rule（ルール）はそれを再定義せず、
宣言と表現の一致のみを要求する。

本Rule（ルール）は、
Requirement Level（要求レベル）ごとに使用してよい
文末表現のCatalog（一覧）を定めない。

#### WRT-SF-006 — Normative Condition Clarity

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
そのRule（ルール）が適用されるかどうかを分ける要素である。
判断基準を伴わない表現だけでそれが示されると、
適用の可否が読み手の裁量で決まり、
Rule（ルール）が対象へ及ぶ範囲が箇所ごとに変わる。
判断可能な形を要求することで、
適合の判定を記述内容から行える。

**Note:** 本Rule（ルール）が対象とするのは、
Normative Meaning（規範的意味）を左右する箇所である。
Non-normative Content（非規範的内容）における
同種の表現は本Rule（ルール）の対象ではない。

本Rule（ルール）は
Prohibited Word Catalog（禁止語一覧）を定義しない。
挙げた表現は、
判断基準を伴わない記述の例示であり、
語そのものの使用可否を定めるものではない。

### Definition Writing（定義の記述）

#### WRT-SF-007 — Definition Clarity

**Rule ID:** `WRT-SF-007`

**Rule Name:** Definition Clarity

**Stability:** Development

**Requirement:** MUST

**Rule:** Definition（定義）としてConcept（概念）を成立させる文章は、
Definition Target（定義対象）を識別可能にし、
その対象が何であるかを肯定的に示す。
Negative Statement（否定文）、
他のConcept（概念）との差分、
およびExample（例）は、
この肯定的な記述の代替として用いない。

**Reason:** Definition（定義）が果たすべきことは、
その対象が何であるかを確定させることである。
何でないか、何と異なるか、どのような場合があるかだけが示されると、
対象の輪郭は示された事項の外側として残るのみであり、
読み手ごとに異なる範囲で解釈される。
肯定的な記述を要求することで、
Concept（概念）の成立が
他の記述の有無や読み手の補完に依存しなくなる。

**Note:** 本Rule（ルール）は
Definition Model（定義モデル）、すなわち
Definition（定義）が意味上どのような要素から成るかの
Model（モデル）を定義しない。
要求するのは、
Definition Target（定義対象）の識別可能性と、
肯定的な記述の存在である。

Negative Statement（否定文）、他のConcept（概念）との差分、
Example（例）は、理解を助ける記述として有用である。
本Rule（ルール）が対象とするのは、
それらが肯定的な記述の位置を占める場合である。
肯定的な記述が成立したうえでこれらを併記することは、
本Rule（ルール）が禁じるところではない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `WRT-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Field（フィールド）を規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書は、自身が定めるRule（規則）にも従っている。

- Natural Language Prose（自然言語本文）、
  Document Title（文書題名）、およびHeading Label（見出しラベル）を
  日本語で記述している。
- Formal English Term（正式英語用語）を、
  Natural Language Prose（自然言語本文）および
  Heading Label（見出しラベル）のいずれにおいても
  `English Term（日本語説明）` の形式で表現している。
- 同一のFormal Concept（正式概念）に対して、
  同じFormal English Term（正式英語用語）と
  同じ日本語説明を使用している。
- 各Rule Statement（ルール文）の表現を、
  宣言したRequirement Level（要求レベル）へ一致させている。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
