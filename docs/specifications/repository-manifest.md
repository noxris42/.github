# Repository Manifest Specification（リポジトリマニフェスト仕様）

## Purpose（目的）

Repository Manifestは、各リポジトリが共通リポジトリから選択する規約・テンプレート・ラベル・ワークフローと、それらの選択・配置関係を単一文書で宣言するためのものである。

Repository Manifestは、リポジトリ構築時には設計図として使用し、構築後は選択された共通資産とリポジトリ固有構成を確認・検証するための構成宣言として使用する。

READMEやCONTRIBUTINGのような文書一覧・規約一覧・利用案内を目的とする文書ではない。

---

## Scope（適用範囲）

本書は、Repository Manifestの構造・記述規則・検証方法を対象とする。

対象は以下を含む。

- 個別リポジトリに配置する`docs/repository-manifest.md`の構造
- 選択またはリポジトリ固有構成が発生するConvention
- 個別リポジトリへ展開するTemplate
- Label定義の取得元および配置先
- 個別リポジトリへ展開するWorkflow
- SourceおよびDestinationの記述規則
- 未選択・未設定状態の表現
- Manifest自体の宣言検証
- Manifestどおりに構築されているかの配置検証

以下は本書の対象外とする。

- Convention・Template・Label・Workflowの内容そのもの
- 資産をコピー・生成・同期・適用する具体的な処理
- Workflow内部の実装方式
- READMEやCONTRIBUTINGに記載する文書一覧・規約一覧
- Repository Profileの定義および選択規則
- リポジトリ固有の設計判断や運用方針本文

---

## File Location（配置関係）

Repository Manifestに関連するファイルは、以下の3種類に分かれる。

| 種別 | パス |
| --- | --- |
| Specification | `docs/specifications/repository-manifest.md` |
| Template | `templates/repository-manifest/repository-manifest.md` |
| Repository Manifest | `docs/repository-manifest.md` |

役割は以下のとおりである。

- Specification：構造と記述規則を定義する
- Template：個別リポジトリへ展開する初期雛形を提供する
- Repository Manifest：個別リポジトリで実際に選択された構成を宣言する

---

## Document Structure（文書構成）

Repository Manifestには、以下の4セクションをこの順序で必須とする。

1. `Conventions（規約構成）`
2. `Templates（適用テンプレート）`
3. `Labels（適用ラベル）`
4. `Workflows（適用ワークフロー）`

対象資産が存在しない場合でも、セクション自体は省略しない。対象資産が存在しないセクションには、次のように記載する。

```markdown
## Workflows（適用ワークフロー）

該当なし
```

Repository Manifestには、以下の情報を記載しない。

- リポジトリ名
- リポジトリ概要
- 利用方法
- 規約一覧
- ドキュメント一覧
- Repository Profile

---

## Conventions（規約構成）

### Conventionsの基本方針

`Conventions（規約構成）`には、すべての共通規約を列挙しない。

次のように、個別リポジトリで選択または固有構成が発生するConventionだけを記載する。

- Pattern Conventionの選択が必要
- 複数の適用方式から選択する
- Repository Conventionが存在する
- リポジトリごとに適用・不適用を選択する

共通Base Conventionが一律にそのまま適用されるだけの場合は、Manifestには記載しない。規約一覧や規約本文への案内は、READMEまたはCONTRIBUTINGの責務である。

### 記述形式

各Conventionは第3階層見出しと縦型表で記載する。

```markdown
## Conventions（規約構成）

### Branch Convention

| 項目 | 内容 |
| --- | --- |
| Base Convention | `noxris42/.github@docs/conventions/branch.md` |
| Pattern Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Repository Convention | — |
```

項目は以下の3つである。

- `Base Convention`
- `Pattern Convention`
- `Repository Convention`

`Base Convention`は必須とする。

Patternを使用しないことが許可されている場合は、`Pattern Convention`に`—`を記載する。Patternの選択が必須だが未選択の場合は、`<SELECT_REQUIRED>`を使用する。

上記の`branch-default.md`は記述形式を示すための概念例であり、本書執筆時点でPattern Convention自体が実装されていないConventionについては、実在資産として扱わない。

Repository Conventionが存在しない場合は、`Repository Convention`に`—`を記載する。

---

## Templates（適用テンプレート）

### Templatesの基本方針

`Templates（適用テンプレート）`には、個別リポジトリへ展開するTemplateを記載する。

