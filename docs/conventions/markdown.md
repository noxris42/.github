# Markdown Convention（Markdown規約）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Documentation（Repository文書）がMarkdownで記述される場合の
Markdown SyntaxおよびMarkup Representationについて、
既に成立しているMeaning（意味）およびSemantic Structure（意味構造）を変更せず、
一貫したPhysical Representation（物理表現）を成立させる
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の3点である。

1. 既に成立しているMeaning（意味）およびSemantic Structure（意味構造）は、
   Markdown上のどのMarkupによって表現されるのか。
2. 同一の対象に対して複数のMarkdown Representationが成立し得る場合、
   どの表現を使用するのか。
3. Markdown側の表現上の都合が、
   Semantic Structure（意味構造）・Physical Name（物理名称）・
   Natural Language Representation（自然言語表現）等の定義へ
   波及しないために、どの境界を保つのか。

[Convention Architecture](../architecture/convention.md)
は、Markdown等の特定の記述媒体上での表現方法を意図的に定義しない。
[Documentation Structure Architecture](../architecture/documentation-structure.md)
は、SectionとHeading（見出し）・
Markdown Heading Marker（Markdown見出し記号）との
具体的なMappingを定義せず、後続のConvention（規約）へ委譲している。

本文書は、Markdownという記述媒体上の表現を担う
Convention Asset（規約資産）として成立する。
ただし本文書が引き受けるのは、
Markdown上のMarkup Representationに限られる。
本文書は、上位設計および他のConvention（規約）が定義する
Concept（概念）・Meaning（意味）・Semantic Structure（意味構造）を
再定義しない。

## Relationships（関係）

本文書は、次を上位Sourceとして参照する。

