# Formal Terminology Architecture（正式用語のArchitecture）

## Purpose（目的）

本文書は、`noxris42` において
**Repository Documentation（Repository文書）で
既存の意味上の対象を安定して識別・参照するために
正式に選択されるFormal Term（正式用語）** について、
そのIdentity（同一性）、参照対象とのRelationship（関係）、
Canonical Documentation Representation（正規文書表現）、および
参照対象のMeaning（意味）との
Definition Authority Boundary（定義権限境界）を定義する
Architecture Asset（アーキテクチャ資産）である。

本文書が扱う問いは次の5点である。

1. Formal Term（正式用語）は、何によって成立するのか。
2. Formal Term（正式用語）は、何を識別・参照するのか。
3. Formal Term（正式用語）は、
   Repository Documentation（Repository文書）上で
   どのように表現されるのか。
4. Formal Term（正式用語）が
   Canonical Documentation Representation（正規文書表現）を
   保持していることと、
   それがConcrete Usage Occurrence（具体使用箇所）で
   表示されることは、どこで分かれるのか。
5. Formal Term（正式用語）に関する
   Definition Responsibility（定義責務）は、
   参照対象を所有する既存の
   Definition Authority（定義権限）とどこで分かれるのか。

本文書が定義するのは、
Formal Term（正式用語）を成立させる
Semantic Model（意味モデル）である。
個々のTerminology Referent Meaning（用語参照対象の意味）、
すなわちFormal Term（正式用語）が参照する対象そのものの意味は、
本文書が定義しない。

## Position（上位設計との関係）

本文書は、次を上位Source（上位の情報源）として参照する。

- [Documentation Structure Architecture](documentation-structure.md)
- [Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)

Design Dependency（設計依存）は次の一方向とする。

