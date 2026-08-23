# Commit Convention（コミット規約）

## Purpose（目的）

本文書は、`noxris42` において
**Commit（コミット）をどのような意味単位で成立させ、
Commit Message（コミットメッセージ）をどのように記述するか**
を定めるConvention Asset（規約資産）である。

本文書が扱う問いは次の4点である。

1. 1つのCommit（コミット）は何を表す単位なのか
   （Commit Semantic Unit／コミット意味単位）。
2. Commit Message（コミットメッセージ）はどのような構造を持つのか
   （Message Structure／メッセージ構造）。
3. Header（ヘッダー）は何を、どのような形式で表すのか
   （Type／Subject）。
4. Message Language（メッセージ言語）が変わったとき、
   何が変わり、何が変わらないのか。

Commit（コミット）はDiff（差分）の記録媒体であるだけでなく、
**その変更が何を目的として行われたのかを保持する場所**
でもある。
本文書は、その意味をCommit単位および
Commit Message（コミットメッセージ）上で一貫して成立させるための
規範を定める。

## Position（上位設計との関係）

本文書は
[Convention Architecture](../architecture/convention.md)
および
[Convention Authoring Convention](convention-authoring.md)
を上位Source（上位の情報源）として参照する。

Design Dependency（設計依存）は
**Convention Architecture → Convention Authoring Convention → 本文書**
の一方向とする。

```text
Convention Architecture（規約の意味構造）
        ▲
        │ refines（表記へ具体化する）
Convention Authoring Convention（規約記述表記）
        ▲
        │ conforms to（記述表記に従う）
Commit Convention（本文書）
```

本文書は
[Repository Governance Documentation Framework Architecture](../architecture/repository-governance-documentation-framework.md)
が定義するConventions Area（規約領域）に属する
通常のDocumentation Asset（文書資産）である。
Commit（コミット）という反復的に発生する開発作業へ
繰り返し適用される
Reusable Normative Standard（再利用可能な規範標準）として成立する。

本文書が使用する次のConcept（概念）の
Definition Authority（定義権限）は上位設計にある。
本文書はこれらを参照するのみで、再定義しない。

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

本文書は、Documentation Asset（文書資産）のIdentity（同一性）、
Formal Name（正式名称）の成立条件、および
Naming Convention（命名規約）を定義しない。
これらを、Commit Header（コミットヘッダー）を記述する必要から
本文書側で新たに成立させることもしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Commit Semantic Unit（コミット意味単位）と
  Semantic Split Boundary（意味分割境界）
- Commit Message（コミットメッセージ）の構造
- Header Format（ヘッダー形式）
- Type（変更種別）のClosed Set（閉じた集合）と
  Gitmoji（Git絵文字）の対応
- Subject（主題）のSemantic Structure（意味構造）
- Change Subject（変更主体）の確定と
  Change Subject Representation（変更主体表現）の決定
- Operation（操作）の表現と
  Preferred Operation Vocabulary（推奨操作語彙）
- Message Language（メッセージ言語）の決定
- Body（本文）のInformation Responsibility（情報責務）

### Out of Scope（本文書が定義しない範囲）

- Footer（フッター）、`Refs`、`BREAKING-CHANGE`、
  Trailer（トレーラー）等のStructured Entry（構造化項目）
- Metadata（構造化メタデータ）およびDeclaration（明示的宣言）のSchema、
  Message Language Override（メッセージ言語上書き）の
  宣言方法・保存場所
- Commit Message（コミットメッセージ）の
  完全なConstruction Algorithm（構築アルゴリズム）、
  および文字列レベルのReproducibility（再現性）
- Type（変更種別）とOperation（操作）の
  組合せ表（Type × Operation Matrix）
- Documentation Asset（文書資産）のIdentity（同一性）、
  Formal Name（正式名称）の成立条件、
  およびNaming Convention（命名規約）
- Branch（ブランチ）、Merge（マージ）、Pull Request、Issue、
  Release（リリース）、Versioning（版管理）、Tag運用
- Commit（コミット）を解析・生成するTool（ツール）との
  Compatibility（互換性）要求
- Convention Application（規約適用）、
  Override（上書き）／Extension（拡張）等の
  Rule Relationship（ルール間関係）

## Concrete Declarations（具体宣言）

本節はConcrete Identifier Assignment（具体識別子割当）の宣言である。
**Normative Rule（規範的ルール）ではない** 。

### Convention Code（規約コード）

