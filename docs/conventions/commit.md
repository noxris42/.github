# Commit Convention（コミット規約）

## Purpose（目的）

本文書は、`noxris42` において
**Commitをどのような意味単位で成立させ、
Commit Messageをどのように記述するか**
を定めるConvention Asset（規約資産）である。

本文書が扱う問いは次の4点である。

1. 1つのCommitは何を表す単位なのか
   （Commit Semantic Unit）。
2. Commit Messageはどのような構造を持つのか
   （Message Structure）。
3. Headerは何を、どのような形式で表すのか
   （Type／Subject）。
4. Message Language（メッセージ言語）が変わったとき、
   何が変わり、何が変わらないのか。

CommitはDiffの記録媒体であるだけでなく、
**その変更が何を目的として行われたのかを保持する場所**
でもある。
本文書は、その意味をCommit単位および
Commit Message上で一貫して成立させるための
規範を定める。

## Relationships（関係）

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Commitという反復的に発生する開発作業へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

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

本文書は、Documentation Asset（文書資産）のIdentity（同一性）、
Formal Name（正式名称）の成立条件、および
Naming Conventionを定義しない。
これらを、Commit Headerを記述する必要から
本文書側で新たに成立させることもしない。

### Position（設計上の位置づけ）

本文書は
[Convention Architecture](../architecture/convention.md)
および
[Convention Authoring Convention](convention-authoring.md)
を上位Sourceとして参照する。

Design Dependency（設計依存）は
**Convention Architecture → Convention Authoring Convention → 本文書**
の一方向とする。

```text
Convention Architecture
        ▲
        │ refines
Convention Authoring Convention
        ▲
        │ conforms to
Commit Convention
```

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Commit Semantic Unitと
  Semantic Split Boundary
- Commit Messageの構造
- Header Format
- TypeのClosed Set（閉じた集合）と
  Gitmojiの対応
- SubjectのSemantic Structure（意味構造）
- Change Subject（変更主体）の確定と
  Change Subject Representation（変更主体表現）の決定
- Operationの表現と
  Preferred Operation Vocabulary（推奨操作語彙）
- Message Language（メッセージ言語）の決定
- BodyのInformation Responsibility

### Out of Scope（本文書が定義しない範囲）

- Footer、`Refs`、`BREAKING-CHANGE`、
  Trailer等のStructured Entry
- MetadataおよびDeclarationのSchema、
  Message Language Overrideの
  宣言方法・保存場所
- Commit Messageの
  完全なConstruction Algorithm、
  および文字列レベルのReproducibility
- TypeとOperationの
  組合せ表
- Documentation Asset（文書資産）のIdentity（同一性）、
  Formal Name（正式名称）の成立条件、
  およびNaming Convention
- Branch、Merge、Pull Request、Issue、
  Release、Versioning（版管理）、Tag運用
- Commitを解析・生成するToolとの
  Compatibility要求
- Convention Application（規約適用）、
  Override（上書き）／Extension等の
  Rule Relationship（規則間関係）

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的規則）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CMT
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的規則）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Commit Model（コミットモデル）

本節は、本文書のNormative Rule（規範的規則）が前提とする
Concept（概念）を示す。
本節はNon-normative Content（非規範的内容）である。

### Semantic Change（意味上の変更）

Commitが表すのは、
Fileの物理的な変更の集合ではなく、
**一つの意味的な変更** である。

```text
Commit
= 1つのChange Subject
+ 1つのSemantic Purpose
```

したがって次は成立しない。

```text
1 Commit = 1 File
```

複数File、参照更新、Test、Navigation等の
Concrete Changeが、
一つの実在するChange Subject（変更主体）と
一つのSemantic Purpose（意味上の目的）へ従属する場合、
それらは同一のSemantic Changeを構成する。

### Change Subject（変更主体）

