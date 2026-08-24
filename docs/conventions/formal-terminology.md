# Formal Terminology Convention（正式用語規約）

## Purpose（目的）

本文書は、`noxris42` において
**[Formal Terminology Architecture](../architecture/formal-terminology.md)
上で成立するFormal Term（正式用語）の
Canonical English Representation（正規英語表現）と
Canonical Japanese Explanation（正規日本語説明）の対応を、
Repository内のFormal Term Registry（正式用語登録簿）へ
一貫して宣言するための
Reusable Normative Standard（再利用可能な規範標準）**
を定義するConvention Asset（規約資産）である。

本文書が扱う問いは次の2点である。

1. Formal Term（正式用語）の
   Canonical Documentation Representation（正規文書表現）は、
   どこに保持されるのか。
2. 個々のFormal Term Declaration（正式用語宣言）は、
   どのようなConcrete Representation（具体表現）で記述されるのか。

本文書が定義するのは、
Canonical Declaration（正規宣言）を
一貫して反復するためのRule（規則）に限られる。
本文書は用語管理一般、
Terminology Governance（用語統治）、
Term Lifecycle（用語ライフサイクル）等を対象としない。

本文書は、上位設計が定義するConcept（概念）を再定義しない。

## Relationships（関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Formal Terminology Architecture](../architecture/formal-terminology.md)
- [Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
- [Convention Architecture](../architecture/convention.md)
- [Convention Authoring Convention](convention-authoring.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Formal Terminology Architecture（正式用語の意味モデル）
        ▲
        │ refines（Canonical Declaration（正規宣言）の反復規則へ具体化する）
Formal Terminology Convention（本文書）

Convention Architecture（規約の意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（規約記述表記）
        ▲
        │ conforms to（記述表記に従う）
Formal Terminology Convention（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Formal Term（正式用語）のCanonical Declaration（正規宣言）へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Formal Term（正式用語）の成立条件
- Formal Term Identity（正式用語同一性）と、
  それがRepresentation（表現）から独立して成立すること
- Formal Term（正式用語）と
  Terminology Referent（用語参照対象）のRelationship（関係）
- Canonical Documentation Representation（正規文書表現）、
  Canonical English Representation（正規英語表現）、
  Canonical Japanese Explanation（正規日本語説明）の意味と
  その非対称な責務
- Canonical Representation Availability（正規表現の利用可能性）と
  Documentation Presentation（文書上の表示）の境界
- Terminology Referent Meaning（用語参照対象の意味）に関する
  Definition Authority Boundary（定義権限境界）
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

Formal Term（正式用語）に関するDefinition Authority（定義権限）は
次のように分離される。
本文書は、上位および隣接する責務を補完しない。

```text
Formal Term（正式用語）の成立条件・Semantic Model（意味モデル）
    → Formal Terminology Architecture（正式用語のArchitecture）

Terminology Referent Meaning（用語参照対象の意味）
    → その対象を所有する既存のDocumentation Asset（文書資産）

Canonical Declaration（正規宣言）の反復規則
    → 本文書

個々のCanonical Pair（正規対応）
    → Formal Term Registry（正式用語登録簿）

Documentation Presentation（文書上の表示）
    → Presentation Rule（表示規則）を所有するConvention（規約）
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

- Formal Term（正式用語）の
  Canonical Documentation Representation（正規文書表現）を
  Formal Term Registry（正式用語登録簿）へ
  Canonical Declaration（正規宣言）として保持すること
- Formal Term Declaration（正式用語宣言）の
  Concrete Representation（具体表現）
- Canonical English Representation（正規英語表現）の
  Entry Key（エントリキー）としての使用
- Canonical Japanese Explanation（正規日本語説明）の
  Field（フィールド）としての保持

### Out of Scope（本文書が定義しない範囲）

- Formal Term（正式用語）の成立条件、および
  Formal Term Identity（正式用語同一性）のSemantic Model（意味モデル）
- Formal Term Identity（正式用語同一性）を表現する
  Concrete Identifier（具体識別子）、
  Stable Identifier（安定識別子）、Stable ID Format（安定ID形式）
- Terminology Referent Reference（用語参照対象参照）、および
  Terminology Referent Meaning（用語参照対象の意味）
- Usage Occurrence（使用箇所）に関する要求
- Presentation Policy（表示方針）、
  Presentation Configuration（表示設定）、
  およびDocumentation Presentation（文書上の表示）一般
- 登録・Review（確認）・検証を行う作業タイミング、
  およびWorkflow（作業手順）
- Canonical Value（正規値）変更後のRepository更新Workflow（作業手順）
- Alias / Synonym（別名／同義語）
- Term Lifecycle（用語ライフサイクル）、Versioning（版管理）、
  Deprecation（廃止）
- Formal Term Registry（正式用語登録簿）の
  Physical Name（物理名称）およびPhysical Location（物理配置）
- Localization（多言語化）の一般Model（一般モデル）
- YAML機能全般に対する禁止／許可Catalog（一覧）、
  および一般的なYAML記述規約
- Validator / Linter / CLI / CI等のTool（ツール）要求

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: FTM
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace／共有基盤名前空間）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Reading Aid（読解のための補足）

本節は、以降のNormative Rule（規範的ルール）が
対象を指すために用いる局所的な区別を示す。
本節はNon-normative Content（非規範的内容）であり、
Normative Meaning（規範的意味）を保持しない。

### Formal Term Registry（正式用語登録簿）

Formal Term Registry（正式用語登録簿）は、
Formal Term（正式用語）の
Canonical Declaration（正規宣言）を
Repository内で中央に保持するCentral Location（中央の保持場所）である。

Formal Term Registry（正式用語登録簿）が保持するのは
Canonical Terminology Data（正規用語データ）であり、
Presentation Policy（表示方針）ではない。

### Formal Term Declaration（正式用語宣言）

Formal Term Declaration（正式用語宣言）は、
Formal Term Registry（正式用語登録簿）において
1つのFormal Term（正式用語）について記述される
Canonical Declaration（正規宣言）の単位である。

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Canonical Declaration（正規宣言）

#### FTM-SF-001 — Central Canonical Declaration

**Rule ID:** `FTM-SF-001`

**Rule Name:** Central Canonical Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** [Formal Terminology Architecture](../architecture/formal-terminology.md)
上で成立するFormal Term（正式用語）の
Canonical Documentation Representation（正規文書表現）は、
Formal Term Registry（正式用語登録簿）へ
Canonical Declaration（正規宣言）として保持する。

**Reason:** Canonical Japanese Explanation（正規日本語説明）が
中央に保持されていなければ、
その説明は使用箇所ごとに記述者が改めて判断することになり、
同一のFormal Term（正式用語）に対して
異なる説明が併存する。
Canonical Declaration（正規宣言）を1箇所へ集約することで、
すでに成立している決定を検索して再利用でき、
説明の揺れが生じない。

**Note:** 本Rule（ルール）が定めるのは
Canonical Declaration（正規宣言）の保持場所である。
登録・確認を行う作業タイミング、Workflow（作業手順）、
およびUsage Occurrence（使用箇所）における
Documentation Presentation（文書上の表示）は
本Rule（ルール）の対象ではない。

#### FTM-SF-002 — Canonical Term Declaration

**Rule ID:** `FTM-SF-002`

**Rule Name:** Canonical Term Declaration

**Stability:** Development

**Requirement:** MUST

**Rule:** Formal Term Registry（正式用語登録簿）の
各Formal Term Declaration（正式用語宣言）は、
Canonical English Representation（正規英語表現）を
Entry Key（エントリキー）とし、
Canonical Japanese Explanation（正規日本語説明）を
`japanese` Field（フィールド）とする
YAML Record（YAML記録）として表現する。

**Reason:** Canonical Declaration（正規宣言）の
Current Primary Use Case（現在の主要利用例）は、
文書中で使用しているCanonical English Representation（正規英語表現）から
対応するCanonical Japanese Explanation（正規日本語説明）を
直接検索して取得することである。
英語表現をそのままEntry Key（エントリキー）とすれば、
この検索が追加の対応表を経ずに成立する。
現在必要性のない別のIdentifier（識別子）を導入しないのは、
それが宣言時と参照時の双方へ、
値の対応を維持するための作業を新たに生じさせるためである。

**Note:** 記述例は次である。

````text
"Design Dependency":
  japanese: "設計依存"

"Single Work Subject":
  japanese: "単一作業主体"
````

Entry Key（エントリキー）は
Registry Lookup Key（登録簿検索キー）であり、
Formal Term Identity（正式用語同一性）そのものではない。

````text
Entry Key
≠ Formal Term Identity
````

同一のCanonical English Representation（正規英語表現）で
複数のFormal Term Identity（正式用語同一性）を区別する
Concrete Need（具体的必要性）は現時点で確認されていない。
本Rule（ルール）は、この点について
Architecture-level Uniqueness Rule（アーキテクチャレベルの一意性規則）を
成立させない。

本Rule（ルール）が定めるのは、
現在必要なEntry Key（エントリキー）と
`japanese` Field（フィールド）に限られる。
Stable Identifier（安定識別子）、
Terminology Referent Reference（用語参照対象参照）、
Presentation Parameter（表示パラメーター）等は導入しない。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `FTM-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
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
  `formal-terminology` はその対象を十分に識別している。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