本Convention Asset（規約資産）のConvention Code（規約コード）は次である。

```text
Convention Code: CMT
```

### Namespace Code（名前空間コード）

本文書のNormative Rule（規範的ルール）は、
[Convention Authoring Convention](convention-authoring.md)
が割り当てたNamespace Code（名前空間コード） `SF`
（Shared Foundation Namespace／共有基盤名前空間）に属する。

本文書はNamespace Code（名前空間コード）を新たに割り当てない。

## Commit Model（コミットモデル）

本節は、本文書のNormative Rule（規範的ルール）が前提とする
Concept（概念）を示す。
本節はNon-normative Content（非規範的内容）である。

### Semantic Change（意味上の変更）

Commit（コミット）が表すのは、
Fileの物理的な変更の集合ではなく、
**一つの意味的な変更** である。

```text
Commit
= 1つのChange Subject（変更主体）
+ 1つのSemantic Purpose（意味上の目的）
```

したがって次は成立しない。

```text
1 Commit = 1 File
```

複数File、参照更新、Test、Navigation等の
Concrete Change（具体変更）が、
一つの実在するChange Subject（変更主体）と
一つのSemantic Purpose（意味上の目的）へ従属する場合、
それらは同一のSemantic Change（意味上の変更）を構成する。

### Change Subject（変更主体）

Change Subject（変更主体）は、
そのCommitのSemantic Purpose（意味上の目的）の中心となる
**意味的対象** である。

Change Subject（変更主体）になり得るものは、
Documentation Asset（文書資産）に限られない。
Model（モデル）、Concept（概念）、Capability（能力）、
Rule（規則）、Configuration（設定）、
Infrastructure（基盤）等も成立し得る。

### Semantic Purpose（意味上の目的）

Semantic Purpose（意味上の目的）は、
そのChange Subject（変更主体）に対して
**何を成立させようとしているのか** である。

Type（変更種別）は、
このSemantic Purpose（意味上の目的）から選択される。

### Change Subject Representation（変更主体表現）

Semantic Change Subject（意味上の変更主体）の確定と、
Header（ヘッダー）へ表示する名称の決定は、別の段階である。

```text
Change Set（変更の集合）
        ↓
Semantic Change Subject（意味上の変更主体）を確定
        ↓
Change Subject Representation（変更主体表現）を決定
```

この順序が逆転すると、
表現しやすい名称からChange Subject（変更主体）が逆算されることになり、
Commitの意味単位そのものが表記の都合へ従属する。

### Operation（操作）

Operation（操作）は、
Change Subject（変更主体）に生じた
**状態変化** を表す。

Operation（操作）はSubject（主題）の必須意味要素であるが、
その語彙はClosed Set（閉じた集合）ではない。

### Information Responsibility（情報責務）

Commit（コミット）が保持する情報の責務分担は次である。

```text
Header = What（何をどう変更したか）
Body   = Commit-specific Why / Context（Commit固有の理由・背景）
Diff   = How（どのように変更したか）
```

Diff（差分）がすでに保持している情報を
Commit Message（コミットメッセージ）へ再記述しても、
新しい情報は生じない。

### Semantic Identifier（意味識別子）と自然言語表現

Commit Semantic Model（コミット意味モデル）は、
Message Language（メッセージ言語）から独立している。

| 層 | 内容 | Message Languageの影響 |
| --- | --- | --- |
| Semantic Identifier（意味識別子） | Type（変更種別）、Operation Semantic Key（操作意味キー）、Change Subject Identity（変更主体同一性） | 受けない |
| Natural Language Representation（自然言語表現） | Subject（主題）およびBody（本文）の文言 | 受ける |

## Normative Rules（規範的ルール）

以降の各Section（節）は、1つのNormative Rule（規範的ルール）を記述する。

各Rule（ルール）の見出しは
Rule Boundary（規則境界）とDocument Presentation（文書表現）のためにあり、
Rule Model（ルールモデル）のCanonical Representation（正規表現）ではない。

Category（分類）を示す小見出しは文書上の整理のためのものであり、
Rule ID（規約ルールID）はCategory（分類）を表現しない。

### Commit Unit（コミット単位）

#### CMT-SF-001 — Single Semantic Change

**Rule ID:** `CMT-SF-001`

**Rule Name:** Single Semantic Change

**Stability:** Development

**Requirement:** MUST