Change Subject（変更主体）は、
そのCommitのSemantic Purpose（意味上の目的）の中心となる
**意味的対象** である。

Change Subject（変更主体）になり得るものは、
Documentation Asset（文書資産）に限られない。
Model、Concept（概念）、Capability、
Rule、Configuration、
Infrastructure等も成立し得る。

### Semantic Purpose（意味上の目的）

Semantic Purpose（意味上の目的）は、
そのChange Subject（変更主体）に対して
**何を成立させようとしているのか** である。

Typeは、
このSemantic Purpose（意味上の目的）から選択される。

### Change Subject Representation（変更主体表現）

Semantic Change Subjectの確定と、
Headerへ表示する名称の決定は、別の段階である。

```text
Change Set
        ↓
Semantic Change Subjectを確定
        ↓
Change Subject Representationを決定
```

この順序が逆転すると、
表現しやすい名称からChange Subject（変更主体）が逆算されることになり、
Commitの意味単位そのものが表記の都合へ従属する。

### Operation（操作）

Operationは、
Change Subject（変更主体）に生じた
**状態変化** を表す。

OperationはSubjectの必須意味要素であるが、
その語彙はClosed Set（閉じた集合）ではない。

### Information Responsibility（情報責務）

Commitが保持する情報の責務分担は次である。

```text
Header = What
Body   = Commit-specific Why / Context
Diff   = How
```

Diffがすでに保持している情報を
Commit Messageへ再記述しても、
新しい情報は生じない。

### Semantic Identifier and Natural Language Representation（Semantic Identifierと自然言語表現）

Commit Semantic Modelは、
Message Language（メッセージ言語）から独立している。

| 層 | 内容 | Message Language（メッセージ言語）の影響 |
| --- | --- | --- |
| Semantic Identifier | Type、Operation Semantic Key、Change Subject Identity | 受けない |
| Natural Language Representation（自然言語表現） | SubjectおよびBodyの文言 | 受ける |

## Normative Rules（規範的ルール）

以降の各Sectionは、1つのNormative Rule（規範的規則）を記述する。

各Ruleの見出しは
Rule Boundary（規則境界）とDocument Presentationのためにあり、
Rule Model（規則モデル）のCanonical Representationではない。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規則ID）はCategory（分類）を表現しない。

### Commit Unit（コミット単位）

#### CMT-SF-001 — Single Semantic Change（単一の意味上の変更）

**Rule ID:** `CMT-SF-001`

**Rule Name:** Single Semantic Change

**Stability:** Development

**Requirement:** MUST

**Rule:** 1つのCommitは、
1つのChange Subject（変更主体）に対する
1つのSemantic Purpose（意味上の目的）を持つ
Semantic Changeを表す。
複数のConcrete Changeを含む場合は、
それらがその単一のChange Subject（変更主体）と
Semantic Purpose（意味上の目的）へ従属するかどうかによって、
同一Commitへ含めてよいかを判断する。

**Reason:** Commitが意味単位でなければ、
履歴は「いつ何が触られたか」の記録に留まり、
「何を成立させようとしたか」を後から復元できない。
Fileの数や物理的なまとまりを単位にすると、
一つの意味的変更が複数Commitへ分断され、
逆に無関係な変更が同一Commitへ同居する。

**Note:** `1 Commit = 1 File` ではない。
複数File・参照更新・Test・Navigation等の
Concrete Changeは、
同一のChange Subject（変更主体）と
Semantic Purpose（意味上の目的）へ従属する限り、
同一Commitに含められる。

#### CMT-SF-002 — Semantic Split Boundary（意味上の分割境界）

**Rule ID:** `CMT-SF-002`

**Rule Name:** Semantic Split Boundary

**Stability:** Development

**Requirement:** MUST

**Rule:** 独立したChange Subject（変更主体）または
独立したSemantic Purpose（意味上の目的）が複数存在する場合は、
それらを同一Commitへ含めず、Commitを分割する。
このとき、複数の変更を1つのCommitへまとめることのみを目的として、
実在しないHigher-order Change Subjectを作らない。

