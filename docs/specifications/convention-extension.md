# Convention Extension Specification（規約拡張仕様）

## Purpose（目的）

Convention Extension Specificationは、Base Conventionを正本として維持しながら、Pattern ConventionおよびRepository ConventionがRule ID単位で明示的にRuleを拡張するための具体的な記述形式と検証規則を定義する。

本Specificationは、`docs/architecture/convention-extension.md`（Convention Extension Architecture）で定義されたレイヤー構造を、実際のMarkdown文書として記述可能にするものである。

本Specification自体は、各Conventionの内容や個別ルールを定義するものではない。

---

## Scope（適用範囲）

本書は、Convention拡張の具体的な構文・記述形式・操作規則・参照方法・配置規則・検証条件を対象とする。

対象は以下を含む。

- Rule IDの具体的な形式
- Scope識別子
- Ruleの継承と同一性
- 拡張操作（Replace・Extend・Disable・Add）
- Core HeaderとExtension Header
- Rule見出し形式
- Target Conventionの記述形式
- Pattern Conventionの配置規則
- Repository Conventionの配置規則
- Rule参照と適用規則
- 完全な有効内容の記述要件
- 禁止事項
- 検証条件
- 完成例と不正例

以下は本書の対象外とする。

- Base／Pattern／Repository／Effective Conventionの責務の再定義
- Effective Conventionの具体的な自動生成実装
- 検証ツールやパーサーの実装
- 既存Rule IDの移行作業
- Repository Manifestの構造
- Branch Pattern各文書の具体的なルール内容
- 個別ConventionのRule Category定義
- Repository Profileの設計

---

## Relationships（関係性）

### Convention Extension Architectureとの関係

- Architectureは責務・関係性・適用順序を定義する
- Specificationは具体的な構文・操作・参照形式・配置・検証条件を定義する
- SpecificationはArchitectureを変更または上書きしない
- 両者が矛盾する場合はArchitectureを優先する

### Repository Manifest Specificationとの関係

- Repository Manifestは、適用するBase／Pattern／Repository Conventionを宣言する
- Convention Extension Specificationは、それらのConvention内部でRuleをどのように記述・拡張するかを定義する
- ManifestはRule単位の操作内容を保持しない
- Convention文書はManifestの資産宣言を代替しない

### Individual Conventionsとの関係

- 各Base Conventionは自身のRule CategoryとPattern選択要件を定義できる
- 本Specificationは個別ConventionのRule内容を定義しない
- Pattern ConventionおよびRepository Conventionは本Specificationの構文に従う

### Conventions READMEとの関係

`docs/conventions/README.md`および既存Conventionは、現在3要素のRule ID形式（`<Convention>-<Category>-<Number>`）を使用している。

本Specificationが定義する4要素形式を運用へ適用するには、Conventions READMEおよび既存ConventionのRule IDを先に移行する必要がある。

既存Rule IDの変換・対応付け・移行期間中の互換処理は、本Specificationの対象外とする。本Specificationに準拠するConvention拡張では、移行完了後の4要素Rule IDだけを使用する。移行が完了するまでの間、本Specificationが定義する拡張操作（Replace・Extend・Disable・Add）を実際のConvention文書へ適用しない。

---

## Terminology（用語）

| 用語 | 定義 |
| --- | --- |
| Base Rule | Base Conventionで新規定義されたRule |
| Pattern Rule | Pattern ConventionでAddされたRule、またはPattern Conventionで変更された有効Rule |
| Repository Rule | Repository ConventionでAddされたRule、またはRepository Conventionで変更された有効Rule |
| Target Rule | Replace・Extend・Disableの対象となる既存Rule |
| Effective Rule | 適用済みのConvention群から導出された現在有効なRule |
| Defining Convention | Rule IDを最初に定義したConvention |
| Applying Convention | 拡張操作を記述しているConvention |
| Full Effective Content | 操作適用後に有効となるRuleの完全な記述内容 |

Base Convention・Pattern Convention・Repository Convention・Effective Conventionというレイヤーそのものの定義は、Convention Extension Architectureを参照する。本書では再定義しない。

---

## Rule ID Structure（Rule ID構造）

### Rule IDの形式

```text
<Convention>-<Scope>-<Category>-<Number>
```

正規表現は次のとおりとする。