**Rule:** 1つのCommit（コミット）は、
1つのChange Subject（変更主体）に対する
1つのSemantic Purpose（意味上の目的）を持つ
Semantic Change（意味上の変更）を表す。
複数のConcrete Change（具体変更）を含む場合は、
それらがその単一のChange Subject（変更主体）と
Semantic Purpose（意味上の目的）へ従属するかどうかによって、
同一Commitへ含めてよいかを判断する。

**Reason:** Commit（コミット）が意味単位でなければ、
履歴は「いつ何が触られたか」の記録に留まり、
「何を成立させようとしたか」を後から復元できない。
Fileの数や物理的なまとまりを単位にすると、
一つの意味的変更が複数Commitへ分断され、
逆に無関係な変更が同一Commitへ同居する。

**Note:** `1 Commit = 1 File` ではない。
複数File・参照更新・Test・Navigation等の
Concrete Change（具体変更）は、
同一のChange Subject（変更主体）と
Semantic Purpose（意味上の目的）へ従属する限り、
同一Commitに含められる。

#### CMT-SF-002 — Semantic Split Boundary

**Rule ID:** `CMT-SF-002`

**Rule Name:** Semantic Split Boundary

**Stability:** Development

**Requirement:** MUST

**Rule:** 独立したChange Subject（変更主体）または
独立したSemantic Purpose（意味上の目的）が複数存在する場合は、
それらを同一Commit（コミット）へ含めず、Commitを分割する。
このとき、複数の変更を1つのCommitへまとめることのみを目的として、
実在しないHigher-order Change Subject（上位変更主体）を作らない。

**Reason:** 分割境界を意味に置かなければ、
Commitの粒度は作業の区切りやTool操作の都合で決まる。
また、まとめるためだけの曖昧な上位語を許すと、
どのような組合せでも1つの
Change Subject（変更主体）へ言い換えられてしまい、
Single Semantic Change（単一意味変更）の要求が実質的に無効化される。

### Message Structure（メッセージ構造）

#### CMT-SF-003 — Message Structure

**Rule ID:** `CMT-SF-003`

**Rule Name:** Message Structure

**Stability:** Development

**Requirement:** MUST

**Rule:** Commit Message（コミットメッセージ）は、
必須のHeader（ヘッダー）と、任意のBody（本文）から構成する。
Body（本文）を記述する場合は、
Header（ヘッダー）との間を1つの空行で分離する。
本Convention（規約）は、これ以外の構成要素を定義しない。

**Reason:** 先頭行がHeader（ヘッダー）であることを固定すると、
一覧表示や履歴の走査において、
各Commitの意味を先頭行だけで判別できる。
空行による分離は、
Header（ヘッダー）の終端をBody（本文）の内容から
一意に確定させるために必要である。
構成要素を最小限に留めるのは、
現時点でRequirement（要求）が確認されていない項目を
先行して固定しないためである。

**Note:** 構造は次である。

````text
Header
[Body]
````

### Header（ヘッダー）

#### CMT-SF-004 — Header Format

**Rule ID:** `CMT-SF-004`

**Rule Name:** Header Format

**Stability:** Development

**Requirement:** MUST

**Rule:** Header（ヘッダー）は
`<gitmoji> <type>: <subject>` の形式で記述する。
`<gitmoji>` と `<type>` の間は半角空白1つで区切り、
`<type>` の直後にコロンと半角空白1つを置く。
Scope（スコープ）は使用しない。

**Reason:** Header（ヘッダー）の
Information Responsibility（情報責務）は
Commit-level What（Commit単位で何をどう変更したか）であり、
Type（変更種別）とSubject（主題）だけでこれを満たせる。
Scope（スコープ）を導入すると、
Change Subject（変更主体）がScope（スコープ）とSubject（主題）へ
二重に現れ、どちらが意味上の主体かが曖昧になる。

**Note:** 記述例は次である。

````text
📝 docs: Repository READMEを改定
````

#### CMT-SF-005 — Type Selection

**Rule ID:** `CMT-SF-005`

**Rule Name:** Type Selection

**Stability:** Development

**Requirement:** MUST

**Rule:** `<type>` は、そのCommit（コミット）の
Semantic Purpose（意味上の目的）から選択する。
File拡張子、Directory、変更File数、使用Tool等の
Physical Attribute（物理属性）のみを根拠として決定しない。
`chore` は、Repository Maintenance（Repository保守）そのものが
Semantic Purpose（意味上の目的）である場合に使用し、
分類できない場合のFallback（フォールバック）として使用しない。