**Reason:** 分割境界を意味に置かなければ、
Commitの粒度は作業の区切りやTool操作の都合で決まる。
また、まとめるためだけの曖昧な上位語を許すと、
どのような組合せでも1つの
Change Subject（変更主体）へ言い換えられてしまい、
Single Semantic Changeの要求が実質的に無効化される。

### Message Structure（メッセージ構造）

#### CMT-SF-003 — Message Structure（メッセージ構造）

**Rule ID:** `CMT-SF-003`

**Rule Name:** Message Structure

**Stability:** Development

**Requirement:** MUST

**Rule:** Commit Messageは、
必須のHeaderと、任意のBodyから構成する。
Bodyを記述する場合は、
Headerとの間を1つの空行で分離する。
本Convention（規約）は、これ以外の構成要素を定義しない。

**Reason:** 先頭行がHeaderであることを固定すると、
一覧表示や履歴の走査において、
各Commitの意味を先頭行だけで判別できる。
空行による分離は、
Headerの終端をBodyの内容から
一意に確定させるために必要である。
構成要素を最小限に留めるのは、
現時点でRequirementが確認されていない項目を
先行して固定しないためである。

**Note:** 構造は次である。

````text
Header
[Body]
````

### Header（ヘッダー）

#### CMT-SF-004 — Header Format（ヘッダーの形式）

**Rule ID:** `CMT-SF-004`

**Rule Name:** Header Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Headerは
`<gitmoji> <type>: <subject>` の形式で記述する。
`<gitmoji>` と `<type>` の間は半角空白1つで区切り、
`<type>` の直後にコロンと半角空白1つを置く。
Scopeは使用しない。

**Reason:** Headerの
Information Responsibilityは
Commit-level Whatであり、
TypeとSubjectだけでこれを満たせる。
Scopeを導入すると、
Change Subject（変更主体）がScopeとSubjectへ
二重に現れ、どちらが意味上の主体かが曖昧になる。

**Note:** 記述例は次である。

````text
📝 docs: Repository READMEを改定
````

#### CMT-SF-005 — Type Selection（Typeの選択）

**Rule ID:** `CMT-SF-005`

**Rule Name:** Type Selection

**Stability:** Development

**Requirement:** MUST

**Rule:** `<type>` は、そのCommitの
Semantic Purpose（意味上の目的）から選択する。
File拡張子、Directory、変更File数、使用Tool等の
Physical Attributeのみを根拠として決定しない。
`chore` は、Repository Maintenanceそのものが
Semantic Purpose（意味上の目的）である場合に使用し、
分類できない場合のFallbackとして使用しない。

**Reason:** Typeが物理属性から決まるのであれば、
それはDiffから機械的に導ける情報の再掲であり、
Commit Messageが
目的を保持する意味がなくなる。
`chore` をFallbackとして許すと、
判断が難しいCommitほど `chore` へ流れ、
Type全体の識別力が失われる。

#### CMT-SF-006 — Base Type and Gitmoji Set（基本TypeとGitmojiの集合）

**Rule ID:** `CMT-SF-006`

**Rule Name:** Base Type and Gitmoji Set

**Stability:** Development

**Requirement:** MUST

**Rule:** `<type>` は、次のClosed Set（閉じた集合）から選択する。
`<gitmoji>` は、選択したTypeに対応するものを使用する。
TypeとGitmojiの対応は1:1であり、
GitmojiをTypeから独立して選択しない。