```regex
^[A-Z]{2}-[A-Z]{2}-[A-Z]{2}-[0-9]{3}$
```

各要素の意味は以下のとおりである。

| 要素 | 形式 | 意味 |
| --- | --- | --- |
| Convention | 英大文字2文字 | Conventionの識別子 |
| Scope | 英大文字2文字 | Ruleを最初に定義したレイヤーまたはPatternの識別子 |
| Category | 英大文字2文字 | Convention内のRule Category |
| Number | 3桁数字 | 同一Convention・Scope・Category内の連番 |

例：

```text
BR-BS-NM-001
BR-BD-NM-001
BR-RP-NM-001
```

上記のCategory（`NM`）は記述形式を示すための概念例であり、実在Conventionの具体的なRule割り当てと混同しない。

### 採番規則

- Numberは`001`から開始する
- 採番単位はConvention・Scope・Categoryの組み合わせとする
- Rule IDは一度使用したら再利用しない
- Rule削除後も欠番を維持する
- 連番に欠番が存在してもよい
- 文書内の表示順とNumber順は一致することをSHOULDとする
- Ruleの移動や見出し変更だけを理由にRule IDを変更しない

### Convention識別子

Convention識別子は、各Base Conventionに対応する2文字コードとする。既存Conventionで使用中のRule IDがある場合は、そのConvention識別子（`docs/conventions/README.md`のConvention Identifierテーブルを参照）との整合を確認する。

本Specification内で、すべてのConvention識別子一覧を新たに設計しない。

---

## Scope Identifiers（Scope識別子）

| Scope | 意味 |
| --- | --- |
| `BS` | Base Conventionで新規定義されたRule |
| Pattern固有コード | 特定Pattern Conventionで新規定義されたRule |
| `RP` | Repository Conventionで新規定義されたRule |

Branch ConventionのPattern固有コードは、次を予定値として例示する。

| Pattern | Scope |
| --- | --- |
| `main-only` | `MO` |
| `branch-required` | `RQ` |
| `branch-default` | `BD` |

Pattern Convention自体は本書執筆時点で未実装であるため、上記のPattern固有コードは予定値かつ概念例であり、実在するConventionの確定済みScopeではない。

### Scopeの決定規則

- ScopeはRuleを最初に定義したConventionレイヤーを示す
- Replace・Extend・DisableによってScopeを変更しない
- Pattern ConventionがBase Ruleを変更しても、Rule IDのScopeは`BS`のままとする
- Repository ConventionがPattern Ruleを変更しても、Rule IDのPattern Scopeを維持する
- AddだけがApplying Conventionに対応する新しいScopeを持つRule IDを作成する

---

## Rule Identity and Inheritance（Ruleの同一性と継承）

### Rule IDが示すもの

Rule IDは、特定の文言や特定ファイル内の段落ではなく、論理的に同一のRuleを識別するものとする。

- Replace・Extend・Disableは既存Rule IDを継承する
- Addは新しいRule IDを作成する
- RuleのSummary、Requirement、Reason、Examplesなどを変更しても、同一Ruleである限りRule IDを維持する
- Ruleの目的や責務が別物になる場合は、既存Ruleの変更ではなく新しいRuleとしてAddする
- Rule IDによって定義元レイヤーを識別できる
- 現在の有効内容はRule IDだけではなく、適用済みConvention群から導出される

### 継承

- 下位Conventionに記載されていないRuleは直前の有効状態からそのまま継承する
- 上位Convention全文を下位Conventionへ複製しない
- 操作対象Ruleだけを下位Conventionに記載する
- 同一Convention文書内で、同じTarget Ruleへ複数回作用してはならない

---

## Rule Structure（Rule構造）

### Core Header

すべてのRuleは、次の項目を持つCore Headerを使用する。

| 項目 | 内容 |
| --- | --- |
| Rule | Rule本文 |
| Requirement | Requirement Level |
| Source | Ruleの根拠または出典 |

Core Headerは、Base Rule、Add Rule、変更後Ruleのすべてで使用する。

### Extension Header

Replace・Extend・Disableでは、Core Headerに加えて次の項目を持つExtension Headerを使用する。

| 項目 | 内容 |
| --- | --- |
| Operation | `Replace`・`Extend`・`Disable`のいずれか |
| Target Convention | Target Rule IDを最初に定義したDefining Convention |
| Target Rule ID | 対象RuleのRule ID |