```text
Documentation Structure Architecture（文書構造の一般意味モデル）
        ▲
        │ presupposes（前提として使用する）
Formal Terminology Architecture（本文書）

Repository Governance Documentation Framework Architecture
（文書体系と領域責務）
        ▲
        │ belongs to（Architecture Areaに属する）
Formal Terminology Architecture（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)
が定義するArchitecture Area（アーキテクチャ領域）に属する
通常のDocumentation Asset（文書資産）である。
同Area（領域）のArea Responsibility（領域責務）である
Semantic / Structural Model（意味・構造モデル）の定義として、
本文書はFormal Term（正式用語）を成立させる
Concept（概念）・Responsibility（責務）・
Relationship（関係）・Boundary（境界）を定義する。
Area（領域）を代表・集約するAsset（資産）ではない。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

- Documentation Asset（文書資産）と
  Document Responsibility（文書責務）
- Definition Authority（定義権限）と、
  それがDefinition（定義）を担う
  Document Responsibility（文書責務）の場合に成立すること
- Documentation Framework（文書体系）・
  Documentation Area（文書責務領域）と
  Area Responsibility（領域責務）
- Logical Identity（論理的同一性）を
  Physical Location（物理配置）から導出しないこと、および
  Logical / Representation Boundary（論理／表現境界）
- 本Framework（体系）のArea Composition（領域構成）、および
  Area（領域）帰属の判定基準
- Local Design Principle（局所設計原則）と
  Fundamental Principle（根本原則）の区別

### Documentation Structure Architectureとの関係

[Documentation Structure Architecture](documentation-structure.md)
（文書構造のArchitecture）は、
Documentation Asset（文書資産）・
Document Responsibility（文書責務）・
Definition Authority（定義権限）の
一般Semantic Model（一般意味モデル）を所有する。

同Architectureは、
Formal Term（正式用語）に固有の
Concept Model（概念モデル）を所有しない。
本文書は、同Architectureが定義する一般Model（一般モデル）を
前提として使用し、
その上でFormal Term（正式用語）に固有の
Concept（概念）と関係を定義する。

### Repository Governance Documentation Framework Architectureとの関係

[Repository Governance Documentation Framework Architecture](repository-governance-documentation-framework.md)
（Repository統治文書体系のArchitecture）は、
Architecture Area（アーキテクチャ領域）が
Semantic / Structural Model（意味・構造モデル）を所有することを定義する。

本文書はそのArchitecture Area（アーキテクチャ領域）に属する
Documentation Asset（文書資産）として、
Formal Term（正式用語）のSemantic Model（意味モデル）を定義する。
本文書は、同Architectureが定義する
Area Composition（領域構成）・
Area Responsibility（領域責務）・
Area（領域）帰属の判定基準を再定義しない。

### Repository Governance Architectureとの関係

[Repository Governance Architecture](repository-governance.md)
（Repository間の統治・責務Architecture）は、
Repository間のOwnership（所有責任）および
Shared Development Foundation（複数Repositoryで共有する開発基盤）を所有する。

同Architectureは、
本文書が定義するFormal Terminology（正式用語）の
内部Semantic Model（内部意味モデル）を所有しない。
本文書も、同Architectureが定義する
Ownership（所有責任）・Shared Scope（共有範囲）・
Foundation Application（共通開発基盤を対象Repositoryへ適用する関係）を
再定義・上書きしない。

### Convention Architectureとの関係

[Convention Architecture](convention.md)
（規約のArchitecture）は、
Convention（規約）およびNormative Rule（規範的ルール）の
内部意味構造を所有する。

同Architectureは、
Formal Term（正式用語）の
一般Semantic Model（一般意味モデル）を所有しない。
本文書も、Convention（規約）・
Normative Rule（規範的ルール）・
Requirement Level（要求レベル）・
Rule Identity（ルール同一性）を再定義しない。

本文書はNormative Rule（規範的ルール）を定義しない。
本文書が定義するのはSemantic Model（意味モデル）であり、
Reusable Normative Standard（再利用可能な規範標準）ではない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Terminology Referent（用語参照対象）の意味と、
  それがRole（役割）として成立すること
- Formal Term（正式用語）の意味と成立条件
- Formal Term Identity（正式用語同一性）の意味と、
  Natural Language Representation（自然言語表現）からの独立
- Formal Term（正式用語）と
  Terminology Referent（用語参照対象）の
  Relationship（関係）、および現在必要なMultiplicity（多重度）
- Canonical Documentation Representation（正規文書表現）の意味と、
  現在必要なその構成要素
- Canonical English Representation（正規英語表現）と
  Canonical Japanese Explanation（正規日本語説明）の
  非対称な責務の区別
- Canonical Japanese Explanation（正規日本語説明）が
  Current Formal Term Model（現在の正式用語モデル）の
  必要構成要素として成立すること
- Canonical Representation Availability
  （Canonical Representation（正規表現）がFormal Term（正式用語）に属し
  利用可能であること）と、
  Documentation Presentation（文書上の表示）との
  Semantic Boundary（意味上の境界）
- Presentation Requirement（表示要求）が
  Concrete Usage Context（具体使用文脈）に応じて
  異なり得るという境界
- Canonical Japanese Explanation（正規日本語説明）が
  存在しない状態と、存在するが表示されない状態との区別
- Terminology Referent Meaning（用語参照対象の意味）と、
  Formal Terminology（正式用語）側の
  Definition Responsibility（定義責務）との
  Definition Authority Boundary（定義権限境界）
- Formal Term（正式用語）と、
  Formal Name（正式名称）・Concept Name（概念名称）・
  Role Name（役割名称）との境界

### Out of Scope（本文書が定義しない範囲）

- 個々のTerminology Referent Meaning（用語参照対象の意味）、
  すなわちFormal Term（正式用語）が参照する対象そのものの意味
- Terminology Referent（用語参照対象）のSubtype（下位型）、
  およびTerm Taxonomy（用語分類体系）
- 現在のRepository Documentation（Repository文書）で使用されている
  用語のうち、どれがFormal Term（正式用語）として成立するかの
  Catalog（一覧）
- Formal Term Registry（正式用語登録簿）、
  Glossary（用語集）等の用語管理機構
- Concrete Identifier（具体識別子）、
  Stable ID Format（安定ID形式）
- Alias / Synonym（別名／同義語）、および
  Terminology Referent（用語参照対象）側から見た
  Multiplicity（多重度）
- Term Lifecycle（用語ライフサイクル）、
  Versioning（版管理）、Deprecation（廃止）
- Canonical Documentation Representation（正規文書表現）の
  具体的な表記形式
- Presentation Requirement（表示要求）、すなわち
  どのUsage Context（使用文脈）で、
  どのCanonical Representation Element（正規表現要素）を、
  どの頻度で表示するか
- Presentation Context（表示文脈）の
  Closed Taxonomy（閉じた分類体系）
- Canonical Japanese Explanation（正規日本語説明）が
  表示されないことが許容される条件
- 表示・非表示のConcrete State Representation（具体状態表現）
- Configuration（設定）のModel（モデル）
- Generic Presentation Architecture（汎用表示アーキテクチャ）
- Generic Language Map（汎用言語対応表）、
  Localization Model（多言語化モデル）
- Formal Term（正式用語）に関する
  Normative Rule（規範的ルール）およびConvention（規約）
- Metadata（構造化メタデータ）および
  Declaration（明示的宣言）のSchema
- Validation（検証）・Lint等のTool（ツール）要求

詳細は「Non-goals / Delegation（今回扱わず後続へ委譲する事項）」に示す。

## Concept Model（概念モデル）

### Model全体像

本文書が定義するConcept（概念）とその関係は次である。

```text
Existing Meaning-bearing Subject
（既存の意味を持つ対象）
        │
        │ plays the role of（役割を果たす）
        ▼