**Reason:** Type（変更種別）が物理属性から決まるのであれば、
それはDiff（差分）から機械的に導ける情報の再掲であり、
Commit Message（コミットメッセージ）が
目的を保持する意味がなくなる。
`chore` をFallback（フォールバック）として許すと、
判断が難しいCommitほど `chore` へ流れ、
Type（変更種別）全体の識別力が失われる。

#### CMT-SF-006 — Base Type and Gitmoji Set

**Rule ID:** `CMT-SF-006`

**Rule Name:** Base Type and Gitmoji Set

**Stability:** Development

**Requirement:** MUST

**Rule:** `<type>` は、次のClosed Set（閉じた集合）から選択する。
`<gitmoji>` は、選択したType（変更種別）に対応するものを使用する。
Type（変更種別）とGitmoji（Git絵文字）の対応は1:1であり、
Gitmoji（Git絵文字）をType（変更種別）から独立して選択しない。

| Gitmoji | Type | Meaning |
| :---: | --- | --- |
| ✨ | `feat` | Capability / Functionality（能力・機能）の意味を成立・変更する |
| 🐛 | `fix` | 意図されたBehavior / Configuration（振る舞い・設定）へ回復する |
| ⚡ | `perf` | Behavior（振る舞い）を維持したPerformance / Efficiency（性能・効率）の改善 |
| 📦 | `build` | Dependency / Build / Packaging / Artifact Generation（依存関係・構築・包装・成果物生成）の変更 |
| ⏪ | `revert` | 過去の変更効果の取り消し |
| 📝 | `docs` | Documentation Asset（文書資産）の内容・定義の成立・変更 |
| ♻️ | `refactor` | Behavior（振る舞い）を維持した内部構造・責務の変更 |
| 💄 | `style` | Meaning / Behavior（意味・振る舞い）を変えないPresentation（表現）の変更 |
| ✅ | `test` | Test Asset / Test Infrastructure（テスト資産・テスト基盤）の変更 |
| 👷 | `ci` | CI/CD Automation（CI/CD自動化）の変更 |
| 🔧 | `chore` | Repository Maintenance（Repository保守）を主目的とする変更 |

**Reason:** Type（変更種別）を閉じた集合に保つことで、
履歴全体を有限個の意味区分で走査でき、
同じ目的の変更が複数の語で表現されることを防げる。
Gitmoji（Git絵文字）を独立した選択肢にしないのは、
同じType（変更種別）に複数の記号が対応すると、
記号が意味を持たない装飾になるためである。

### Subject（主題）

#### CMT-SF-007 — Subject Composition

**Rule ID:** `CMT-SF-007`

**Rule Name:** Subject Composition

**Stability:** Development

**Requirement:** MUST

**Rule:** `<subject>` は、
Change Subject Representation（変更主体表現）と
Operation Representation（操作表現）から構成し、
そのCommit（コミット）のWhat（何をどう変更したか）を表す。
Why（理由）を `<subject>` へ含めない。

**Reason:** Subject（主題）に必要な意味要素を固定することで、
何が変わったのかを読み取れないHeader（ヘッダー）が成立しなくなる。
Why（理由）をSubject（主題）へ含めないのは、
Header（ヘッダー）とBody（本文）の
Information Responsibility（情報責務）を分離し、
同じ情報が両方へ重複して現れることを防ぐためである。

**Note:** Subject（主題）の
Semantic Structure（意味構造）は次である。

````text
Subject
= Change Subject Representation
+ Operation Representation
````

日本語の助詞や英語の語順等、
Natural Language Representation（自然言語表現）上の形は固定しない。

#### CMT-SF-008 — Change Subject Selection

**Rule ID:** `CMT-SF-008`

**Rule Name:** Change Subject Selection

**Stability:** Development

**Requirement:** MUST

**Rule:** Change Subject（変更主体）は、
そのCommit（コミット）のSemantic Purpose（意味上の目的）の
中心となる意味的対象として確定する。
あるFileまたはDocumentation Asset（文書資産）を変更したという
Physical Fact（物理的事実）のみを根拠に、
それをChange Subject（変更主体）としない。

**Reason:** 変更されたFileをそのまま
Change Subject（変更主体）とすると、
Commitの意味は常にDiff（差分）の写像になり、
複数Fileにまたがる一つの意味的変更を表現できなくなる。
意味的対象から確定することで、
Change Subject（変更主体）がCommitの目的と一致した単位で成立する。