Addでは既存Ruleを対象としないため、Extension Headerを使用しない。

### 表の構造

Core HeaderとExtension Headerは別々の表に分けず、1つの縦型表として記載する。

ReplaceまたはExtendの例：

```markdown
| 項目 | 内容 |
| --- | --- |
| Rule | ... |
| Requirement | MUST |
| Source | ... |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |
```

項目順は以下に固定する。

1. Rule
2. Requirement
3. Source
4. Operation
5. Target Convention
6. Target Rule ID

Addでは次の3項目だけを使用する。

1. Rule
2. Requirement
3. Source

### Supporting Sections

Ruleには必要に応じて次の補助セクションを使用できる。

- Reason
- Examples
- Notes
- Exceptions

操作対象Ruleは、操作後の有効内容を下位Convention単体でも確認できるように記述する。

「上位Ruleの一部へ一文を追加する」だけの差分表現は禁止する。

### Rule Heading（Rule見出し）

#### BaseおよびAdd Rule

新規定義Ruleの見出しは次の形式とする。

```text
### <Rule ID>: <Rule Summary>
```

例：

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）
```

#### Replace・Extend・Disable

既存Ruleへ作用する見出しは次の形式とする。

```text
### <Rule ID>: <Rule Summary>: <Operation>
```

例：

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Replace
```

- 見出し先頭のRule IDはTarget Rule IDと一致する
- Operation表記はExtension HeaderのOperationと一致する
- Rule Summaryは操作後のRule内容を簡潔に表す
- ReplaceやExtendによってRule Summaryを変更してもRule IDは維持する
- Addの見出しには`: Add`を付けない

---

## Extension Operations（拡張操作）

操作は次の4種類とする。

- Replace
- Extend
- Disable
- Add

### Replace

既存Ruleの有効内容を置き換える。

- Target Rule IDを維持する
- 操作後の完全な有効内容を記載する
- 上位Ruleの一部だけを差分として記載しない
- Requirement、Source、Reason、Examples、Notes、Exceptionsも必要に応じて完全に再記載する
- Replace後は、Replace側の内容がそのRuleの有効内容となる

Replaceは、既存Ruleの責務を維持しながら内容を変更する場合に使用する。Ruleの目的自体が異なる場合は、DisableとAdd、または別RuleのAddを検討する。

### Extend

既存Ruleへ条件、例外、補足、要求などを追加して具体化する。

- Target Rule IDを維持する
- 操作後の完全な有効内容を記載する
- 追加部分だけを差分として記載しない
- 上位Ruleと追加内容を統合した結果を記載する
- Effective Convention上では、Extend後の統合済み内容だけが有効Ruleとなる

ReplaceとExtendの違いは次のように整理する。

- Replace：既存内容を別の有効内容へ置換する
- Extend：既存内容を維持したまま追加要件を統合する

ただし、この違いは文面の編集方法ではなく、論理的な操作意図によって区別する。

### Disable

既存Ruleを適用対象外にする。

- Target Rule IDを維持する
- Ruleを削除したことにはしない
- Core HeaderのRuleおよびRequirementには、無効化対象となる元Ruleの内容とRequirementをそのまま記載する
- 無効化されている状態は、RuleやRequirementの反転によってではなく、Operationが`Disable`であることによって表す
- 後続Conventionは、Disable済みRuleをそのままReplaceまたはExtendしてはならない
- 再有効化の仕組みは本Specificationでは定義しない
- Disable後も、Rule IDの履歴と対象関係は保持する
- Disable理由をReasonに明記する

Disableの例：

```markdown
### BR-BS-NM-002: Branch Name Character Set（ブランチ名の使用文字）: Disable

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は小文字・英数字・ハイフン（`-`）のみを使用する |
| Requirement | MUST |
| Source | Branch Convention |
| Operation | Disable |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-002` |

**Reason:**