Terminology Referent（用語参照対象）
        ▲
        │ identifies（識別・参照する）
        │
Formal Term（正式用語）
        │
        ├─ Formal Term Identity（正式用語同一性）
        │
        └─ has（保持する）
           ↓
           Canonical Documentation Representation
           （正規文書表現）
                ├─ Canonical English Representation
                │  （正規英語表現）
                └─ Canonical Japanese Explanation
                   （正規日本語説明）
                        │
                        │ available for presentation
                        │ （表示のために利用可能である）
                        ▼
                   Documentation Presentation
                   （文書上の表示）
                        │
                        └─ governed by downstream normative rules
                           （下位の規範的ルールが決定する）
```

このModel（モデル）が成立させる中心的な境界は次である。

```text
Referent Meaning（参照対象の意味）
≠ Formal Term Identity（正式用語同一性）
≠ Canonical Documentation Representation（正規文書表現）
```

```text
Formal Term（正式用語）
≠ English String（英語文字列）
≠ Japanese Explanation（日本語説明）
```

```text
Canonical Representation Availability
（Canonical Representation（正規表現）がFormal Term（正式用語）に属し
利用可能であること）
≠
Documentation Presentation
（Concrete Usage Occurrence（具体使用箇所）で表示されること）
```

### Terminology Referent（用語参照対象）

Terminology Referent（用語参照対象）は、
Formal Term（正式用語）によって識別・参照される
既存の意味上の対象が、
Formal Terminology（正式用語）のRelationship（関係）の中で果たす
Role（役割）である。

既存の意味上の対象が、
Formal Term（正式用語）による識別・参照の相手となるとき、
その対象はTerminology Referent（用語参照対象）としての
Role（役割）を果たす。
Terminology Referent（用語参照対象）は、
このRelationship（関係）の中で成立する。

その対象そのものの意味、すなわち
Terminology Referent Meaning（用語参照対象の意味）の
Definition Authority（定義権限）は、
その対象を所有する既存の
Documentation Asset（文書資産）にある。
本文書はそれを複製・再定義しない。

本文書は、Terminology Referent（用語参照対象）を
新しいUniversal Entity Type（汎用実体種別）として一般化しない。
すなわち、Repository上のあらゆる対象を
Terminology Referent（用語参照対象）として分類する
Entity Model（実体モデル）を導入しない。

本文書は、Terminology Referent（用語参照対象）の
Subtype（下位型）を定義しない。
Concept（概念）・Responsibility（責務）・Role（役割）・
Principle（原則）・Rule-related Concept（規則関連概念）等は、
Terminology Referent（用語参照対象）としての
Role（役割）を果たし得るが、
本文書はそれらをSubtype（下位型）として区別しない。

### Formal Term（正式用語）

Formal Term（正式用語）は、
Repository Documentation（Repository文書）において、
特定のTerminology Referent（用語参照対象）を
一貫して識別・参照するために正式に選択された
Terminology Unit（用語単位）である。

Formal Term（正式用語）が成立するのは、
次の3つがすべて満たされる場合である。

1. 特定のTerminology Referent（用語参照対象）が存在する。
2. Repository Documentation（Repository文書）上で
   その対象を安定して識別・参照する役割を持つ。
3. その用途のFormal Term（正式用語）として正式に選択されている。

この3つは、Formal Term（正式用語）が成立するための
Positive Condition（正の条件）である。
次の性質は、それだけでは
Formal Term（正式用語）を成立させない。

- Repository Documentation（Repository文書）上で頻出すること
- 英語で表記されていること
- 一般に通用するTechnical Term（技術用語）であること

Repository固有の識別を担わず、
一般に通用する意味で使用される
Ordinary Technical Term（一般技術用語）は、
Formal Term（正式用語）の成立条件を満たさない。
本文書は、そうした用語を
Architecture Concept（アーキテクチャ概念）として新規に定義しない。

### Formal Term Identity（正式用語同一性）

Formal Term Identity（正式用語同一性）は、
あるFormal Term（正式用語）を、
その具体的なNatural Language Representation（自然言語表現）から
独立して、同一のTerminology Unit（用語単位）として識別する
Logical Identity（論理的同一性）である。

Formal Term Identity（正式用語同一性）は、
Representation（表現）から独立して成立する。

```text
Formal Term Identity（正式用語同一性）
≠ Canonical English Representation（正規英語表現）
≠ Canonical Japanese Explanation（正規日本語説明）
```

この独立から、次が成立する。

- Representation（表現）が変更されたことだけを根拠として、
  Formal Term Identity（正式用語同一性）が変更されたと導出しない。
- 同一のCharacter String（文字列）であっても、
  異なるTerminology Referent（用語参照対象）を識別する場合、
  文字列の一致だけを根拠として
  Formal Term Identity（正式用語同一性）の一致を導出しない。

本文書は、Formal Term Identity（正式用語同一性）を
表現するためのConcrete Identifier（具体識別子）または
Stable ID Format（安定ID形式）を定義しない。
現時点では、Identity（同一性）が
Representation（表現）から独立して成立するという
Semantic Model（意味モデル）で足りる。

### Formal Term（正式用語）とTerminology Referent（用語参照対象）の関係

Formal Term（正式用語）と
Terminology Referent（用語参照対象）の
Relationship（関係）は次である。

```text
Formal Term（正式用語）
    ── identifies（識別・参照する）──▶