**Note:** Change Subject（変更主体）は、
Documentation Asset（文書資産）、Model（モデル）、Concept（概念）、
Capability（能力）、Rule（規則）、Configuration（設定）、
Infrastructure（基盤）等になり得る。

#### CMT-SF-009 — Change Subject Representation

**Rule ID:** `CMT-SF-009`

**Rule Name:** Change Subject Representation

**Stability:** Development

**Requirement:** MUST

**Rule:** Change Subject Representation（変更主体表現）は、
Semantic Change Subject（意味上の変更主体）を確定させたうえで決定する。
Representation（表現）からChange Subject（変更主体）を逆算しない。
Repository内ですでに利用可能な
Explicit State（明示状態）、Formal Name（正式名称）、
安定した名称等が存在する場合は、それを優先して使用する。
Formal Name（正式名称）が存在しないことを理由に、
Change Subject（変更主体）そのものを変更しない。
Commit Header（コミットヘッダー）を記述するためだけに、
新しいFormal Name（正式名称）、Identity（同一性）、
Documentation Rule（文書規則）を成立させない。

**Reason:** 確定と表現を分離しなければ、
名称を与えやすい対象がChange Subject（変更主体）として選ばれ、
Commitの意味単位が表記の都合へ従属する。
既存の名称を優先するのは、
同一の対象がCommitごとに別名で現れることを防ぐためである。
Header（ヘッダー）の都合で新しい正式名称や規則を作らないのは、
Commit Convention（コミット規約）が、
自身の責務外にあるDocumentation Identity（文書同一性）や
Naming（命名）の決定権を持たないためである。

**Note:** 代表的な例は次である。

````text
README.md
→ Repository README
→ 📝 docs: Repository READMEを改定
````

この例が成立するのは、
`Repository README` という安定した
Change Subject Representation（変更主体表現）が、
Current Source（現在の情報源）または
Explicit State（明示状態）によって利用可能な場合である。

その名称が利用可能でない場合、
本Convention（規約）は
`README.md` というPath（パス）やDocumentation構造から
`Repository README` という名称を導出しない。
本Convention（規約）は、
Documentation構造からAsset名称を導出するModel（モデル）を持たない。
利用可能な名称が存在しない場合は、
そのCommitにおいて妥当な名称を記述側で選ぶ。

本例は、新たな
Documentation Identity（文書同一性）、
Naming Rule（命名規則）、
Metadata Schema（メタデータスキーマ）を定義しない。

#### CMT-SF-010 — Operation Expression

**Rule ID:** `CMT-SF-010`

**Rule Name:** Operation Expression

**Stability:** Development

**Requirement:** SHOULD

**Rule:** Operation Representation（操作表現）には、
Preferred Operation Vocabulary（推奨操作語彙）に
適切な語が存在する場合、その語を優先して使用する。
適切な語が存在しない場合は、
Preferred Operation Vocabulary（推奨操作語彙）に含まれない
Operation（操作）を使用してよい。

**Reason:** 頻出するOperation（操作）へ共通語を与えることで、
同じ状態変化がCommitごとに異なる語で表現されることを減らせる。
一方でOperation（操作）をClosed Set（閉じた集合）にすると、
語彙へ収まらない変更を表現するために
Change Subject（変更主体）やType（変更種別）の側が歪められる。
推奨に留めるのは、
語彙の統一よりも意味の正確さを優先するためである。

**Note:** Preferred Operation Vocabulary（推奨操作語彙）の内容は
「Preferred Operation Vocabulary（推奨操作語彙）」に示す。
推奨語彙に含まれないOperation（操作）が使用されること自体は、
Convention Gap（規約不足）ではない。
ある語を推奨語彙へ追加するかどうかは
Operational Judgment（運用上の判断）である。

### Message Language（メッセージ言語）

#### CMT-SF-011 — Message Language

**Rule ID:** `CMT-SF-011`

**Rule Name:** Message Language

**Stability:** Development

**Requirement:** MUST

**Rule:** Commit Message（コミットメッセージ）の
Natural Language Representation（自然言語表現）は、
Effective Message Language（有効メッセージ言語）に従う。
Effective Message Language（有効メッセージ言語）は、
Explicit Message Language（明示メッセージ言語）の指定がある場合は
その指定とし、指定がない場合はJapanese（日本語）とする。
Type（変更種別）、Operation Semantic Key（操作意味キー）、
Change Subject Identity（変更主体同一性）等の
Semantic Identifier（意味識別子）は、
Message Language（メッセージ言語）によって変化しない。
Formal Name（正式名称）、Identifier（識別子）、Product Name等は、
Message Language（メッセージ言語）の変更のみを理由として
翻訳・改称しない。