このリポジトリが連携する既存ツールの制約により、文字種の制約を適用できないため、このRuleを無効化する。
```

RuleおよびRequirementには元Ruleの内容をそのまま記載し、新しい禁止事項や反対の要求へ書き換えない。無効化されているという事実はOperation（`Disable`）が示す。Reasonには、無効化した理由を記載する。

### Add

Applying Conventionで新しいRuleを追加する。

- 新しいRule IDを発行する
- Applying Conventionに対応するScopeを使用する
- Target ConventionおよびTarget Rule IDを持たない
- Operation項目を持たない
- 上位Conventionに存在しない独立Ruleとして追加する
- 後続ConventionからReplace・Extend・Disableの対象にできる

### Full Effective Content Requirements（完全な有効内容の要件）

Convention Extension Architectureで定義された「完全な有効内容」を、本Specification上の要件として次のとおり具体化する。

ReplaceおよびExtendでは、少なくとも次を満たす。

- Core Headerが完全である
- Extension Headerが完全である
- 操作後のRule本文が単独で理解できる
- Requirementが確定している
- Sourceが確定している
- 必要なReason、Examples、Notes、Exceptionsを含む
- 上位Conventionを参照しなければ意味が成立しない差分断片を残さない

次のような記述は禁止例とする。

```markdown
**Notes:**

Base Ruleに次を追加する。

- private repositoryでは例外とする
```

正しい例では、Base Ruleと追加内容を統合した完全なRuleを示す（Examples章の該当例を参照）。

「全文コピー」と「完全な有効内容」の違いは次のとおりである。

- 上位Convention文書全体をコピーしてはならない
- 操作対象となる個別Ruleについては、操作後の完全な内容を記載する

---

## Target Convention（対象Convention）

### Target Conventionの形式

```text
<repository>@<repository-relative-path>
```

例：

```text
noxris42/.github@docs/conventions/branch.md
```

同一リポジトリ内のConventionを参照する場合は、repository部分を省略し、リポジトリルート基準の相対パスだけを使用できる。

例：

```text
docs/conventions/branch.md
```

### 禁止形式

次を禁止する。

- GitHub Web URL
- Raw URL
- ローカル絶対パス
- リポジトリ外を示す`../`
- `./`で始まるパス
- Markdownアンカー
- ブランチ名やコミットSHAを含む固定URL
- Target Rule IDをパス末尾へ付加する形式

Ruleの特定は、Target ConventionとTarget Rule IDの組み合わせで行う。

### Target Conventionが示す対象

Target Conventionは、Target Rule IDを最初に定義したDefining Conventionを示す。Ruleの現在の有効内容がどこで最後に変更されたかではなく、そのRule IDがどの文書で定義されたかを表す。

- BaseでAddされたRuleのTarget ConventionはBase Conventionである
- PatternでAddされたRuleのTarget ConventionはそのPattern Conventionである
- RepositoryでAddされたRuleのTarget ConventionはそのRepository Conventionである
- Replace・Extend・DisableによってTarget Conventionは変化しない。Rule IDのDefining Conventionを常に維持する
- Repository Conventionは、Pattern Conventionを選択している場合でも、Base RuleのTarget Rule IDによってBase Conventionを直接Targetにできる
- 実際にどの適用済み内容へ作用するかは、Target Conventionではなく、Application Rulesで定義する逐次適用順序によって決まる
- Target Conventionの記載によって、逐次適用モデルを飛び越えて古い内容へ作用してはならない

#### 例：Repository ConventionがBase Ruleを直接参照する場合

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | （Base Ruleの内容にRepository固有の要求を統合した完全な内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |
```

`BR-BS-NM-001`はBase Conventionで定義されたRuleであるため、Target ConventionはBase Conventionを示す。Pattern Conventionが選択されており、Pattern適用後の有効状態が実際の操作対象になっている場合でも、Target Convention自体はDefining Convention（Base Convention）のまま変化しない。

#### 例：Repository ConventionがPattern Add Ruleを参照する場合

```markdown
### BR-BD-NM-001: Default Branch Naming Exception（既定ブランチ命名の例外）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | （Pattern ConventionでAddされた内容にRepository固有の要求を統合した完全な内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Target Rule ID | `BR-BD-NM-001` |
```

`BR-BD-NM-001`はPattern ConventionでAddされたRuleであるため、Target ConventionはそのPattern Conventionを示す。`branch-default.md`はPattern Convention未実装のため概念例である。

---

## Application Rules（適用規則）

### 適用順序

次の順序を維持する。

```text
Base Convention
    ↓
Pattern Convention
    ↓
Repository Convention
    ↓
Effective Convention
```

後段Conventionは、直前までに成立している有効状態へ作用する。