Terminology Referent（用語参照対象）
```

現在必要なMultiplicity（多重度）として、
本文書は次を定義する。

```text
1 Formal Term（正式用語）
    → 1 Terminology Referent（用語参照対象）
```

すなわち、1つのFormal Term（正式用語）は、
1つのTerminology Referent（用語参照対象）を識別・参照する。

本文書は、Terminology Referent（用語参照対象）側から見た
Multiplicity（多重度）を定義しない。
1つのTerminology Referent（用語参照対象）に対して
複数のFormal Term（正式用語）が成立し得るかは、
本文書では確定しない。
Alias / Synonym（別名／同義語）も、
本文書のConcept（概念）として導入しない。

### Canonical Documentation Representation（正規文書表現）

Canonical Documentation Representation（正規文書表現）は、
Formal Term Identity（正式用語同一性）を
Repository Documentation（Repository文書）上で
一貫して表現する正規の
Natural Language Representation（自然言語表現）である。

Canonical Documentation Representation（正規文書表現）は
Representation（表現）として成立する。
Formal Term Identity（正式用語同一性）そのものでも、
Terminology Referent Meaning（用語参照対象の意味）でもない。

Formal Term（正式用語）は、
Canonical Documentation Representation（正規文書表現）を保持する。
保持されるのは、
Repository Documentation（Repository文書）上で
一貫した表現を成立させるために利用可能な
Canonical Representation Elements（正規表現要素）である。
Concrete Usage Occurrence（具体使用箇所）へ
そのまま表示される完成文字列ではない。

本文書が現在扱うのは、
次の2つの非対称な要素のみである。

```text
Canonical Documentation Representation（正規文書表現）
├─ Canonical English Representation（正規英語表現）
└─ Canonical Japanese Explanation（正規日本語説明）
```

この2つは対等な言語対ではない。
それぞれが担う責務が異なる。

本文書は、
Generic Language Map（汎用言語対応表）または
Localization Model（多言語化モデル）を導入しない。
現在扱うのは、この非対称な2要素に限られる。

#### Canonical English Representation（正規英語表現）

Canonical English Representation（正規英語表現）は、
Formal Term Identity（正式用語同一性）を
Repository Documentation（Repository文書）上で
英語によって表現するCanonical Representation（正規表現）である。

#### Canonical Japanese Explanation（正規日本語説明）

Canonical Japanese Explanation（正規日本語説明）は、
Canonical English Representation（正規英語表現）に伴って
Formal Term（正式用語）の理解を日本語で補助する
Canonical Explanation（正規説明）である。

Canonical Japanese Explanation（正規日本語説明）が担うのは
理解の補助である。
次のいずれでもない。

```text
Canonical Japanese Explanation（正規日本語説明）
≠ Japanese Formal Term（日本語の正式用語）
≠ Referent Definition（参照対象の定義）
```

すなわち、Canonical Japanese Explanation（正規日本語説明）は、
Formal Term Identity（正式用語同一性）を
単独で表現するCanonical Representation（正規表現）ではなく、
Terminology Referent Meaning（用語参照対象の意味）を
確定させるDefinition（定義）でもない。

Canonical Japanese Explanation（正規日本語説明）は、
Current Formal Term Model（現在の正式用語モデル）において、
各Formal Term（正式用語）が保持する必要構成要素である。

この必要性が成立する根拠は、
Formal Terminology（正式用語）の現在の
Semantic Need（意味上の必要性）にある。
Formal Term（正式用語）を補助する日本語説明が
箇所ごとに揺れると、
同じFormal Term（正式用語）であってもConcept（概念）の範囲が
異なって理解される。
Canonical Explanation（正規説明）を
Formal Term（正式用語）側に成立させることで、
その日本語説明のSemantic Drift（意味上の揺れ）を防ぐ。

この必要性は、
下位Convention（規約）が現在定めている
Normative Rule（規範的ルール）から逆に導出したものではない。
Rule（規則）の有無とは独立に、
本Model（モデル）の構成要素として成立する。

#### Representation Availability（正規表現の利用可能性）とDocumentation Presentation（文書上の表示）

Documentation Presentation（文書上の表示）は、
Canonical Representation Element（正規表現要素）が
Concrete Usage Occurrence（具体使用箇所）へ
実際に現れることである。

本文書は、次を境界として成立させる。

```text
Canonical Representation Availability
（Canonical Representation（正規表現）がFormal Term（正式用語）に属し
利用可能であること）
≠
Documentation Presentation
（Concrete Usage Occurrence（具体使用箇所）で表示されること）
```

すなわち、あるFormal Term（正式用語）が
Canonical Representation Element（正規表現要素）を保持していることは、
その要素がすべてのUsage Occurrence（使用箇所）へ
表示されることを意味しない。
逆に、ある使用箇所へ表示されていないことは、
その要素がFormal Term（正式用語）に属していないことを意味しない。

Presentation Requirement（表示要求）は、
Concrete Usage Context（具体使用文脈）に応じて
異なり得る。
本文書が保持するのは、この境界のみである。

本文書は、Presentation Context（表示文脈）の
Closed Taxonomy（閉じた分類体系）を導入しない。
Document Title（文書題名）・Heading Label（見出しラベル）・
Natural Language Prose（自然言語本文）等を、
Architecture-level Closed Set（アーキテクチャレベル閉集合）として
定義しない。

本文書は、Documentation Presentation（文書上の表示）を
Formal Terminology（正式用語）以外の対象へ適用する
Generic Presentation Architecture（汎用表示アーキテクチャ）へ
一般化しない。

#### Canonical Japanese Explanation（正規日本語説明）の不在と非表示

本文書は、次の2つの状態を区別する。

```text
Canonical Japanese Explanation does not exist
（Canonical Japanese Explanation（正規日本語説明）が存在しない）
≠
Canonical Japanese Explanation exists but is not presented
（Canonical Japanese Explanation（正規日本語説明）は存在するが
表示されていない）
```

Canonical Japanese Explanation（正規日本語説明）は
Current Formal Term Model（現在の正式用語モデル）の
必要構成要素であるため、
それが存在しない状態は、
そのFormal Term（正式用語）が
本Model（モデル）を満たしていない状態である。
本文書は、この状態を
正式なExplicit Omission State（明示的非併記状態）として導入しない。

Canonical Japanese Explanation（正規日本語説明）が存在し、
特定のUsage Occurrence（使用箇所）で表示されていない状態は、
本Model（モデル）の上で区別可能な状態である。
その非表示が許容されるかどうかは、
適用されるPresentation Rule（表示規則）が決定する。
本文書はその可否を定めない。

本文書は、これらの状態を表す
`none` ・ `omit` ・ Boolean Flag（真偽値フラグ）等の
Concrete State Representation（具体状態表現）を設計しない。

### Formal Term（正式用語）とName（名称）の境界

本文書は、次の境界を保持する。

```text
Formal Term（正式用語） ≠ Formal Name（正式名称）
Formal Term（正式用語） ≠ Concept Name（概念名称）
Formal Term（正式用語） ≠ Role Name（役割名称）
```

これらのName（名称）は、
Formal Term（正式用語）の成立条件を満たす場合に、
Formal Term（正式用語）として本Model（モデル）の対象になり得る。
本文書が保持するのは、この境界のみである。

本文書は、これらのName（名称）を
Formal Term（正式用語）のSubtype（下位型）として定義せず、
Term Taxonomy（用語分類体系）も定義しない。

## Definition Authority Boundary（定義権限境界）

Definition Authority Boundary（定義権限境界）は、
Terminology Referent Meaning（用語参照対象の意味）と、
Formal Terminology（正式用語）側の
Definition Responsibility（定義責務）とを分ける境界である。

```text
Terminology Referent Meaning（用語参照対象の意味）
        ↓