| Gitmoji | Type | Meaning（意味） |
| :---: | --- | --- |
| ✨ | `feat` | Capability / Functionalityの意味を成立・変更する |
| 🐛 | `fix` | 意図されたBehavior / Configurationへ回復する |
| ⚡ | `perf` | Behaviorを維持したPerformance / Efficiencyの改善 |
| 📦 | `build` | Dependency（依存） / Build / Packaging / Artifact Generationの変更 |
| ⏪ | `revert` | 過去の変更効果の取り消し |
| 📝 | `docs` | Documentation Asset（文書資産）の内容・定義の成立・変更 |
| ♻️ | `refactor` | Behaviorを維持した内部構造・責務の変更 |
| 💄 | `style` | Meaning（意味） / Behaviorを変えないPresentationの変更 |
| ✅ | `test` | Test Asset / Test Infrastructureの変更 |
| 👷 | `ci` | CI/CD Automationの変更 |
| 🔧 | `chore` | Repository Maintenanceを主目的とする変更 |

**Reason:** Typeを閉じた集合に保つことで、
履歴全体を有限個の意味区分で走査でき、
同じ目的の変更が複数の語で表現されることを防げる。
Gitmojiを独立した選択肢にしないのは、
同じTypeに複数の記号が対応すると、
記号が意味を持たない装飾になるためである。

### Subject（主題）

#### CMT-SF-007 — Subject Composition（主題の構成）

**Rule ID:** `CMT-SF-007`

**Rule Name:** Subject Composition

**Stability:** Development

**Requirement:** MUST

**Rule:** `<subject>` は、
Change Subject Representation（変更主体表現）と
Operation Representationから構成し、
そのCommitのWhatを表す。
Whyを `<subject>` へ含めない。

**Reason:** Subjectに必要な意味要素を固定することで、
何が変わったのかを読み取れないHeaderが成立しなくなる。
WhyをSubjectへ含めないのは、
HeaderとBodyの
Information Responsibilityを分離し、
同じ情報が両方へ重複して現れることを防ぐためである。

**Note:** Subjectの
Semantic Structure（意味構造）は次である。

````text
Subject
= Change Subject Representation
+ Operation Representation
````

日本語の助詞や英語の語順等、
Natural Language Representation（自然言語表現）上の形は固定しない。

#### CMT-SF-008 — Change Subject Selection（変更主体の選択）

**Rule ID:** `CMT-SF-008`

**Rule Name:** Change Subject Selection

**Stability:** Development

**Requirement:** MUST

**Rule:** Change Subject（変更主体）は、
そのCommitのSemantic Purpose（意味上の目的）の
中心となる意味的対象として確定する。
あるFileまたはDocumentation Asset（文書資産）を変更したという
Physical Factのみを根拠に、
それをChange Subject（変更主体）としない。

**Reason:** 変更されたFileをそのまま
Change Subject（変更主体）とすると、
Commitの意味は常にDiffの写像になり、
複数Fileにまたがる一つの意味的変更を表現できなくなる。
意味的対象から確定することで、
Change Subject（変更主体）がCommitの目的と一致した単位で成立する。

**Note:** Change Subject（変更主体）は、
Documentation Asset（文書資産）、Model、Concept（概念）、
Capability、Rule、Configuration、
Infrastructure等になり得る。

#### CMT-SF-009 — Change Subject Representation（変更主体表現）

**Rule ID:** `CMT-SF-009`

**Rule Name:** Change Subject Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Change Subject Representation（変更主体表現）は、
Semantic Change Subjectを確定させたうえで決定する。
Representation（表現）からChange Subject（変更主体）を逆算しない。
Repository内ですでに利用可能な
Explicit State、Formal Name（正式名称）、
安定した名称等が存在する場合は、それを優先して使用する。
Formal Name（正式名称）が存在しないことを理由に、
Change Subject（変更主体）そのものを変更しない。
Commit Headerを記述するためだけに、
新しいFormal Name（正式名称）、Identity（同一性）、
Documentation Ruleを成立させない。