### RepositoryからBaseへの直接操作

Repository Conventionは、Pattern Conventionを選択している場合でも、Base RuleをTarget Rule IDによって直接操作できる。

ただし、これはPattern Conventionの適用結果を無視する意味ではない。同じBase RuleがPattern Conventionで既に変更されている場合、Repository Conventionはその変更後の有効状態へ作用する。

```text
Base Rule
    ↓ Pattern Replace
Pattern適用後のEffective Rule
    ↓ Repository Extend
Repository適用後のEffective Rule
```

### Pattern Ruleへの操作

Repository Conventionは、Pattern ConventionでAddされたRuleも対象にできる。この場合、Target Rule IDはPattern Scopeを持つRule IDになる。

例：

```text
BR-BD-NM-001
```

### 未選択Patternへの参照

選択されていないPattern Convention内のRuleを、Repository Conventionから参照してはならない。Repository Manifestで選択されたConvention構成と一致する必要がある。

### 同一文書内の重複

同一Convention文書内では、同じTarget Rule IDに対して複数の操作を記述してはならない。

禁止例：

```text
BR-BS-NM-001: Replace
BR-BS-NM-001: Extend
```

1つのRuleに複数の変更が必要な場合は、1つの操作後内容へ統合する。

---

## File Location（配置規則）

### Base Convention

既存のConvention配置に従う。

```text
docs/conventions/<convention>.md
```

### Pattern Convention

Pattern Conventionは次の形式で配置する。

```text
docs/conventions/patterns/<convention>/<pattern>.md
```

Branch Conventionの予定例：

```text
docs/conventions/patterns/branch/main-only.md
docs/conventions/patterns/branch/branch-required.md
docs/conventions/patterns/branch/branch-default.md
```

これらは本書執筆時点で未実装であり、予定構成例である。

### Repository Convention

Repository Conventionは対象リポジトリ側で次の形式を基本とする。

```text
docs/conventions/<convention>.md
```

Base ConventionとRepository Conventionは異なるリポジトリに配置されるため、相対パスが同じでも別の文書として成立する。

### Effective Convention

Effective Conventionの物理配置は本Specificationで必須化しない。生成する場合の具体的な配置先やファイル名は、将来の生成仕様へ委ねる。

---

## Validation Rules（検証規則）

Validationは少なくとも次の観点に分ける。

### Structural Validation

- Rule見出し形式が正しい
- Rule ID形式が正しい
- 必須Header項目が存在する
- Header項目順が正しい
- AddにExtension Headerが存在しない
- Replace・Extend・DisableにExtension Headerが存在する
- 見出しOperationとHeader Operationが一致する
- 見出しRule IDとTarget Rule IDが一致する

### Reference Validation

- Target Conventionが存在する
- Target Rule IDが参照経路上に存在する
- Target Rule IDのConvention識別子が対象Conventionと整合する
- 選択されていないPattern ConventionのRuleを参照していない
- Disable済みRuleへ不正な後続操作をしていない
- 同一文書内で同じTarget Rule IDへ複数回作用していない

### Identity Validation

- Replace・Extend・DisableでRule IDを変更していない
- Addで既存Rule IDを使用していない
- AddのScopeがApplying Conventionと一致する
- 使用済みRule IDを再利用していない
- CategoryとNumberの採番単位が正しい

### Content Validation

- Replace・ExtendがFull Effective Contentを持つ
- 差分断片だけを記述していない
- RequirementとSourceが確定している
- Disable理由が記載されている
- 下位Convention単体で操作後Ruleを理解できる
- Ruleの基本目的を逸脱する変更をReplaceとして扱っていない

### File Validation

- Pattern Conventionのパス形式が正しい
- Repository Conventionのパス形式が正しい
- Target Conventionのパス形式が正しい
- URL、絶対パス、アンカーなどの禁止形式を使用していない

具体的な検証ツールや自動化処理は本書の対象外とする。

---

## Examples（例）

以下の例は、可能な限りBranch Convention（`BR`）を使用して統一する。ただし、現在のBranch Conventionに実在しないRule IDやPatternファイルを使用する場合は、その旨を明示する。実在するRule IDと概念上のRule IDは混在させない。