その対象を所有する既存のDefinition Authority（定義権限）

Formal Term Identity（正式用語同一性）
Formal Term（正式用語）とTerminology Referent（用語参照対象）の
Relationship（関係）
Canonical Documentation Representation（正規文書表現）
        ↓
Formal Terminology（正式用語）側の
Definition Responsibility（定義責務）
```

Formal Terminology（正式用語）側が
Definition Responsibility（定義責務）を持つのは、
次の4つのみである。

- Formal Term Identity（正式用語同一性）
- Formal Term（正式用語）と
  Terminology Referent（用語参照対象）の
  Relationship（関係）
- Canonical English Representation（正規英語表現）
- Canonical Japanese Explanation（正規日本語説明）

Terminology Referent Meaning（用語参照対象の意味）の
Definition Authority（定義権限）は、
その対象を所有する既存の
Documentation Asset（文書資産）にある。
Formal Terminology（正式用語）は、
その意味を複製・再定義・上書きしない。

したがって、あるFormal Term（正式用語）が
Canonical Japanese Explanation（正規日本語説明）を伴っていることは、
その説明が
Terminology Referent Meaning（用語参照対象の意味）を
確定させていることを意味しない。
意味の確定は、常に参照対象を所有する
Definition Authority（定義権限）側にある。

本文書は、`Source of Truth` を
新しいArchitecture Concept（アーキテクチャ概念）として導入しない。
Definition Authority（定義権限）は
[Documentation Structure Architecture](documentation-structure.md)
が所有するConcept（概念）であり、
本文書は同じ責務を別のConcept（概念）として再導入しない。

## Design Principles（設計原則）

本節が示すのは、本文書が定義する
Semantic Model（意味モデル）の内部で成立する
Local Design Principle（局所設計原則）である。
Philosophy Area（思想領域）が所有する
Fundamental Principle（根本原則）ではない。

### 1. Identity and Representation Separation（同一性と表現の分離）

Formal Term Identity（正式用語同一性）は、
Canonical Documentation Representation（正規文書表現）から
独立して成立させる。
Representation（表現）の一致・不一致だけを根拠として
Identity（同一性）の一致・不一致を導出しない。

### 2. Referent Authority Preservation（参照対象の定義権限維持）

Terminology Referent Meaning（用語参照対象の意味）の
Definition Authority（定義権限）は、
その対象を所有する既存の
Documentation Asset（文書資産）に留める。
Formal Terminology（正式用語）が担うのは、
識別・参照と表現に関する
Definition Responsibility（定義責務）である。

### 3. Positive Formality Condition（正式用語の正条件による成立）

Formal Term（正式用語）の成立は、
満たされるべきPositive Condition（正の条件）によって判定する。
頻度・言語・用語の一般性といった
付随的な性質からは導出しない。

### 4. Current Representation Need Only（現在必要な表現だけを定義する）

Canonical Documentation Representation（正規文書表現）として
定義するのは、
現在Semantic Need（意味上の必要性）が確認された要素に限る。
将来の必要性を見込んで、
一般化されたLanguage Model（言語モデル）または
Representation Model（表現モデル）を先行して導入しない。

### 5. Concrete Mechanism Independence（具体機構からの独立）

本Model（モデル）は、
Registry（登録簿）・Identifier Format（識別子形式）・
Schema・Tool（ツール）等の具体機構から独立して成立させる。
具体機構は、必要性が確認された時点で、
本Model（モデル）を前提とする後続設計が定める。

### 6. Availability over Presentation（保持と表示を分離する）

Canonical Representation Element（正規表現要素）が
Formal Term（正式用語）に属し利用可能であることと、
それがConcrete Usage Occurrence（具体使用箇所）で表示されることを
分離して扱う。
表示の有無だけを根拠として、
その要素がFormal Term（正式用語）に属するかどうかを導出しない。
表示の可否を決めるのは、
本Model（モデル）を前提とする
Presentation Rule（表示規則）である。

## Non-goals / Delegation（今回扱わず後続へ委譲する事項）

本文書は次を定義しない。これらは後続設計へ委譲する。

### 管理機構に関する事項

- Formal Term Registry（正式用語登録簿）、
  Glossary（用語集）等の用語管理機構
- 現在のRepository Documentation（Repository文書）で使用されている
  用語のうち、どれがFormal Term（正式用語）として成立するかの
  Catalog（一覧）
- Formal Term（正式用語）の
  Term Lifecycle（用語ライフサイクル）、
  Versioning（版管理）、Deprecation（廃止）

### Identity（同一性）に関する事項

- Concrete Identifier（具体識別子）および
  Stable ID Format（安定ID形式）
- Alias / Synonym（別名／同義語）
- Terminology Referent（用語参照対象）側から見た
  Multiplicity（多重度）

### Representation（表現）に関する事項

- Canonical Documentation Representation（正規文書表現）の
  具体的な表記形式
- Generic Language Map（汎用言語対応表）、
  Localization Model（多言語化モデル）

### Presentation（表示）に関する事項

本文書が所有するのは、次までである。

- Canonical Representation（正規表現）が何であるか
- Formal Term（正式用語）が
  Canonical Representation（正規表現）を保持すること
- Canonical Representation Availability（正規表現の利用可能性）と
  Documentation Presentation（文書上の表示）が別であること

次は所有しない。

- どのUsage Context（使用文脈）で表示するか
- どのCanonical Representation Element（正規表現要素）を表示するか
- 初出箇所のみ表示するか、常に表示するか
- Document Title（文書題名）・Heading Label（見出しラベル）・
  Natural Language Prose（自然言語本文）等で
  どのように表示するか
- Presentation Context（表示文脈）の
  Closed Taxonomy（閉じた分類体系）
- Canonical Japanese Explanation（正規日本語説明）が
  表示されないことが許容される条件、および
  その状態のConcrete State Representation（具体状態表現）
- Configuration（設定）のModel（モデル）
- Documentation Presentation（文書上の表示）を
  Formal Terminology（正式用語）以外へ適用する
  Generic Presentation Architecture（汎用表示アーキテクチャ）

これらのPresentation Requirement（表示要求）は、
Human-readable Natural Language Representation（人間可読な自然言語表現）を
対象とする下位Convention（規約）の責務とする。

現在必要なSemantic Need（意味上の必要性）は、次の分担で解決する。
Configuration（設定）を
Architecture Concept（アーキテクチャ概念）として導入しない。

```text
Architecture
    → Canonical Representation Availability（正規表現の利用可能性）と
      Documentation Presentation（文書上の表示）を分離する