**Reason:** 確定と表現を分離しなければ、
名称を与えやすい対象がChange Subject（変更主体）として選ばれ、
Commitの意味単位が表記の都合へ従属する。
既存の名称を優先するのは、
同一の対象がCommitごとに別名で現れることを防ぐためである。
Headerの都合で新しい正式名称や規則を作らないのは、
Commit Conventionが、
自身の責務外にあるDocumentation Identityや
Namingの決定権を持たないためである。

**Note:** 代表的な例は次である。

````text
README.md
→ Repository README
→ 📝 docs: Repository READMEを改定
````

この例が成立するのは、
`Repository README` という安定した
Change Subject Representation（変更主体表現）が、
Current Sourceまたは
Explicit Stateによって利用可能な場合である。

その名称が利用可能でない場合、
本Convention（規約）は
`README.md` というPathやDocumentation構造から
`Repository README` という名称を導出しない。
本Convention（規約）は、
Documentation構造からAsset名称を導出するModelを持たない。
利用可能な名称が存在しない場合は、
そのCommitにおいて妥当な名称を記述側で選ぶ。

本例は、新たな
Documentation Identity、
Naming Rule（命名規則）、
Metadata Schemaを定義しない。

#### CMT-SF-010 — Operation Expression（操作の表現）

**Rule ID:** `CMT-SF-010`

**Rule Name:** Operation Expression

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Operation Representationには、
Preferred Operation Vocabulary（推奨操作語彙）に
適切な語が存在する場合、その語を優先して使用する。
適切な語が存在しない場合は、
Preferred Operation Vocabulary（推奨操作語彙）に含まれない
Operationを使用してよい。

**Reason:** 頻出するOperationへ共通語を与えることで、
同じ状態変化がCommitごとに異なる語で表現されることを減らせる。
一方でOperationをClosed Set（閉じた集合）にすると、
語彙へ収まらない変更を表現するために
Change Subject（変更主体）やTypeの側が歪められる。
推奨に留めるのは、
語彙の統一よりも意味の正確さを優先するためである。

**Note:** Preferred Operation Vocabulary（推奨操作語彙）の内容は
「Preferred Operation Vocabulary（推奨操作語彙）」に示す。
推奨語彙に含まれないOperationが使用されること自体は、
Convention Gapではない。
ある語を推奨語彙へ追加するかどうかは
Operational Judgmentである。

### Message Language（メッセージ言語）

#### CMT-SF-011 — Message Language（メッセージ言語）

**Rule ID:** `CMT-SF-011`

**Rule Name:** Message Language

**Stability:** Development

**Requirement:** MUST

**Rule:** Commit Messageの
Natural Language Representation（自然言語表現）は、
Effective Message Languageに従う。
Effective Message Languageは、
Explicit Message Languageの指定がある場合は
その指定とし、指定がない場合はJapaneseとする。
Type、Operation Semantic Key、
Change Subject Identity等の
Semantic Identifierは、
Message Language（メッセージ言語）によって変化しない。
Formal Name（正式名称）、Identifier（識別子）、Product Name等は、
Message Language（メッセージ言語）の変更のみを理由として
翻訳・改称しない。

**Reason:** 既定言語を定めなければ、
同一Repositoryの履歴に複数言語のCommit Messageが混在し、
履歴を読むための前提が一定しない。
Semantic Identifierを言語から独立させるのは、
言語設定の変更によってTypeや
Change Subject（変更主体）の同一性が変わってしまうと、
Commit Semantic Modelが
表記へ依存することになるためである。
Formal Name（正式名称）を翻訳しないのは、
名称が指す対象の同一性を保つためである。

**Note:** 決定順序は次である。

````text
Explicit Message Languageあり
→ その指定を優先

指定なし
→ Japanese
````

Japaneseを既定とするのは、
本Shared Development Foundationの
Default Message Languageとしてである。

Explicit Message Languageの
具体的な宣言方法・保存場所・Schemaは、
本Convention（規約）では定義しない。

### Body（本文）

#### CMT-SF-012 — Body Responsibility（本文の責務）