各TemplateまたはTemplate Setは、第3階層見出しと次の縦型表で記載する。

```markdown
| 項目 | 内容 |
| --- | --- |
| Source | ... |
| Destination | ... |
```

### 単一ファイル

単一ファイルとして提供されるTemplateは、SourceとDestinationの双方をファイルパスで記載する。

```markdown
### Standard Pull Request Template

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/pull-request-templates/standard/PULL_REQUEST_TEMPLATE.md` |
| Destination | `.github/PULL_REQUEST_TEMPLATE.md` |
```

### 複数ファイル

複数ファイルを不可分なTemplate Setとして採用する場合は、SourceとDestinationの双方をディレクトリパスで記載する。

```markdown
### Standard Issue Templates

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/issue-templates/standard/` |
| Destination | `.github/ISSUE_TEMPLATE/` |
```

ディレクトリを指定した場合は、Sourceディレクトリ配下のすべてのファイルおよびサブディレクトリを、相対構造を維持したままDestinationへ展開するものとする。

Template Set内の一部ファイルだけを選択・除外・個別指定する運用は許可しない。

SourceとDestinationの種別は一致させる。

- ファイル → ファイル
- ディレクトリ → ディレクトリ

以下は許可しない。

- ファイル → ディレクトリ
- ディレクトリ → ファイル

---

## Labels（適用ラベル）

### Labelsの基本方針

`Labels（適用ラベル）`には、個別リポジトリへ展開または作成するLabel定義の取得元と配置先を記載する。

Label Sync Workflowの内部処理やフォールバック先は、Repository Manifestの責務に含めない。

Labelsセクションは、次の表で記載する。

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | ... |
| Destination | ... |
```

### 個別ラベル定義なし

個別リポジトリへラベル定義を展開または作成しない場合は、次のように記載する。

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | — |
```

これは「個別ラベル定義を持たない」ことだけを示す。その状態でどのラベル定義が適用されるかは、Label Sync Workflow側の仕様および実装の責務である。

標準ラベルの参照先として、次をSourceに記載しない。

```text
noxris42/.github@templates/labels/standard/labels.yml
```

標準構成では、このテンプレートを個別リポジトリへコピーしないためである。

### 共通ラベル定義を展開

将来、Profile別などの共通ラベル定義を個別リポジトリへ展開する場合は、次の形式とする。

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/labels/software/labels.yml` |
| Destination | `.github/labels.yml` |
```

`software`は将来の配置例であり、Repository Profileの正式な定義として扱わない。

### 独自ラベル定義

共通リポジトリから取得せず、個別リポジトリで独自のLabel定義を作成する場合は、次の形式とする。

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | `.github/labels.yml` |
```

### 有効な組み合わせ

以下を有効とする。

| Source | Destination | 意味 |
| --- | --- | --- |
| `—` | `—` | 個別ラベル定義を持たない |
| 共通資産のファイルパス | 個別リポジトリ内のファイルパス | 共通ラベル定義を展開する |
| `—` | 個別リポジトリ内のファイルパス | 独自ラベル定義を作成する |

以下は無効とする。

| Source | Destination |
| --- | --- |
| 共通資産のパス | `—` |
| ディレクトリ | ファイル |
| ファイル | ディレクトリ |

Labelsでは`Mode`項目を追加しない。

---

## Workflows（適用ワークフロー）

### Workflowsの基本方針

`Workflows（適用ワークフロー）`には、個別リポジトリへ展開するWorkflowを記載する。

各WorkflowまたはWorkflow Setは、第3階層見出しと縦型表で記載する。

```markdown
### Label Sync Workflow

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/workflows/sync-labels.yml` |
| Destination | `.github/workflows/sync-labels.yml` |
```

Sourceには、Destinationへ実際に展開するWorkflow資産そのものを指定する。

Workflowが別のWorkflowまたはActionを利用する場合でも、その依存先をSourceとして指定してはならない。依存先はDestinationへ展開する資産ではないためである。

Workflowの呼び出し関係、再利用方式、および内部処理は、Repository Manifestの対象外とする。

Repository Manifestは現存資産の一覧ではなく、リポジトリ構成の設計図である。標準構成としてLabel Sync Workflowの適用が既に決まっている場合は、Sourceが未実装であっても、SourceおよびDestinationを記載した状態を維持する。この場合、Declaration Validationは構造・記述形式の完全性を検証して合格しうるが、Deployment Validationは対象Sourceが共通リポジトリ内に存在しないことを理由に不合格となる。Manifestの宣言完成と実際のリポジトリ構築完了は別の状態として扱う。