なお、既存の`docs/conventions/branch.md`は本Specification策定前の3要素Rule ID形式（例：`BR-NM-001`）で記述されている。以下の例で使用する4要素形式のRule ID（例：`BR-BS-NM-001`）は、Rule ID移行が完了した後の状態を示す概念例であり、実際に`branch.md`へ反映済みのIDではない。移行が完了するまで、本章の例をそのまま実運用へ適用しない。

### 1. Base Rule

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は `<type>/<issue-number>-<short-description>` の形式とする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Type・Issue番号・説明の3要素を含めることで、ブランチ名のみで作業種別・Issueとの対応・内容が一読で把握できるため。
```

### 2. Pattern ConventionによるReplace

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Replace

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は `<issue-number>-<short-description>` の形式とする（Typeを省略する） |
| Requirement | MUST |
| Source | Branch Pattern Convention |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |

**Reason:**

main-only運用ではTypeによる作業分類の必要性が薄いため、命名形式を簡略化する。
```

`main-only.md`は未実装のため概念例である。

### 3. Pattern ConventionによるExtend

```markdown
### BR-BS-NM-002: Branch Name Character Set（ブランチ名の使用文字）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は小文字・英数字・ハイフン（`-`）のみを使用する。ただし、Pull Request必須運用では、ブランチ名の先頭にリリース種別を示す固定接頭辞（`release-`）を追加してもよい |
| Requirement | MUST |
| Source | Branch Pattern Convention |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-002` |

**Reason:**

BranchおよびPRを必須とする運用では、リリース関連ブランチを識別しやすくするため。
```

`branch-required.md`は未実装のため概念例である。

### 4. Pattern ConventionによるDisable

```markdown
### BR-BS-CR-001: Create Branch at Work Start（作業開始時のブランチ作成）: Disable

| 項目 | 内容 |
| --- | --- |
| Rule | BranchとPull Requestを使用する運用では、作業開始時にIssueに対応するBranchを作成する |
| Requirement | SHOULD |
| Source | Branch Pattern Convention |
| Operation | Disable |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-CR-001` |

**Reason:**

main-only運用ではBranch自体を作成しないため、作業開始時のBranch作成要求を無効化する。
```

`main-only.md`は未実装のため概念例である。

### 5. Pattern ConventionによるAdd

```markdown
### BR-MO-EX-001: Main-Only Direct Commit Exception（main-only運用の直接コミット例外）

| 項目 | 内容 |
| --- | --- |
| Rule | main-only運用では、Issueに対応する変更をmainブランチへ直接commitしてよい |
| Requirement | MAY |
| Source | Branch Pattern Convention |

**Reason:**

Branchを作成しない運用であるため、既存のException Ruleとは別に、main-only運用固有の直接作業を許可する独立Ruleとして追加する。
```

Scopeは`MO`（main-only）であり、`main-only.md`は未実装のため概念例である。

### 6. Repository ConventionによるBase RuleのReplace

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Replace

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は `<issue-number>_<short-description>` の形式とする（区切り文字にアンダースコアを使用する） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |

**Reason:**

このリポジトリが連携する既存ツールの制約により、区切り文字をアンダースコアへ置き換える必要がある。
```

### 7. Repository ConventionによるBase RuleのExtend

```markdown
### BR-BS-DL-001: Delete Branch after Merge（Merge後のブランチ削除）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | MergeされたBranchは削除する。ただし、`release/`で始まるBranchは削除せず保持する |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-DL-001` |

**Reason:**

リリース履歴の追跡のため、リリース関連Branchのみ削除対象から除外する。
```

### 8. Repository ConventionによるPattern Add RuleのReplaceまたはExtend

```markdown
### BR-MO-EX-001: Main-Only Direct Commit Exception（main-only運用の直接コミット例外）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | main-only運用では、Issueに対応する変更をmainブランチへ直接commitしてよい。ただし、本番環境へ影響する変更は事前にIssueへレビュー依頼を記載する |
| Requirement | MAY |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/patterns/branch/main-only.md` |
| Target Rule ID | `BR-MO-EX-001` |

**Reason:**

このリポジトリでは本番環境への影響が大きいため、直接commitの前にレビュー依頼を明示させる。
```

### 9. Repository ConventionによるAdd