- [Repository Governance](../architecture/repository-governance.md)
- [Documentation Structure Architecture](../architecture/documentation-structure.md)
- [Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

本文書は
[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Markdownで記述されるRepository Documentation（Repository文書）という
反復して成立する対象へ繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Areaを代表・集約するAssetではない。

### Responsibility Boundary（責務境界）

本文書が担うのは、
Markdown上のMarkup Representationに限られる。
隣接する責務との境界は次である。

```text
Semantic Structure、Section、
Section Responsibility、
Standard Section Identity
    → Documentation Structure Architecture、および
      Documentation Structure Convention

Document Titleの意味、
Heading Label等のNatural Language Representation、
日英表記、文体、用語選択
    → Documentation Structure Architecture、および
      Writing Convention

File名、Directory名、Path等のPhysical Name
    → Naming Convention

Convention固有のRule Presentation
（Rule ID Format、Rule Field、
Rule Section Heading Representation）
    → Convention Authoring Convention

Markdown SyntaxおよびMarkup Representation
    → 本文書
```

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は本文書の外にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- SectionとSection Responsibility（Section責務）、
  およびResponsibility Decomposition（責務分解）
- `Section ≠ Heading` をはじめとする
  Logical / Representation Boundary
- Document Title（文書題名）の意味と、
  それをIdentity（同一性）・Document Responsibility（文書責務）・
  Documentation Area（文書責務領域）への所属から導出しないこと
- Standard Section（標準Section）と
  Standard Section Heading Representation（標準Section見出し表現）
- Human-readable Natural Language Representation（人間可読な自然言語表現）、
  およびCanonical Japanese Support（正規日本語補助）の表示
- Physical Name（物理名称）とその形式
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的規則）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（規則モデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（規則同一性）とその安定性
- Rule ID Format（規則ID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  Rule Section Heading Representation（Rule Section見出し表現）、
  StabilityのField表現
- Namespace Code（名前空間コード）の割当

本文書は、Markdown側から
Section、Document Title（文書題名）、Physical Name（物理名称）、
およびNatural Language Representation（自然言語表現）の
Meaning（意味）を成立させない。

### Position（設計上の位置づけ）

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture
        ▲
        │ refines
Markdown Convention

Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Markdown Convention
```

本文書は、他のConvention Asset（規約資産）が定めるRuleを
Markdown上で表現する場合の表現を扱うが、
それらのRuleのNormative Meaning（規範的意味）を変更しない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 本文書のRuleが適用されるMarkdown Representationの
  Markdown Baselineの定義
- Document Title（文書題名）をMarkdown上で表現する場合の
  Markdown Heading Marker（Markdown見出し記号）
- Heading（見出し）をMarkdown上で表現する場合の
  Heading Level（見出しレベル）の使用
- Heading（見出し）として表現する対象に対する
  Markdown Syntaxの選択、およびHeading Syntaxの表現
- EmphasisおよびStrong EmphasisのMarker表現
- 列挙をMarkdown上で表現する場合のList Representation、
  およびList Markerと番号の表現
- 対応関係をMarkdown上で表現する場合のTable Representation、
  およびTableのSource上の表現
- 引用をMarkdown上で表現する場合のBlockquote Representation
- CodeおよびLiteral StringをMarkdown上で表現する場合の
  Code Block RepresentationおよびInline Code Representation、
  ならびにそれらのFenceおよびDelimiterの表現
- LinkをMarkdown上で表現する場合のLink Syntaxの選択
- 同一Repository内の対象を参照する場合の
  Link Reference Representation
- Image RepresentationにおけるAlt Textの保持
- Markdown Source上のBlock Spacingおよび行末表現
- Markdown RepresentationとHTMLの選択

### Out of Scope（本文書が定義しない範囲）

- Section、Section Responsibility（Section責務）、
  およびResponsibility Decomposition（責務分解）の
  Semantic Model（意味モデル）
- SectionとHeading（見出し）のMapping Rule（対応規則）、
  およびSection構成の要否
- Standard Section（標準Section）の定義・適用・
  Presence Requirement（設置要求）、および
  Standard Section Heading Representation（標準Section見出し表現）の
  値とその定義権限
- Document Title（文書題名）の意味、
  Title Component（題名構成要素）およびComposition Rule（構成規則）
- Heading Label（見出しラベル）その他の
  Natural Language Representation（自然言語表現）、
  日英表記、文体、用語選択、Alt Textの文章品質、
  およびLink Textの自然言語品質
- File名、Directory名、Path等の
  Physical Name（物理名称）の形式および選択
- Rule ID Format（規則ID形式）、Rule Field（規則フィールド）、
  Rule Section Heading Representation（Rule Section見出し表現）等、
  Convention（規約）固有のRule Presentation
- Section間のHorizontal Rule、
  Documentation Asset（文書資産）全体にわたる
  Heading（見出し）の一意性、
  およびList Nestingの深さ制限
- Line Length上限およびHard Wrap
- File Encoding、Byte Order Mark、Final Newline等の
  Repository全体のFile Property
- Front Matter、Metadata、およびそれらのSchema
- Lint、Validator、Formatter、Editor等の
  External Toolの設定・実行・適合判定、
  およびそれらのRuleとの対応関係
- Markdownを使用しない記述媒体上の表現
- Markdown Rendererの実装差異の完全なCatalog

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: MDK
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的規則）を読むための補足である。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。

### Representation Boundary（表現の境界）

本文書が扱うのはMarkdown上の表現であり、
表現から意味を導出しない。

```text
Markdown Heading Marker ≠ Heading
Heading                 ≠ Section
Heading Level           ≠ Section Responsibility Decomposition
Markdown Representation ≠ Document Title
Inline Code             ≠ Physical Name Definition
```

Heading Level（見出しレベル）およびMarkdown上の入れ子は、
読み手が構造を把握するためのRepresentation（表現）である。
Section間の責務関係は、
Documentation Structure Architecture（文書構造アーキテクチャ）が定める
Responsibility Decomposition（責務分解）によって成立するのであり、
Markdown Representationからは成立しない。

### External Tool Handling（External Toolの扱い）

Lint、Validator、Formatter、Editor等はExternal Toolであり、
本文書の外にある。

External Toolが報告するErrorは、
あるMarkdown Representationを検討するきっかけとなり得る。
しかし本文書のNormative Rule（規範的規則）は、
External ToolのRuleを根拠として成立しない。
各RuleのReasonは、
そのRuleが成立させようとしている表現上の必要から記述される。

本文書は、External ToolのRule識別子、
External Toolとの対応関係、
およびExternal Toolの設定を保持しない。
Ruleの粒度は、
External ToolのRule単位ではなく、
Normative Meaning（規範的意味）の単位で定める。

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規則ID）はCategory（分類）を表現しない。

各Ruleは、Markdown上の表現のみを対象とする。
Ruleが適用されるのは、
対象がMarkdownで記述され、
かつそのRuleが対象とする表現がその文書上に現れる場合である。
本文書のいずれのRuleも、
Documentation Asset（文書資産）に対して
Document Title（文書題名）・Heading（見出し）・List・Table・
Blockquote・Code・Link・Image等を
設けること自体を要求しない。

### Markdown Baseline（Markdown基準）

#### MDK-SF-001 — Markdown Baseline（Markdown基準）

**Rule ID:** `MDK-SF-001`

**Rule Name:** Markdown Baseline

**Stability:** Development

**Requirement:** MUST

**Rule:** 本文書のRuleは、
GitHub上でRepository Documentation（Repository文書）として
表示・解釈可能なMarkdown Representationを
Markdown Baselineとして適用する。

**Reason:** Markdownには複数の仕様と実装が存在し、
同じ記述が受け手によって異なる結果へ解釈され得る。
Baselineが定まっていなければ、
以降のRuleがどの解釈のもとで成立しているかが確定せず、
ある環境では意図した表現になり、
別の環境では成立しないという分岐を
Rule側から判別できない。
Repository Documentation（Repository文書）が実際に読まれる場である
GitHub上での表示・解釈をBaselineとすることで、
各Ruleが前提とする解釈が一意に定まり、
Ruleへの適合が読み手の受け取る結果と対応する。

**Note:** 本Ruleは、
GitHub上で表示・解釈可能なSyntaxをすべて使用することを要求しない。
GitHub上で利用可能であることは、
その記法を使用しなければならないことを意味しない。

本Ruleは、Baselineを特定の単一のMarkdown仕様だけへ限定しない。

個々のSyntaxまたはRepresentation（表現）を使用するかどうかは、
以降のNormative Rule（規範的規則）が定める。

### Document and Heading Representation（DocumentおよびHeadingの表現）

#### MDK-SF-002 — Document Title Heading Representation（文書題名の見出し表現）

**Rule ID:** `MDK-SF-002`

**Rule Name:** Document Title Heading Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Markdownで記述されたDocumentation Asset（文書資産）において、
Document Title（文書題名）をMarkdown上で表現する場合、
Heading Level（見出しレベル）1を使用する。

Heading Level（見出しレベル）1は、
Document Title（文書題名）以外の目的へ使用しない。

**Reason:** Document Title（文書題名）は、
読み手がその文書の扱う対象を最初に受け取る表現であり、
文書内の他のHeading（見出し）とは表示上区別されている必要がある。
最上位のHeading Level（見出しレベル）を
Document Title（文書題名）の表現へ限定すると、
読み手も、Markdownを解釈するRendererその他の受け手も、
どの表現が題名としての位置を占めているかを
文書ごとの解釈なしに一意に取り出せる。
Heading Level（見出しレベル）1を他の目的にも使用すると、
同じ表示上の位置を複数の対象が占め、
その区別が失われる。

**Note:** 本Ruleは、
Documentation Asset（文書資産）が
Document Title（文書題名）を持つことを要求せず、
それをMarkdown上へ表現することも要求しない。
表現する場合の表現のみを定める。

本Ruleは、Heading Level（見出しレベル）1で表現されていることから
Document Title（文書題名）としてのMeaning（意味）を
成立させたり推論させたりしない。
Document Title（文書題名）の意味、
およびその構成は
[Documentation Structure Architecture](../architecture/documentation-structure.md)
および
[Writing Convention](writing.md)
が所有する。
本Ruleはこれらを再定義しない。

Heading Level（見出しレベル）1を
Document Title（文書題名）以外へ使用しないことにより、
文書内でHeading Level（見出しレベル）1が
複数の対象を表現することは生じない。
本Ruleは、そのためのRuleを別に設けない。

#### MDK-SF-003 — Heading Level Continuity（見出しレベルの連続性）

**Rule ID:** `MDK-SF-003`

**Rule Name:** Heading Level Continuity

**Stability:** Development

**Requirement:** MUST

**Rule:** Markdown上でHeading（見出し）を表現する場合、
直前のHeading（見出し）より深いHeading Level（見出しレベル）を
使用するときは、1段だけ深いHeading Level（見出しレベル）を使用する。
Heading Level（見出しレベル）を飛ばして深くしない。

**Reason:** Heading Level（見出しレベル）は、
読み手・Renderer・Outline生成のいずれに対しても
入れ子の深さとして解釈される。
深さが飛ぶと、その位置には対応する表現が存在しないため、
読み手は欠けた段が省略されたのか、
それとも表現上の誤りなのかを判断できない。
深くする際の増分を1段に固定することで、
Markdown上の入れ子の深さが表現として一意に読み取れる。

**Note:** 本Ruleは、
浅いHeading Level（見出しレベル）へ戻る場合の
段数を制限しない。

本Ruleが定めるのはMarkdown上の表現に限られる。
SectionのSemantic Parent / Child関係を
Heading Level（見出しレベル）から定義せず、推論もしない。
Section間の責務関係は
[Documentation Structure Architecture](../architecture/documentation-structure.md)
が定めるResponsibility Decomposition（責務分解）によって成立する。

本Ruleは、
どのSectionをHeading（見出し）として表現するか、
およびHeading（見出し）を設けるかどうかを定めない。

#### MDK-SF-004 — Heading Syntax Representation（見出し記法の表現）

**Rule ID:** `MDK-SF-004`

**Rule Name:** Heading Syntax Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Markdown上でHeading（見出し）を表現する場合、
ATX Heading Syntaxを使用する。

Heading Level（見出しレベル）は、
行頭のOpening `#` Markerの個数で表し、
Marker直後にASCII Spaceを1つ置く。

Setext Headingを使用しない。
Closing `#` Markerを使用しない。

Canonical Formは次である。

```text
# Heading
## Heading
### Heading
```

**Reason:** Markdownは同じHeading（見出し）に対して
複数の記法を認めており、
どれを使用しても表示上の結果は変わらない。
記法が箇所ごとに分かれると、
Heading（見出し）を探す側は複数の形を同時に想定することになり、
Source上でHeading（見出し）を一意の形として扱えない。
Setext Headingは表現できるHeading Level（見出しレベル）が限られ、
下線行を失うだけでHeading（見出し）でなくなるため、
Level（レベル）を変えるだけの編集にも別の記法への移行を伴う。
Closing `#` MarkerとMarker直後の空白の揺れも、
表示に現れないまま差分だけを生む。
Heading Level（見出しレベル）をOpening Markerの個数だけで表す
1つの形へ固定することで、
すべてのHeading（見出し）が同じ形で現れ、
Level（レベル）の変更もMarkerの個数の変更として完結する。

**Note:** 本Ruleが定めるのはHeading（見出し）の記法である。
Heading Level（見出しレベル）の飛びは
`MDK-SF-003` が扱う。
どの対象をHeading（見出し）として表現するかは
本Ruleの対象ではない。

Heading Label（見出しラベル）の
Natural Language Representation（自然言語表現）は
[Writing Convention](writing.md)
が所有する。

#### MDK-SF-005 — Sibling Heading Uniqueness（同一親配下の見出しの一意性）

**Rule ID:** `MDK-SF-005`

**Rule Name:** Sibling Heading Uniqueness

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 同一のParent Heading（親見出し）の配下では、
同一のHeading Representation（見出し表現）を
重複させるべきではない。

**Reason:** Markdown上のHeading（見出し）は、
文書内の位置を指し示すために使用される。
同一のParent Heading（親見出し）の配下に
同じ表現のHeading（見出し）が複数現れると、
その表現ではどちらを指しているかを特定できず、
読み手も参照する側も、
前後の本文を読むまで対象を決められない。
同じ範囲の中で表現を重複させないことで、
Heading（見出し）が位置の指示として機能する。

**Note:** 本Ruleは、
異なるParent Heading（親見出し）の配下に
同一のHeading Representation（見出し表現）が現れることを制限しない。
異なる文脈で同じ表現が成立することは、
それ自体では指示の曖昧さを生じさせない。

本Ruleは、Documentation Asset（文書資産）全体にわたる
Heading（見出し）の一意性を要求しない。

Heading Label（見出しラベル）の
Natural Language Representation（自然言語表現）は
[Writing Convention](writing.md)
が所有する。
Standard Section Heading Representation（標準Section見出し表現）の
値およびその再利用は
[Documentation Structure Convention](documentation-structure.md)
が所有する。
本Ruleはこれらを再定義せず、
定義済みの表現の使用を妨げない。

#### MDK-SF-006 — Emphasis as Heading Substitute（強調記法による見出しの代用）

**Rule ID:** `MDK-SF-006`

**Rule Name:** Emphasis as Heading Substitute

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Heading（見出し）として表現する対象に対して、
Emphasis Syntaxを
Heading Syntaxの代用として使用してはならない。

**Reason:** Emphasis Syntaxは、
文中の一部を強調するための表現であり、
Markdownを解釈する側にとってはHeading（見出し）ではない。
Heading（見出し）として意図した表現を
Emphasis Syntaxで代用すると、
その表現はOutline上に現れず、
文書内の位置として参照することもできない。
見た目が近いことは、
表現としての役割が同じであることを意味しない。
Heading（見出し）として表現する対象へ
Heading Syntaxを使用することで、
その表現がHeading（見出し）として扱われる。

**Note:** 本Ruleが禁止するのは、
Heading（見出し）としての代用に限られる。

強調としてのEmphasis Syntaxの使用は本Ruleの対象ではない。
Rule Field（規則フィールド）のField名の表示のように、
Heading（見出し）ではないLabelを
Emphasis Syntaxで表現することも、本Ruleは禁止しない。
Rule Field（規則フィールド）のMarkdown表現は
[Convention Authoring Convention](convention-authoring.md)
が所有する。

本Ruleは、
どの対象をHeading（見出し）として表現するかを定めない。

#### MDK-SF-007 — Emphasis Marker Representation（強調記号の表現）

**Rule ID:** `MDK-SF-007`

**Rule Name:** Emphasis Marker Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Markdown上でEmphasisを表現する場合はアスタリスク1個 `*` を、
Strong Emphasisを表現する場合はアスタリスク2個 `**` を
Markerとして使用する。

アンダースコア `_` および `__` を
Emphasis Markerとして使用しない。

Canonical Formは次である。

```text
*Emphasis*
**Strong Emphasis**
```

**Reason:** Markdownは同一のEmphasisに対して
アスタリスクとアンダースコアの双方を認めており、
どちらを使用しても表示上の結果は変わらない。
Markerが箇所ごとに分かれると、
同じ意味の表現がSource上で複数の形を持ち、
検索・置換・差分のいずれもその形ごとに分かれる。
またアンダースコアは、Identifier（識別子）その他の
Literal Stringの構成文字として現れるため、
記法として使用すると、
文字としての出現と記法としての出現が同じ文字で混在する。
Markerをアスタリスクの1個と2個へ固定することで、
Emphasisの表現が1つの形に定まり、
アンダースコアは文字としての出現のみを担う。

**Note:** 本Ruleが定めるのはEmphasis Markerの表現である。
どこにEmphasisを用いるか、
およびHeading（見出し）としての代用の禁止は
本Ruleの対象ではなく、
後者は `MDK-SF-006` が扱う。

本Ruleは、Emphasisの入れ子および
Emphasis範囲の取り方を定めない。

### List and Content Representation（ListおよびContentの表現）

#### MDK-SF-008 — Unordered List Representation（順不同列挙の表現）

**Rule ID:** `MDK-SF-008`

**Rule Name:** Unordered List Representation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 順序そのものに意味を持たない列挙をMarkdown上で表現する場合、
Unordered Listを使用すべきである。

**Reason:** Markdown上のListは、
複数の項目が並列であることを表現として示す。
並列の項目を段落や1行の羅列として記述すると、
どこからどこまでが1項目かを読み手が本文から復元することになり、
項目の追加・削除の影響範囲も表現から読み取れない。
順序に意味を持たない列挙をUnordered Listで表現すると、
項目の境界と並列性が表現として現れ、
同時に、順序へ意味がないことも読み手へ伝わる。

**Note:** 本Ruleは、
どの内容を列挙として構成するかを定めない。

本Ruleは、Listの入れ子の深さを制限せず、
深いListを理由にSectionを構成することを要求しない。
Section構成は
[Documentation Structure Convention](documentation-structure.md)
が所有する。

#### MDK-SF-009 — Ordered List Representation（順序付き列挙の表現）

**Rule ID:** `MDK-SF-009`

**Rule Name:** Ordered List Representation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 順序そのものに意味を持つ列挙をMarkdown上で表現する場合、
Ordered Listを使用すべきである。

**Reason:** 手順・段階・優先順位のように、
項目の並び自体が意味を持つ場合、
その並びは表現から読み取れなければならない。
Unordered Listで表現すると、
記述された並びが意味を持つのか、
単に記述順にすぎないのかを読み手が判別できず、
順序を根拠として参照することもできない。
Ordered Listで表現することで、
順序が意味を持つことと、
各項目がその並びのどこに位置するかが表現として確定する。

**Note:** 本Ruleは、
Ordered ListのMarker表記および番号の付け方を定めない。

順序に意味を持たない列挙は本Ruleの対象ではなく、
`MDK-SF-008` が扱う。

#### MDK-SF-010 — Unordered List Marker（順不同Listの記号）

**Rule ID:** `MDK-SF-010`

**Rule Name:** Unordered List Marker

**Stability:** Development

**Requirement:** MUST

**Rule:** Unordered ListのList Markerには、
ハイフン `-` を使用し、
Markerの直後にASCII Spaceを1つ置く。

Canonical Formは次である。

```text
- Item
```

**Reason:** MarkdownはUnordered ListのMarkerとして
複数の記号を認めており、
いずれを使用しても表示上の結果は変わらない。
Markerの直後の空白数についても同様に、
複数の記述が同じ表示へ落ちる。
そのため記述者ごと・箇所ごとにこれらが分岐しても
表示からは気づかれず、
Markdown Sourceを読む側と編集する側だけが差異を負う。
MarkerとMarker直後の空白を1つの形へ固定することで、
Sourceの見た目とDiffが対象の違いだけを反映し、
表示上の結果を伴わない差分が生じない。

**Note:** 本Ruleが定めるのはUnordered ListのMarkerと
その直後の空白であり、
Ordered ListのMarker表記は本Ruleの対象ではない。

本Ruleは、Indent幅、
およびList Itemの継続行の表現を定めない。

#### MDK-SF-011 — Ordered List Marker and Numbering Representation（順序付きListの記号と番号の表現）

**Rule ID:** `MDK-SF-011`

**Rule Name:** Ordered List Marker and Numbering Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Ordered ListのList Markerは、
十進数の番号にピリオド `.` を続け、
その直後にASCII Spaceを1つ置いた形とする。

各ItemのSource上の番号は、
意図されたOrdered Sequenceにおけるその項目の番号を明示し、
連続するItemでは順に増加させる。

Canonical Formは次である。

```text
1. First
2. Second
3. Third
```

**Reason:** Ordered Listは、
項目の並び自体が意味を持つ場合に使用される。
その番号がSource上に現れていなければ、
Sourceを読む側は表示された結果を見るまで
各項目が何番目として意図されているかを確認できず、
項目の移動・挿入が意図した順序を保っているかも
Source上では判断できない。
すべての行を同じ番号で記述してRendererの採番へ委ねる形は、
表示上は成立するが、
意図された順序をSourceから失わせるため、
Canonical Formとしない。
番号を順に増加させることで、
Source上の並びと意図された順序が一致し、
差分もその変化だけを示す。

**Note:** 本Ruleは開始番号を `1` へ固定しない。
意図されたSequenceが途中から始まる場合、
その番号から始めることは本Ruleに反しない。

```text
3. Third
4. Fourth
5. Fifth
```

本Ruleが定めるのはOrdered ListのMarkerと番号の表現であり、
Unordered ListのMarkerは `MDK-SF-010` が扱う。

本Ruleは、Indent幅、
およびList Itemの継続行の表現を定めない。

#### MDK-SF-012 — Table Representation（対応関係の表現）

**Rule ID:** `MDK-SF-012`

**Rule Name:** Table Representation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 複数の対象について、
同じ観点による比較または対応関係を表現する内容が、
RowとColumnによって明確に表現できる場合、
Tableを使用すべきである。

**Reason:** 比較・対応の内容は、
どの対象のどの観点についての記述かという2つの軸を同時に持つ。
これを本文やListで表現すると、
2つの軸は記述の順序としてしか現れず、
読み手は対応関係を読み進めながら組み立て直すことになる。
またある対象について観点が欠けていても、
表現からはそれが読み取れない。
Tableで表現すると、
2つの軸が行と列としてそのまま現れ、
対応と欠落の双方を表現から確認できる。

**Note:** 本Ruleは、
RowとColumnによって明確に表現できない内容へTableを要求しない。
Tableとして表現するために内容を切り詰めることは、
本Ruleが求めるものではない。

本Ruleは、Tableの列数・整列・
Header行の内容を定めない。

#### MDK-SF-013 — Table Source Representation（TableのSource表現）

**Rule ID:** `MDK-SF-013`

**Rule Name:** Table Source Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** TableをMarkdown上で表現する場合、
各RowはLeading PipeとTrailing Pipeを持つ。

Cell ContentがあるCellは、
Cell Contentと両側のPipeとの間にASCII Spaceを1つ置く。
Cell Contentが空のCellは、
隣接するPipeの間にASCII Spaceを1つだけ置く。

Alignmentを指定しないDelimiter Cellは `---` とする。

Visual Column Widthを揃える目的で
Cell内へSpace Paddingを行わない。
これは空のCellについても同様である。
同じ目的でDelimiter Cellのハイフンの個数を増やさない。

Canonical Formは次である。

```text
| Column A | Column B |
| --- | --- |
| Value A | Value B |
| Value C | |
```

**Reason:** Markdown SourceのCell幅は、
表示されるTableの列幅とは対応しない。
表示側の列幅はContentとFontおよびRendererによって決まるため、
Source上でPaddingを揃えても、
その見た目が表示に現れる保証はない。
一方でPaddingを維持する場合、
あるCellの内容が1文字変わるだけで
同じ列の他のすべての行を書き換えることになり、
差分は内容の変更ではなく桁揃えの追従で占められる。
Source上の形をContentだけで決まる1つの形へ固定することで、
Markdown SourceがRendering Widthを模倣しなくなり、
差分が内容の変化だけを示す。

**Note:** Alignment自体に意味がある場合、
Delimiter CellへColonを用いてAlignmentを指定することは
本Ruleに反しない。

```text
| Left | Right | Center |
| :--- | ---: | :---: |
```

本Ruleが定めるのはTableのSource上の形である。
どのような場合にTableを使用するかは
`MDK-SF-012` が扱う。

本Ruleは、列数、Header行の内容、
およびCell内の記述内容を定めない。

本Ruleは、空のCellを使用することを要求せず、
Cellが空であることが何を意味するかも定めない。
定めるのは、空のCellを使用する場合のSource上の形に限られる。

#### MDK-SF-014 — Blockquote Representation（引用の表現）

**Rule ID:** `MDK-SF-014`

**Rule Name:** Blockquote Representation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 他の情報源からの引用として提示する内容をMarkdown上で表現する場合、
Blockquote Syntaxを使用すべきである。

**Reason:** 引用は、
その文書自身の記述ではなく、
他の情報源に由来する内容である。
両者が同じ表現で並ぶと、
読み手はどこまでが当該文書の記述で、
どこからが引用された内容かを判別できず、
記述の帰属が失われる。
Blockquote Syntaxで表現することで、
引用の範囲が表現として明示され、
当該文書自身の記述と区別される。

**Note:** 本Ruleは、
Blockquote Syntaxを引用以外の目的で使用することを禁止しない。
本Ruleが定めるのは、
引用として提示する内容についての表現である。

引用元の示し方、および引用の是非は本Ruleの対象ではない。

### Code Representation（Codeの表現）

#### MDK-SF-015 — Fenced Code Block Representation（Code Blockの表現）

**Rule ID:** `MDK-SF-015`

**Rule Name:** Fenced Code Block Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Code BlockをMarkdown上で表現する場合、
Fenced Code Blockを使用する。

Fence MarkerにはBacktickを使用し、
通常はBacktick 3個をFence Lengthとする。
Contentとの衝突を避ける必要がある場合に限り、
衝突しない必要最小の長さまでFence Lengthを増やす。
OpeningとClosingのFenceは対応する長さとする。
Tilde FenceをCanonical Formとして使用しない。

通常のCanonical Formは次である。

````text
```text
content
```
````

**Reason:** Fenced Code Blockは、
開始と終了の位置を明示的な区切りとして持つ。
Indentによって表現されたCode Blockは、
先頭の空白の有無だけが境界の根拠となるため、
List等の入れ子の中では周囲のIndentと区別できず、
編集時の空白の増減で範囲が意図せず変化する。
また空行を含む内容では、
どこまでがBlockかが表現から確定しない。
明示的な区切りを持つ表現へ固定することで、
Code Blockの範囲が周囲の記述に依存せず確定し、
`MDK-SF-016` が定める識別子の付与も同じ位置で成立する。

Fence MarkerとしてBacktickとTildeのいずれも使用できる状態では、
同じ内容が箇所ごとに異なるFenceで書かれ、
表示上の結果は変わらないまま
Sourceの読み取りと編集だけが分岐する。
またFence Lengthを内容と無関係に増やすと、
その長さが衝突回避のためのものか
単なる記述上の揺れかを区別できない。
Fence Markerを1つへ固定し、
長さの増加を衝突回避に必要な場合へ限定することで、
Fenceの形そのものが内容についての情報を持つ。

**Note:** 本Ruleは、
どの内容をCode Blockとして表現するかを定めない。

Code Block自身がMarkdownのFenceを内容として含む場合のように、
Backtick 3個では内容と衝突する場合は、
衝突しない必要最小の長さまでFence Lengthを増やす。
これは本Ruleが定める衝突回避に当たる。

#### MDK-SF-016 — Code Block Identifier（Code Blockの内容識別子）

**Rule ID:** `MDK-SF-016`

**Rule Name:** Code Block Identifier

**Stability:** Development

**Requirement:** MUST

**Rule:** Fenced Code Blockには、
その内容が何であるかを示す
LanguageまたはContent Identifierを指定する。

特定の言語または形式ではないPlain Textには、
`text` を使用する。

**Reason:** Code Blockの内容は、
その表現だけでは何として読むべきかが確定しない。
識別子が付与されていれば、
読み手はその内容をどの言語・形式として解釈すべきかを
本文の説明に頼らず判断でき、
表示側も内容に応じた提示を行える。
一方、識別子の省略と、
Plain Textであることの明示とを同じ表現に委ねると、
識別子がないCode Blockが、
Plain Textなのか指定漏れなのかを区別できない。
Plain Textへ明示的な値を定めることで、
すべてのCode Blockが内容についての表現を持つ。

**Note:** 本Ruleは、
使用可能な識別子の完全なCatalogを保持しない。
`text` 以外の値は、
その内容が属する言語または形式に従う。

本Ruleは、Code Blockの内容の妥当性を定めない。

#### MDK-SF-017 — Inline Code Representation（Inline Codeの表現）

**Rule ID:** `MDK-SF-017`

**Rule Name:** Inline Code Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** File名、Path、Command、Identifier（識別子）、Literal Value、
Syntax等を、具体的なLiteral Stringとして本文中へ現す場合、
Inline Codeを使用する。

Inline CodeのDelimiterには、
通常はBacktick 1個を使用する。
Content自身がBacktickを含む場合に限り、
衝突しない必要最小の長さまでDelimiter Lengthを増やす。

通常のCanonical Formは次である。

```text
`value`
```

**Reason:** Literal Stringは、
その綴りがそのまま対象を指す。
本文と同じ表現で現すと、
どこからどこまでがその綴りなのかが確定せず、
隣接する助詞・句読点・括弧が
綴りの一部かどうかを読み手が判断できない。
記号を含む文字列では、
Markdownの他の記法として解釈される可能性もある。
Inline Codeで表現することで、
Literal Stringの範囲が確定し、
そのままの表記として読み取れる。
Delimiter Lengthを通常1個へ固定し、
その増加をContentとの衝突に限定するのは、
長さの違いがそれ自体で意味を持つようにするためである。
衝突がないまま長いDelimiterが使われると、
読み手はそれをContentの性質によるものと読む余地を負い、
同じ内容が箇所ごとに異なるDelimiterで書かれることにもなる。

**Note:** 本Ruleは、
Concept（概念）または用語としての一般的な言及へは適用されない。
たとえば、ある概念について述べる場合と、
その概念のIdentifier（識別子）としての綴りを示す場合とでは、
現している対象が異なる。

本Ruleは、
どのLiteral Stringを本文中へ現すかを定めず、
Physical Name（物理名称）およびIdentifier（識別子）そのものの
形式も定めない。
これらは
[Naming Convention](naming.md)
その他の対象を所有するDefinition Authority（定義権限）が所有する。

### Link and Image Representation（LinkおよびImageの表現）

#### MDK-SF-018 — Inline Link Representation（Inline Linkの表現）

**Rule ID:** `MDK-SF-018`

**Rule Name:** Inline Link Representation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Markdown上でLinkを表現する場合、
Inline Link Syntaxを使用すべきである。

Canonical Formは次である。

```text
[Link Text](target)
```

**Reason:** Inline Link Syntaxでは、
Link TextとTargetが同じ位置に現れる。
Reference-style Linkでは、
Targetの定義がLinkの位置から離れた場所に置かれるため、
読み手は参照先を確認するために別の箇所を探すことになり、
Linkの削除や移動の際に定義だけが残っても
その箇所からは気づけない。
Linkの位置でTargetが確認できる形を通常の形とすることで、
Linkとその参照先が同じ箇所で保たれる。

**Note:** 本Ruleは、
Reference-style Linkを禁止しない。
同一のTargetを繰り返し参照する場合のように、
Targetの再利用そのものに理由がある場合、
Reference-style Linkを使用することは本Ruleの想定する例外である。

本Ruleが定めるのはLink SyntaxのSelectionである。
同一Repository内のTargetをどう表現するかは
`MDK-SF-019` が扱う。
Link Textの自然言語としての品質は本Ruleの対象ではなく、
[Writing Convention](writing.md)
が所有する。

#### MDK-SF-019 — Internal Link Representation（Repository内参照の表現）

**Rule ID:** `MDK-SF-019`

**Rule Name:** Internal Link Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** 同一Repository内のMarkdown文書その他のAssetを
Markdown上のLinkとして参照する場合、
参照元のFileからRepository内で解決できる
Relative Referenceを使用する。

**Reason:** 同一Repository内の参照は、
Repositoryが置かれている場所とは独立に成立していなければならない。
Host名やRepositoryの所在を含む参照は、
Clone、Fork、Rename、移動、Offlineでの閲覧のいずれにおいても
参照先が失われるか、
現在のRepositoryではない別の実体を指す。
Relative Referenceであれば、
参照はRepository内部の関係としてのみ成立し、
Repositoryごと移動しても対象を指し続ける。

**Note:** 本Ruleは、
Repository外を指す参照の表現を定めない。

本Ruleは、
参照を設けるかどうか、
どのAssetを参照するかを定めない。
Link Textの自然言語としての品質は本Ruleの対象ではなく、
[Writing Convention](writing.md)
が所有する
Natural Language Representation（自然言語表現）の責務に属する。

File名およびPathの形式は
[Naming Convention](naming.md)
が所有する。

#### MDK-SF-020 — Image Alt Text（画像の代替テキスト）

**Rule ID:** `MDK-SF-020`

**Rule Name:** Image Alt Text

**Stability:** Development

**Requirement:** MUST

**Rule:** Markdown上でImageを表現する場合、
そのImageにAlt Textを持たせる。

**Reason:** Imageの内容は、
画像そのものが表示されて初めて受け取れる。
表示されない環境、読み上げによる利用、
参照先が失われた場合のいずれにおいても、
Alt Textがなければ、
そこに何が置かれていたのかが文書上に残らない。
Alt Textを持たせることで、
Imageが伝えている内容が
画像の表示に依存しない形で文書へ保持される。

**Note:** 本Ruleが要求するのはAlt Textの保持である。
Alt Textの文章としての品質、文体、言語、
および長さは本Ruleが定めない。
Natural Language Representation（自然言語表現）は
[Writing Convention](writing.md)
が所有する。

本Ruleは、
Imageを使用するかどうか、
およびその配置を定めない。

### Source Formatting（Markdown Sourceの記述形式）

#### MDK-SF-021 — Block Spacing（Block間の空行）

**Rule ID:** `MDK-SF-021`

**Rule Name:** Block Spacing

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 独立したMarkdown Block間は、
1行の空行で分離すべきである。

**Reason:** Markdownでは、
Blockの境界が空行の有無によって決まる箇所がある。
空行なしで異なるBlockを連ねると、
意図した区切りが成立せず、
前のBlockの継続として解釈される場合がある。
逆に空行が過剰であれば、
Sourceの見た目上の区切りが実際のBlock構造と対応しなくなる。
分離を1行の空行へそろえることで、
Source上の区切りと解釈されるBlock構造が一致し、
編集時にも境界を保ったまま追記・削除ができる。

**Note:** 本Ruleは、
Heading（見出し）の前後、Listの前後等について
個別のRuleを設けない。
いずれも独立したMarkdown Block間の分離として本Ruleが扱う。

Markdownの構文上、
空行を置かないことが自然である箇所は本Ruleの対象ではない。
List Itemの継続、Table Rowの連続、
Code Block内部の記述はいずれも
独立したBlock間の分離ではない。

#### MDK-SF-022 — Trailing Space（行末の空白）

**Rule ID:** `MDK-SF-022`

**Rule Name:** Trailing Space

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** 行末に空白文字を残してはならない。

Hard Line Breakを表現する目的であっても、
行末の空白をCanonical Formとしない。

**Reason:** 行末の空白は表示されず、
Markdown Sourceを読んでも存在を確認できない。
存在が見えない文字が意味を持つ場合、
その意味は編集の過程で容易に失われ、
逆に意図せず追加された空白が
意味を持つ表現として解釈される。
また、見えない差異はDiffへ現れ、
内容の変更と区別できない差分を生む。
行末の空白を使用しないことで、
Markdown Sourceに現れる表現と、
実際に意味を持つ表現とが一致する。

**Note:** 本Ruleは、
Hard Line Breakという表現自体を禁止しない。
禁止するのは、
行末の空白によってそれを表現することである。

本Ruleは、
行内および行頭の空白、Indent、
Line Length、Hard Wrapを定めない。

#### MDK-SF-023 — Markdown over HTML（HTMLよりMarkdown表現を優先する）

**Rule ID:** `MDK-SF-023`

**Rule Name:** Markdown over HTML

**Stability:** Development

**Requirement:** SHOULD

**Rule:** 同等の内容をMarkdown Representationで表現できる場合は、
HTMLではなくMarkdown Representationを使用すべきである。

**Reason:** 同じ内容に対してMarkdownとHTMLの双方が使用されると、
同一の対象が文書ごと・箇所ごとに異なる表現を持ち、
読み手も編集者も、
まずどちらの記法で書かれているかを確認してからでなければ
内容へ到達できない。
またHTMLは表示環境によって扱いが異なり得るため、
Markdownで表現できる内容をHTMLで表現すると、
表示上の結果まで環境に依存させることになる。
Markdownで表現できる範囲をMarkdownへそろえることで、
表現の選択が内容の違いだけを反映する。

**Note:** 本Ruleは、HTMLの使用を全面的に禁止しない。
Markdown Representationでは表現できない内容について、
HTMLを使用することは本Ruleの対象ではない。

本Ruleは、
使用してよいHTML要素のCatalogを保持しない。