`該当なし`は、そのリポジトリで当該Workflowを適用する対象がそもそも存在しない（適用しないことが決まっている）場合に限って使用する。適用する予定があるが、Sourceとなる資産が未実装であることを理由に`該当なし`とはしない。

Workflowでも、単一ファイルと不可分なディレクトリセットの両方を許可する。ディレクトリを指定する場合は、配下のすべてのファイルおよびサブディレクトリを相対構造を維持して展開するものとする。

SourceとDestinationの種別は一致させる。

---

## Source and Destination Rules（SourceおよびDestinationの記述規則）

### Source

Sourceは、個別リポジトリへ展開する共通資産の取得元を示す。

共通リポジトリ内の資産は、次の形式で記載する。

```text
<owner>/<repository>@<repository-relative-path>
```

例：

```text
noxris42/.github@templates/pull-request-templates/standard/PULL_REQUEST_TEMPLATE.md
```

Sourceには以下を使用しない。

- GitHub Web URL
- Raw URL
- ローカル絶対パス
- リポジトリルート基準ではないパス
- Markdownアンカーを含むパス

共通資産から取得しない場合は`—`を使用する。

### Destination

Destinationは、個別リポジトリ内の配置先または独自資産の作成先を示す。

個別リポジトリルートを基準とした相対パスで記載する。

例：

```text
.github/workflows/sync-labels.yml
```

Destinationには以下を使用しない。

- リポジトリ名を含むパス
- GitHub Web URL
- ローカル絶対パス
- リポジトリ外を参照するパス
- `./`で始まるパス
- `../`を含むパス

配置または作成を行わない場合は`—`を使用する。

### ファイルとディレクトリ

ディレクトリパスには末尾の`/`を付ける。ファイルパスには末尾の`/`を付けない。

Conventionの参照項目はコピー元・配置先を表すものではないため、このSource／Destination規則の直接対象外である。

---

## Placeholder Values（プレースホルダー値）

以下の値を定義する。

| 値 | 意味 |
| --- | --- |
| `—` | 対象外、不要、または意図的に使用しない |
| `<SELECT_REQUIRED>` | 必須の選択が完了していない |
| `<SETUP_REQUIRED>` | 設定すべき具体値または配置先がまだ決定していない |

`—`は未設定を意味しない。必須選択が未完了の場合に`—`を使わない。

配置先が既に決まっているが、まだファイルが存在しないだけの場合は、`<SETUP_REQUIRED>`ではなく実際の予定パスを記載する。ファイルの存在有無はDeployment Validationで確認する。

`<SELECT_REQUIRED>`または`<SETUP_REQUIRED>`が残っているManifestは、宣言完成状態とみなさない。

`該当なし`はセクション全体に対象資産が存在しない場合だけに使用し、表内の値として使用しない。

---

## Validation（検証）

Validationは、以下の2段階に分ける。

### Declaration Validation（宣言検証）

Repository Manifest自体の記述が完全かを検証する。

少なくとも以下を確認する。

- 4つの必須セクションが定義順に存在する
- 対象なしのセクションに`該当なし`が記載されている
- 必須項目が欠落していない
- SourceおよびDestinationの形式が正しい
- ファイルとディレクトリの種別が対応している
- 必須のPattern Conventionが選択されている
- `<SELECT_REQUIRED>`および`<SETUP_REQUIRED>`が残っていない
- LabelsのSource／Destinationの組み合わせが有効である
- Conventionsに一律適用の共通規約一覧を重複記載していない

### Deployment Validation（配置検証）

Manifestに宣言された構成どおりに、リポジトリが構築されているかを検証する。

少なくとも以下を確認する。

- Manifestに記載されたSourceが共通リポジトリ内に存在する
- Sourceのファイル／ディレクトリ種別が正しい
- Manifestに記載されたDestinationが個別リポジトリ内に存在する
- Destinationのファイル／ディレクトリ種別が正しい
- Template SetおよびWorkflow Setが部分展開されていない
- ディレクトリ配下の相対構造が維持されている
- Repository Conventionの参照先が存在する
- 必須のPattern Conventionが選択されている

Manifestの宣言完成と、実際のリポジトリ構築完了は別の状態として扱う。

SourceとDestinationの内容一致や派生関係をどのように確認するかという具体的な実装方法は、本仕様の対象外とする。

---

## Examples（例）