**Rule ID:** `CMT-SF-012`

**Rule Name:** Body Responsibility

**Stability:** Development

**Requirement:** MAY

**Rule:** Bodyは、
Headerだけでは保持できず、
そのCommitを後から理解するために保存価値のある
Commit-specific Rationale / Contextを
記録するために使用してよい。
この許容は、File一覧、Section一覧、
Change Summary、Diffの自然言語化、
作業完了報告、およびHeaderの単なる言い換えには及ばない。

**Reason:** HeaderはWhatを、
DiffはHowをすでに保持している。
どちらにも残らないのは、
なぜその変更が必要だったかというCommit固有の理由・背景である。
Bodyをこの用途へ限定するのは、
Diffから得られる情報を自然言語で再記述しても
新しい情報が生じず、
かえって本当に必要な理由が埋没するためである。

**Note:** Information Responsibilityの分担は次である。

````text
Header = What
Body   = Commit-specific Why / Context
Diff   = How
````

Bodyは任意である。
記録すべきCommit固有の理由・背景が存在しない場合は、
Bodyを記述しない。

## Preferred Operation Vocabulary（推奨操作語彙）

本節は `CMT-SF-010` が参照する
Preferred Operation Vocabulary（推奨操作語彙）の内容である。
本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。

各Entryは
English Semantic Keyを基準とし、
Message Language（メッセージ言語）ごとの
Natural Language Representation（自然言語表現）を対応付ける。

Effective Message Languageごとの
Operation Representationは次である。

| Effective Message Language | Operation Representation |
| --- | --- |
| Japanese | 下表のJapanese列の語を使用する |
| English | Semantic Keyをそのまま使用する |

English Semantic Keyは
Englishにおける
Natural Language Representation（自然言語表現）としても成立するため、
English用の列を別に設けない。

上記以外のMessage Language（メッセージ言語）に対する
Natural Language Representation（自然言語表現）は、
現時点では対応付けていない。

| Semantic Key | Japanese | Usage Guidance |
| --- | --- | --- |
| `establish` | 策定 | それまで存在しなかった定義・規則・体系を新たに成立させる |
| `revise` | 改定 | 既存の定義・規則の内容を、正式な形で改める |
| `add` | 追加 | 既存の構成を保ったまま要素を加える |
| `fix` | 修正 | 誤り・不整合・意図しない状態を正す |
| `unify` | 統一 | 複数に分かれていた表現・方式を1つへ揃える |
| `align` | 整合 | 他の定義・実装との食い違いを解消し、辻褄を合わせる |
| `build` | 構築 | 仕組み・環境・基盤を新たに組み立てる |
| `apply` | 適用 | すでに決まっている定義・規則を対象へ反映する |
| `update` | 更新 | 内容を現在の状態へ合わせる |
| `improve` | 改善 | 成立している内容を、より良い状態へ進める |
| `restructure` | 再構成 | 内容を保ったまま構造・配置を組み替える |
| `format` | 整形 | 意味を変えずに表記・体裁を整える |
| `remove` | 削除 | 要素を取り除く |
| `revert` | 取り消し | 過去の変更の効果を元へ戻す |
| `rename` | 改称 | 対象の名称を変更する |
| `migrate` | 移行 | 対象を別の方式・場所・基盤へ移す |

各Entryは、
厳密な排他的Selection Boundaryを定めるものではない。
複数のEntryが当てはまる場合は、
そのCommitのSemantic Purpose（意味上の目的）に
最も近いものを選ぶ。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRuleに従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations」で明示的に宣言している。
- すべてのNormative Rule（規範的規則）が
  `CMT-SF-NNN` 形式のRule ID（規則ID）を持つ。
- すべてのNormative Rule（規範的規則）が、
  必須Fieldを規定の順序・表現で持つ。
- すべてのNormative Rule（規範的規則）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規則ID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
