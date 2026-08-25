# Canonical Japanese Support Convention（正規日本語補助規約）

## Purpose（目的）

本文書は、`noxris42` において
**[Canonical Japanese Support Architecture](../architecture/canonical-japanese-support.md)
上で成立するCanonical Japanese Support Association（正規日本語補助対応）について、
Candidate Recommendation（候補提案）と
Canonical Declaration（正規宣言）を一貫して扱うための
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の3点である。

1. 成立したCanonical Japanese Support Association（正規日本語補助対応）は、
   どこに、どのようなConcrete Representation（具体表現）で
   Canonical Declaration（正規宣言）として保持されるのか。
2. Canonical Japanese Support Association（正規日本語補助対応）の
   Candidate Recommendation（候補提案）は、
   何を優先して行うのか。
3. Candidate Recommendation（候補提案）と
   Canonical Association Establishment（正規対応成立）は、
   どこで分かれるのか。

本文書が定義するのは、この3点に関するRule（規則）に限られる。
本文書は、English Representation（英語表現）そのものの
Identity（同一性）・Meaning（意味）・Formal Status（正式地位）・
Category（分類）、および
Underlying Meaning（対象の意味）を対象としない。
Documentation Presentation（文書上の表示）、
Human Review Workflow（人によるレビュー手順）、
Lifecycle（生存期間）等も対象としない。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Canonical Japanese Support Architecture](../architecture/canonical-japanese-support.md)
- [Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Canonical Japanese Support Architecture（正規日本語補助の意味モデル）
        ▲
        │ refines（Candidate Recommendation（候補提案）と
        │          Canonical Declaration（正規宣言）の規則へ具体化する）
Canonical Japanese Support Convention（本文書）

Convention Architecture（規約の意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（規約記述表記）
        ▲
        │ conforms to（記述表記に従う）
Canonical Japanese Support Convention（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Canonical Japanese Support Association（正規日本語補助対応）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- English Representation（英語表現）が
  本Model（モデル）において対応元として扱われること、および
  そのIdentity（同一性）・Meaning（意味）を
  Canonical Japanese Support（正規日本語補助）が定義しないこと
- Canonical Japanese Support Representation（正規日本語補助表現）の意味
- Canonical Japanese Support Association（正規日本語補助対応）の意味、
  およびその成立
- 同Association（対応）のMultiplicity（多重度）
- Canonical Japanese Support Association（正規日本語補助対応）の成立と
  Documentation Presentation（文書上の表示）との
  Boundary（境界）
- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Definition Authority（定義権限）
- Convention（規約）およびConvention Responsibility（規約責務）
- Normative Rule（規範的ルール）と
  Non-normative Content（非規範的内容）の区別
- Rule Model（ルールモデル）の必須要素・任意要素
- Requirement Level（要求レベル）の語彙とその意味
- Rule Identity（ルール同一性）とその安定性
- Rule ID Format（規約ルールID形式）、
  Rule Field（規則フィールド）の構成・順序・Markdown表現、
  Stability（安定性）のField表現
- Namespace Code（名前空間コード）の割当

### Responsibility Boundary（責務境界）

Canonical Japanese Support（正規日本語補助）に関する
Definition Authority（定義権限）は次のように分離される。
本文書は、上位および隣接する責務を補完しない。

```text
Canonical Japanese Support Association（正規日本語補助対応）の
Semantic Model（意味モデル）・Boundary（境界）
    → Canonical Japanese Support Architecture（正規日本語補助のArchitecture）

English Representation（英語表現）そのもの、および
Underlying Meaning（対象の意味）
    → それぞれの対象を所有する既存のDefinition Authority（定義権限）

Canonical Declaration（正規宣言）の保持と反復規則、および
Candidate Recommendation（候補提案）の規則
    → 本文書

個々のCanonical Japanese Support Association（正規日本語補助対応）の値
    → Central Concrete Declaration Source（中央具体宣言情報源）

Documentation Presentation（文書上の表示）
    → Presentation Rule（表示規則）を所有するConvention（規約）
```

本文書が保持する境界は次である。

```text
Candidate Recommendation（候補提案）
≠ Canonical Association Establishment（正規対応成立）
≠ Documentation Presentation（文書上の表示）
```

Documentation Presentation（文書上の表示）は本文書の責務ではない。
Current Repository（現在のRepository）において
Human-readable Natural Language Representation（人間可読な自然言語表現）を
対象とするのは
[Writing Convention](writing.md)
であり、本文書はそのRule（規則）を前提とせず、
変更・再定義もしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- 成立したCanonical Japanese Support Association（正規日本語補助対応）を
  Central Concrete Declaration Source（中央具体宣言情報源）へ
  Canonical Declaration（正規宣言）として保持すること
- 各Canonical Declaration（正規宣言）が表現する
  Semantic Content（意味内容）
- Canonical Declaration（正規宣言）の
  Concrete Representation（具体表現）
- Candidate Recommendation（候補提案）において
  何を優先して提案するか
- Candidate Recommendation（候補提案）と
  Canonical Association Establishment（正規対応成立）との
  Boundary（境界）

### Out of Scope（本文書が定義しない範囲）

- English Representation（英語表現）のIdentity（同一性）、
  Meaning（意味）、Formal Status（正式地位）、Category（分類）
- English Representation（英語表現）が指す
  Underlying Meaning（対象の意味）
- Presentation Rule（表示規則）、および
  Title（題名）・Heading（見出し）・Body（本文）等における表示条件
- Registration Qualification（登録条件）、
  Occurrence Threshold（出現回数閾値）、
  Candidate Score（候補スコア）
- Candidate Recommendation（候補提案）を行う
  AI-specific Algorithm（AI固有アルゴリズム）
- Human Review Workflow（人によるレビュー手順）、
  Actor Model（主体モデル）、
  Approval / Rejection State（承認／却下状態）、
  Rejected Candidate History（非採用候補履歴）、
  Permanent Exclusion（永久除外）
- Stable Identifier（安定識別子）、
  Alias / Synonym（別名／同義語）
- Lifecycle（生存期間）、Versioning（版管理）
- 本文書が定めるもの以外の
  Additional YAML Field（追加YAMLフィールド）
- 一般的なYAML記述規約、
  およびYAML機能全般に対する禁止／許可Catalog（一覧）
- Validator（検証器）・Linter・CLI・CI等のTool（ツール）要求
- Central Concrete Declaration Source（中央具体宣言情報源）の
  Asset Name（資産名称）・Path（配置）・
  Asset Type（資産種別）に関する一般Rule（一般規則）

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CJS
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace／共有基盤名前空間）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

### Central Concrete Declaration Source（中央具体宣言情報源）

Current Repository（現在のRepository）において
`CJS-SF-001` が要求する
Central Concrete Declaration Source（中央具体宣言情報源）の役割を
担うAsset（資産）は次である。

```text
docs/canonical-japanese-support.yaml
```

本宣言はCurrent Repository（現在のRepository）における
Concrete Source Assignment（具体情報源割当）の値のみを示す。
Central Concrete Declaration Source（中央具体宣言情報源）に関する
Naming Rule（命名規則）・Path Rule（配置規則）・
Asset Type Rule（資産種別規則）等の一般Rule（一般規則）は、
本宣言によって成立しない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的ルール）が
対象を指すために用いる局所的な区別を示す。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。

本節は新たなArchitecture-level Concept（アーキテクチャレベル概念）を
定義しない。

### Central Concrete Declaration Source（中央具体宣言情報源）

Central Concrete Declaration Source（中央具体宣言情報源）は、
成立したCanonical Japanese Support Association（正規日本語補助対応）の
Canonical Declaration（正規宣言）を
Repository内で中央に保持する
Central Location（中央の保持場所）である。

本文書は、この保持場所の
Asset Name（資産名称）およびPath（配置）に関する
一般Rule（一般規則）を定めない。
Current Repository（現在のRepository）において
この役割を担うAsset（資産）の具体値は、
「Concrete Declarations（具体宣言）」が宣言する。

### Canonical Declaration（正規宣言）

Canonical Declaration（正規宣言）は、
Central Concrete Declaration Source（中央具体宣言情報源）において
1つのCanonical Japanese Support Association（正規日本語補助対応）について
記述される保持の単位である。

### Candidate Recommendation（候補提案）

Candidate Recommendation（候補提案）は、
あるEnglish Representation（英語表現）について
Canonical Japanese Support Association（正規日本語補助対応）を
成立させることを提案する行為である。

Candidate Recommendation（候補提案）は
Canonical Association Establishment（正規対応成立）への
Input（入力）であり、
それ自体はCanonical Decision（正規判断）ではない。

## Candidate Recommendation Guidance（候補提案指針）

本節はNon-normative Content（非規範的内容）であり、
`CJS-SF-004` の解釈補助として置かれる。
本節は新たなNormative Requirement（規範要求）を追加せず、
Registration Qualification（登録条件）も定めない。

### 候補になり得るSignal（兆候）

次は、Candidate Recommendation（候補提案）の優先を考える際に
現時点で有用と考えられる観点である。
いずれもRequirement（要求）ではない。

- Concept（概念）・Responsibility（責務）・Role（役割）・
  Relationship（関係）・Principle（原則）等の理解に
  日本語による補助が有用である。
- Document Title（文書題名）およびHeading Label（見出しラベル）等、
  文書の理解上重要な位置で使用されている。
- Japanese Representation（日本語表現）が複数考えられ、
  1つのCanonical Japanese Support Representation（正規日本語補助表現）を
  定めることで表現の揺れを抑えられる。
- 複数のUsage Occurrence（使用箇所）があり、
  一貫した日本語補助の価値が高い。

### Occurrence Count（出現回数）の扱い

Occurrence Count（出現回数）は
Candidate Qualification（候補資格）ではない。

```text
Occurrence Count
≠ Candidate Qualification
```

1回のみ登場するHeading Label（見出しラベル）であっても
候補になり得る。
例として `Design Principles` のような
Heading Label（見出しラベル）が挙げられる。

### Code Block（コードブロック）の扱い

Code Block（コードブロック）内に現れることは、
それだけで候補から除かれることを意味しない。

```text
Code Block placement
≠ automatic exclusion
```

一方、Code（コード）・Identifier（識別子）・Path等として機能する
Literal Representation（そのままの表記）は、
自然言語による理解を補助する対象でない場合、
通常はCandidate Recommendation（候補提案）の優先対象としない。

これはHard Exclusion Rule（厳密な除外規則）ではない。

### 再提案の扱い

過去にCandidate（候補）が採用されなかったことを
Permanent Rejection（永久却下）として扱うMechanism（機構）は、
本文書に存在しない。
同じEnglish Representation（英語表現）について
改めてCandidate Recommendation（候補提案）を行うことは妨げられない。

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Canonical Declaration（正規宣言）

#### CJS-SF-001 — Central Canonical Declaration

**Rule ID:** `CJS-SF-001`

**Rule Name:** Central Canonical Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** [Canonical Japanese Support Architecture](../architecture/canonical-japanese-support.md)
上で成立したCanonical Japanese Support Association（正規日本語補助対応）は、
Repository内の
Central Concrete Declaration Source（中央具体宣言情報源）へ
Canonical Declaration（正規宣言）として保持する。

**Reason:** 成立したCanonical Decision（正規判断）が
中央に保持されていなければ、
どのJapanese Representation（日本語表現）を用いるかを
使用箇所ごとに記述者が改めて判断することになり、
同一のEnglish Representation（英語表現）に対して
異なる日本語補助が併存する。
Canonical Declaration（正規宣言）を1箇所へ集約することで、
すでに成立している決定を検索して再利用でき、
使用箇所ごとの再判断が生じない。

**Note:** 本Rule（ルール）が定めるのは
Canonical Declaration（正規宣言）の保持先である。
Central Concrete Declaration Source（中央具体宣言情報源）の
Asset Name（資産名称）、Path（配置）、
および具体的なAsset Type（資産種別）に関する
一般Rule（一般規則）は、本Rule（ルール）では定めない。
Current Repository（現在のRepository）における
Concrete Source Assignment（具体情報源割当）は
「Concrete Declarations（具体宣言）」が宣言する。
本Rule（ルール）のRequirement（要求）は
その具体値に依存しない。

保持されていることと、
Usage Occurrence（使用箇所）における
Documentation Presentation（文書上の表示）とは別である。
表示は本Rule（ルール）の対象ではない。

#### CJS-SF-002 — Canonical Association Declaration

**Rule ID:** `CJS-SF-002`

**Rule Name:** Canonical Association Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** 各Canonical Declaration（正規宣言）は、
対象となるEnglish Representation（英語表現）と
Canonical Japanese Support Representation（正規日本語補助表現）との
Canonical Japanese Support Association（正規日本語補助対応）を
表現する。

**Reason:** Canonical Declaration（正規宣言）が保持すべき意味は、
Canonical Japanese Support Association（正規日本語補助対応）そのものである。
対応元と対応先のいずれかを欠く宣言は、
どのEnglish Representation（英語表現）に対して
どのJapanese Representation（日本語表現）を
一貫して再利用するのかを確定させず、
中央から検索して再利用するという目的を満たさない。

**Note:** 意味上必要なのは次のAssociation（対応）である。

````text
English Representation
+
Canonical Japanese Support Representation
````

本Rule（ルール）は、これ以外の要素を
Canonical Declaration（正規宣言）へ導入しない。
Stable Identifier（安定識別子）、Category（分類）、
Formal Status（正式地位）、
Presentation Parameter（表示パラメーター）等は含めない。

#### CJS-SF-003 — YAML Scalar Mapping Representation

**Rule ID:** `CJS-SF-003`

**Rule Name:** YAML Scalar Mapping Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Central Concrete Declaration Source（中央具体宣言情報源）は
YAMLで表現する。
各Canonical Declaration（正規宣言）は、
English Representation（英語表現）を
Mapping Key（マッピングキー）とし、
Canonical Japanese Support Representation（正規日本語補助表現）を
Scalar Value（スカラー値）とする
Scalar Mapping（スカラー対応）として表現する。
Mapping Key（マッピングキー）とScalar Value（スカラー値）は、
双方ともDouble-quoted String（ダブルクォート文字列）で表記する。

**Reason:** `CJS-SF-002` が要求するSemantic Content（意味内容）は、
English Representation（英語表現）から
Canonical Japanese Support Representation（正規日本語補助表現）への
単純なAssociation（対応）である。
Scalar Mapping（スカラー対応）は、この意味内容を
余分な構造を挟まずそのまま表す最も直接的な形であり、
English Representation（英語表現）から
対応する値を検索する現在の利用に追加の対応表を要しない。
Double Quote（ダブルクォート）を要求するのは、
Key（キー）とValue（値）を常にString（文字列）として明示し、
YAMLのImplicit Typing（暗黙型解釈）や特殊文字によって
不要な表記判断と揺れが生じることを抑えるためである。

**Note:** Canonical Shape（正規形状）は次である。

````yaml
"Design Principles": "設計原則"
"Design Dependency": "設計依存"
````

Record Mapping（レコード対応）は採用しない。
次の形は本Rule（ルール）に適合しない。

````yaml
"Design Principles":
  japanese: "設計原則"
````

Double Quote（ダブルクォート）の要求は、
空白を含む表記への対処を目的とするものではない。

本Rule（ルール）が定めるのは、
Central Concrete Declaration Source（中央具体宣言情報源）における
Canonical Declaration（正規宣言）の表現に限られる。
一般的なYAML Style Guide（YAML書式規約）は定めない。

### Candidate Recommendation（候補提案）

#### CJS-SF-004 — Candidate Recommendation

**Rule ID:** `CJS-SF-004`

**Rule Name:** Candidate Recommendation

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Candidate Recommendation（候補提案）を行う場合は、
Canonical Japanese Support Representation（正規日本語補助表現）を
定めることが、
そのEnglish Representation（英語表現）の理解補助、または
Repository Documentation（Repository文書）における
Japanese Support Representation（日本語補助表現）の一貫性に対して
意味を持つと合理的に見込まれるものを優先して提案する。

**Reason:** Candidate Recommendation（候補提案）は
Canonical Association Establishment（正規対応成立）への
Input（入力）である。
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

**Note:** 本Rule（ルール）は
Registration Qualification（登録条件）ではない。
本Rule（ルール）が述べるのは提案の優先であり、
Canonical Japanese Support Association（正規日本語補助対応）が
成立し得る対象を限定しない。

本Rule（ルール）は、次のいずれも必要条件としない。

````text
Occurrence Count（出現回数）
Formal Status（正式地位）
専門用語であること
英語難易度
Category（分類）
Title（題名）またはHeading（見出し）であること
````

解釈補助は
「Candidate Recommendation Guidance（候補提案指針）」に示す。
同節はNon-normative Content（非規範的内容）である。

#### CJS-SF-005 — Recommendation Does Not Establish Canonicality

**Rule ID:** `CJS-SF-005`

**Rule Name:** Recommendation Does Not Establish Canonicality

**Stability:** Development

**Requirement:** MUST NOT

**Rule:** Candidate Recommendation（候補提案）が行われたことのみを根拠として、
Canonical Japanese Support Association（正規日本語補助対応）が
成立したものとして扱ってはならない。

**Reason:** Canonical Japanese Support Association（正規日本語補助対応）は、
Repositoryが一貫して再利用すると決定したときに成立する。
提案の存在を成立と同一視すると、
決定されていない対応がCanonical（正規）として
Central Concrete Declaration Source（中央具体宣言情報源）へ入り、
Canonical Declaration（正規宣言）が
成立済みの決定を表さなくなる。
提案と決定を分けることで、
中央に保持される内容が
成立したCanonical Decision（正規判断）に限られる。

**Note:** 本Rule（ルール）が禁じるのは、
Candidate Recommendation（候補提案）のみを根拠として
成立を認めることである。
Human Direct Decision（人による直接判断）から
Canonical Japanese Support Association（正規日本語補助対応）が
成立する経路は妨げない。

本Rule（ルール）は、
Human Review Workflow（人によるレビュー手順）、
具体的なActor（主体）、
Approval / Rejection State（承認／却下状態）を規定しない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- Current Repository（現在のRepository）における
  Central Concrete Declaration Source（中央具体宣言情報源）の
  Concrete Source Assignment（具体情報源割当）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `CJS-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Field（フィールド）を規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

また本文書自身のPhysical Name（物理名称）は、
[Naming Convention](naming.md)
が定めるRule（規則）に従っている。

- File Stem（拡張子を除いた名称部分）は
  英字をすべて小文字で表記し、語をハイフンで区切っている。
- 現在のPath Context（Path上の文脈）において、
  `canonical-japanese-support` はその対象を十分に識別している。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