### 1. 標準的なRepository Manifest全体例

```markdown
# Repository Manifest（リポジトリマニフェスト）

このManifestは、このリポジトリで選択する共通資産と、その配置関係を宣言する。

## Conventions（規約構成）

### Branch Convention

| 項目 | 内容 |
| --- | --- |
| Base Convention | `noxris42/.github@docs/conventions/branch.md` |
| Pattern Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Repository Convention | — |

## Templates（適用テンプレート）

### Standard Issue Templates

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/issue-templates/standard/` |
| Destination | `.github/ISSUE_TEMPLATE/` |

### Standard Pull Request Template

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/pull-request-templates/standard/PULL_REQUEST_TEMPLATE.md` |
| Destination | `.github/PULL_REQUEST_TEMPLATE.md` |

## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | — |

## Workflows（適用ワークフロー）

### Label Sync Workflow

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/workflows/sync-labels.yml` |
| Destination | `.github/workflows/sync-labels.yml` |
```

これは宣言完成状態（Declaration Validation合格）を示す概念上の完成例である。Branch PatternとLabel Sync Workflowは、本書執筆時点でSourceとなる資産（`branch-default.md`・`templates/workflows/sync-labels.yml`）がまだ共通リポジトリに実装されていないため、実際に構築すればDeployment Validationは不合格となる。Manifestの宣言完成と実際のリポジトリ構築完了は別の状態として扱う。

### 2. Branch Pattern選択例

```markdown
### Branch Convention

| 項目 | 内容 |
| --- | --- |
| Base Convention | `noxris42/.github@docs/conventions/branch.md` |
| Pattern Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Repository Convention | — |
```

この`branch-default.md`は、Pattern Convention実装後の予定構成を示す概念例であり、本書執筆時点での実在資産ではない。

### 3. Repository Conventionを持つ例

```markdown
### Branch Convention

| 項目 | 内容 |
| --- | --- |
| Base Convention | `noxris42/.github@docs/conventions/branch.md` |
| Pattern Convention | `noxris42/.github@docs/conventions/patterns/branch/branch-default.md` |
| Repository Convention | `docs/conventions/branch.md` |
```

本例も同様に、Pattern Convention実装後を想定した概念例である。

### 4. 単一ファイルTemplate例

```markdown
### Standard Pull Request Template

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/pull-request-templates/standard/PULL_REQUEST_TEMPLATE.md` |
| Destination | `.github/PULL_REQUEST_TEMPLATE.md` |
```

### 5. ディレクトリTemplate Set例

```markdown
### Standard Issue Templates

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/issue-templates/standard/` |
| Destination | `.github/ISSUE_TEMPLATE/` |
```

### 6. 個別ラベル定義なし

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | — |
```

### 7. 共通ラベル定義を展開

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/labels/software/labels.yml` |
| Destination | `.github/labels.yml` |
```

`software`は将来の配置例であり、本書執筆時点では実在しない概念例である。Repository Profileの正式な定義として扱わない。

### 8. 独自ラベル定義を作成

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | `.github/labels.yml` |
```

### 9. Label Sync Workflow配置例

```markdown
### Label Sync Workflow

| 項目 | 内容 |
| --- | --- |
| Source | `noxris42/.github@templates/workflows/sync-labels.yml` |
| Destination | `.github/workflows/sync-labels.yml` |
```

この例のSourceは、個別リポジトリへ配置するWorkflowファイルの予定パスを示す。共通リポジトリ上で当該Workflowから参照される別のWorkflowは、展開対象ではないためSourceとして記載しない。

### 10. 対象資産なしのセクション

```markdown
## Workflows（適用ワークフロー）

該当なし
```

### 11. `<SELECT_REQUIRED>`を含む未完了例

```markdown
### Branch Convention

| 項目 | 内容 |
| --- | --- |
| Base Convention | `noxris42/.github@docs/conventions/branch.md` |
| Pattern Convention | `<SELECT_REQUIRED>` |
| Repository Convention | — |
```

Pattern Convention自体が未実装であり、かつリポジトリ側でもまだ選択していない初期Templateの状態を示す。Example 2（Branch Pattern選択例）の完成状態に対して、これは選択未完了の状態を表す。

### 12. `<SETUP_REQUIRED>`を含む未完了例

```markdown
## Labels（適用ラベル）

| 項目 | 内容 |
| --- | --- |
| Source | — |
| Destination | `<SETUP_REQUIRED>` |
```