Convention
    → Presentation Rule（表示規則）を定義する
```

### Normative Standard（規範標準）に関する事項

- Formal Term（正式用語）に関する
  Normative Rule（規範的ルール）およびConvention（規約）
- 現在のRepository Documentation（Repository文書）へ
  Formal Term（正式用語）を一括適用する作業

[Writing Convention](../conventions/writing.md)
は、Human-readable Natural Language Representation（人間可読な自然言語表現）を
対象とするConvention（規約）であり、
本文書が定義するModel（モデル）の
下位利用者になり得る。
Presentation Requirement（表示要求）を担う責務は、
Current Repository（現在のRepository）では同Convention（規約）に該当する。

ただし本文書は、同Convention（規約）との
Concrete Dependency（具体依存）を今回設計しない。
本文書は、同Convention（規約）が定義する
Normative Rule（規範的ルール）を前提とせず、
それを本文書側で変更・再定義することもしない。
同Convention（規約）が現在
Formal English Term（正式英語用語）の使用箇所へ
日本語説明の併記を要求していることは、
Presentation Rule（表示規則）側の判断である。
本Model（モデル）における
Canonical Representation Availability（正規表現の利用可能性）と
同一視しない。

### 導入しないConcept（概念）

- **Terminology Referent（用語参照対象）の
  Universal Entity Type（汎用実体種別）化**

  Repository上のあらゆる対象を分類する
  Entity Model（実体モデル）を導入しない。
  Terminology Referent（用語参照対象）は、
  Formal Terminology（正式用語）の
  Relationship（関係）の中で成立する
  Role（役割）に留める。

- **Term Taxonomy（用語分類体系）**

  Terminology Referent（用語参照対象）のSubtype（下位型）、
  およびFormal Term（正式用語）の分類体系を導入しない。
  Formal Name（正式名称）・Concept Name（概念名称）・
  Role Name（役割名称）についても、
  本文書が保持するのは境界のみである。

- **`Source of Truth`**

  Definition Authority（定義権限）は
  [Documentation Structure Architecture](documentation-structure.md)
  が所有するConcept（概念）である。
  同じ責務を指す別の
  Architecture Concept（アーキテクチャ概念）を
  本文書で新規に導入しない。

### 記述・宣言に関する事項

- Metadata（構造化メタデータ）および
  Declaration（明示的宣言）のSchema
- Formal Term（正式用語）の機械可読な表現形式
- Validator / Linter / CLI等のTool（ツール）要求、
  およびAutomatic Replacement（自動置換）

これらはDesign Gap（設計不足）ではなく、
現時点で確定していない事項を先行決定しないための意図的な委譲である。

## Usage by Downstream Design（下位設計からの参照）

後続設計は、本文書を参照して次を前提にできる。
これらを再定義する必要はない。

1. Formal Term（正式用語）が何によって成立するか。
   → 「Formal Term（正式用語）」が示す
   Positive Condition（正の条件）による。
2. Formal Term Identity（正式用語同一性）が
   Representation（表現）から独立して成立すること。
   → 「Formal Term Identity（正式用語同一性）」による。
3. Formal Term（正式用語）に関する
   Definition Responsibility（定義責務）が及ぶ範囲。
   → 「Definition Authority Boundary（定義権限境界）」による。
4. Canonical Representation Element（正規表現要素）の保持と、
   その表示が別であること。
   → 「Representation Availability（正規表現の利用可能性）と
   Documentation Presentation（文書上の表示）」による。
5. Canonical Japanese Explanation（正規日本語説明）が
   各Formal Term（正式用語）に必要な構成要素であること、および
   不在と非表示が別の状態であること。
   → 「Canonical Japanese Explanation（正規日本語説明）」および
   「Canonical Japanese Explanation（正規日本語説明）の不在と非表示」による。

### Canonical Declaration（正規宣言）を具体化する下位Asset

Canonical Declaration（正規宣言）を具体化する
下位のDocumentation Asset（文書資産）は、
本文書のModel（モデル）から、
少なくとも次の情報を保持し得ることを導出できる。

- Formal Term Identity（正式用語同一性）
- Formal Term（正式用語）と
  Terminology Referent（用語参照対象）の
  Relationship（関係）
- Canonical English Representation（正規英語表現）
- Canonical Japanese Explanation（正規日本語説明）

そのAsset（資産）は
Presentation Policy（表示方針）を所有しない。
次はCanonical Terminology Data（正規用語データ）ではなく、
Presentation Rule（表示規則）側の責務である。

- Title Presentation Requirement（文書題名における表示要求）
- Heading Presentation Requirement（見出しにおける表示要求）
- Body Presentation Requirement（本文における表示要求）
- Presentation Frequency（表示頻度）
- Context-specific Presentation Selection（文脈ごとの表示選択）

本文書は、そのAsset（資産）の成立要否、保持形式、
およびField（フィールド）構成を定義しない。

### 本文書からは判断できない事項

本文書からは判断できないのは、
どの用語がFormal Term（正式用語）として成立するかという個別の判定、
その用語のTerminology Referent Meaning（用語参照対象の意味）、
Canonical Documentation Representation（正規文書表現）の
具体的な表記形式、および
Presentation Requirement（表示要求）である。
これらは後続設計、または参照対象を所有する
Definition Authority（定義権限）の責務に属する。