```markdown
### BR-RP-EX-001: Hotfix Branch Naming（Hotfixブランチの命名例外）

| 項目 | 内容 |
| --- | --- |
| Rule | 緊急修正Branchは `hotfix/<issue-number>-<short-description>` の形式とする |
| Requirement | SHOULD |
| Source | Repository Override |

**Reason:**

このリポジトリでは緊急修正を通常のType体系と区別して識別する運用を採用しているため、独立Ruleとして追加する。
```

Scopeは`RP`（Repository Convention）である。

### 10. Target Conventionの同一リポジトリ省略形式

```markdown
| Target Convention | `docs/conventions/branch.md` |
```

Pattern ConventionとBase Conventionが同じ共通リポジトリ（`noxris42/.github`）内に存在するため、repository部分を省略できる。Repository Conventionから共通リポジトリのBase Conventionを参照する場合は、引き続き完全形式（`noxris42/.github@docs/conventions/branch.md`）を使用する。

### 11. Full Effective Contentの正しい例

```markdown
### BR-BS-NM-002: Branch Name Character Set（ブランチ名の使用文字）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は小文字・英数字・ハイフン（`-`）のみを使用する。ただし、private repositoryでは、社内管理番号を示す大文字プレフィックス（例：`PRJ-`）の使用を例外として認める |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-002` |

**Exceptions:**

private repositoryに限り、大文字プレフィックスの使用を認める。
```

Base Ruleの内容と追加内容を統合した完全なRule本文を記載しており、下位Convention単体で有効内容を理解できる。

### 12. 差分断片だけを記述した不正例

```markdown
### BR-BS-NM-002: Branch Name Character Set（ブランチ名の使用文字）: Extend

**Notes:**

Base Ruleに次を追加する。

- private repositoryでは例外とする
```

Core HeaderおよびExtension Headerが存在せず、追加分だけの差分断片であり、単独では有効内容を理解できない。

### 13. 同一Target Ruleへの重複操作の不正例

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Replace

| 項目 | 内容 |
| --- | --- |
| Rule | （1回目の変更内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |

### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | （2回目の変更内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |
```

同一Convention文書内で同じTarget Rule ID（`BR-BS-NM-001`）へ2回作用しており、禁止されている。

### 14. ReplaceでRule IDを変更した不正例

```markdown
### BR-BS-NM-099: Branch Name Format（ブランチ名形式）: Replace

| 項目 | 内容 |
| --- | --- |
| Rule | （変更内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |
```

見出しのRule ID（`BR-BS-NM-099`）とTarget Rule ID（`BR-BS-NM-001`）が一致しておらず、Replaceによって新しいRule IDへ変更したかのような不正な記述である。

### 15. Addで既存Rule IDを再利用した不正例

```markdown
### BR-RP-NM-001: Custom Naming Rule（固有命名規則）

| 項目 | 内容 |
| --- | --- |
| Rule | （新規Rule内容） |
| Requirement | MUST |
| Source | Repository Override |
```

このRule IDが既に同一Convention・Scope・Category内で使用済みの場合、既存Rule IDの再利用となり禁止される。

### 16. 未選択Pattern Ruleへの参照の不正例

```markdown
### BR-BD-NM-001: Default Branch Naming Exception（既定ブランチ命名の例外）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | （変更内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Extend |
| Target Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Target Rule ID | `BR-BD-NM-001` |
```

Repository ManifestでPattern Conventionとして`branch-default`を選択していない場合、この参照は不正である。Repository Manifestで選択されたConvention構成と一致しないRuleへの参照は禁止される。

### 17. SourceなしまたはTarget Rule IDなしの不正なExtension Header

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Replace

| 項目 | 内容 |
| --- | --- |
| Rule | （変更内容） |
| Requirement | MUST |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
```

SourceおよびTarget Rule IDが欠落しており、Core HeaderおよびExtension Headerが不完全である。

### 18. 見出しOperationとHeader Operationが不一致の例

```markdown
### BR-BS-NM-001: Branch Name Format（ブランチ名形式）: Extend

| 項目 | 内容 |
| --- | --- |
| Rule | （変更内容） |
| Requirement | MUST |
| Source | Repository Override |
| Operation | Replace |
| Target Convention | `noxris42/.github@docs/conventions/branch.md` |
| Target Rule ID | `BR-BS-NM-001` |
```

見出しの表記は`Extend`だが、Header内のOperationは`Replace`であり、両者が一致していない。