**Reason:** 既定言語を定めなければ、
同一Repositoryの履歴に複数言語のCommit Messageが混在し、
履歴を読むための前提が一定しない。
Semantic Identifier（意味識別子）を言語から独立させるのは、
言語設定の変更によってType（変更種別）や
Change Subject（変更主体）の同一性が変わってしまうと、
Commit Semantic Model（コミット意味モデル）が
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

Japanese（日本語）を既定とするのは、
本Shared Development Foundation（複数Repositoryで共有する開発基盤）の
Default Message Language（既定メッセージ言語）としてである。

Explicit Message Language（明示メッセージ言語）の
具体的な宣言方法・保存場所・Schemaは、
本Convention（規約）では定義しない。

### Body（本文）

#### CMT-SF-012 — Body Responsibility

**Rule ID:** `CMT-SF-012`

**Rule Name:** Body Responsibility

**Stability:** Development

**Requirement:** MAY

**Rule:** Body（本文）は、
Header（ヘッダー）だけでは保持できず、
そのCommit（コミット）を後から理解するために保存価値のある
Commit-specific Rationale / Context（Commit固有の理由・背景）を
記録するために使用してよい。
この許容は、File一覧、Section一覧、
Change Summary（変更要約）、Diff（差分）の自然言語化、
作業完了報告、およびHeader（ヘッダー）の単なる言い換えには及ばない。

**Reason:** Header（ヘッダー）はWhat（何をどう変更したか）を、
Diff（差分）はHow（どのように変更したか）をすでに保持している。
どちらにも残らないのは、
なぜその変更が必要だったかというCommit固有の理由・背景である。
Body（本文）をこの用途へ限定するのは、
Diff（差分）から得られる情報を自然言語で再記述しても
新しい情報が生じず、
かえって本当に必要な理由が埋没するためである。

**Note:** Information Responsibility（情報責務）の分担は次である。

````text
Header = What
Body   = Commit-specific Why / Context
Diff   = How
````

Body（本文）は任意である。
記録すべきCommit固有の理由・背景が存在しない場合は、
Body（本文）を記述しない。

## Preferred Operation Vocabulary（推奨操作語彙）

本節は `CMT-SF-010` が参照する
Preferred Operation Vocabulary（推奨操作語彙）の内容である。
本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。

各Entry（項目）は
English Semantic Key（英語意味キー）を基準とし、
Message Language（メッセージ言語）ごとの
Natural Language Representation（自然言語表現）を対応付ける。

Effective Message Language（有効メッセージ言語）ごとの
Operation Representation（操作表現）は次である。

| Effective Message Language | Operation Representation |
| --- | --- |
| Japanese（日本語） | 下表のJapanese列の語を使用する |
| English（英語） | Semantic Key（意味キー）をそのまま使用する |

English Semantic Key（英語意味キー）は
English（英語）における
Natural Language Representation（自然言語表現）としても成立するため、
English（英語）用の列を別に設けない。

上記以外のMessage Language（メッセージ言語）に対する
Natural Language Representation（自然言語表現）は、
現時点では対応付けていない。

| Semantic Key | Japanese | Usage Guidance（使用指針） |
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

各Entry（項目）は、
厳密な排他的Selection Boundary（選択境界）を定めるものではない。
複数のEntry（項目）が当てはまる場合は、
そのCommitのSemantic Purpose（意味上の目的）に
最も近いものを選ぶ。

## Self Application（本文書自身への適用）

本文書は通常のConvention Asset（規約資産）であり、
[Convention Authoring Convention](convention-authoring.md)
が定めるRule（規則）に従って記述されている。

- Convention Code（規約コード）を
  「Concrete Declarations（具体宣言）」で明示的に宣言している。
- すべてのNormative Rule（規範的ルール）が
  `CMT-SF-NNN` 形式のRule ID（規約ルールID）を持つ。
- すべてのNormative Rule（規範的ルール）が、
  必須Field（フィールド）を規定の順序・表現で持つ。
- すべてのNormative Rule（規範的ルール）が
  `Stability: Development` である。
- Retired Rule ID（廃止済み規約ルールID）は現時点で存在しないため、
  `Retired Rule IDs` の記録を設けていない。

本節はNon-normative Content（非規範的内容）であり、
新たなNormative Requirement（規範要求）を追加しない。
