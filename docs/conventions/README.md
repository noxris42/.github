# Conventions README（規約共通基盤）

## Purpose（目的）

本書は、`docs/conventions/` 配下のすべてのConvention文書が共通して従う基盤を定義する。

Conventions は、Repository Philosophy・Documentation Philosophy・Repository Architecture・Documentation Architecture で定義された思想・構造を、日常運用で一貫して実践するための運用ルールを定義する層である。本書はその層全体に共通する運用原則・ルール形式・責務境界を定義し、各Convention文書の設計判断の出発点となる。

---

## Scope（適用範囲）

本書は `docs/conventions/` 配下のすべてのConvention文書に適用される。

初期対象は以下とする。将来追加されるConvention文書にも同様に適用する。

```text
docs/conventions/
├── README.md
├── markdown.md
├── writing.md
└── naming.md
```

Markdown・Writing・Namingなど固有の規約は本書の対象外とし、各Convention文書で定義する。

---

## Common Principles（共通運用原則）

本書はConventions全体の共通基盤である。各Convention文書に共通事項を重複して記述しない。共通事項は本書のみで管理し、各Convention文書は必要に応じて参照する。

各Convention文書は、その責務に固有のルールのみを定義する。

---

## Requirement Levels（要求レベル）

Conventions全体で共通して使用する要求レベルを以下のように定義する。各Convention文書では独自に再定義せず、本定義を参照する。

| Level | 意味 |
| --- | --- |
| MUST | 必ず従わなければならない |
| MUST NOT | 従ってはならない |
| SHOULD | 原則として従う。正当な理由がある場合に限り逸脱できる |
| SHOULD NOT | 原則として行わない。正当な理由がある場合に限り実施できる |
| MAY | 任意。状況に応じて選択できる |

---

## Rule Components（ルール構成要素）

Conventions全体で共通するルールの構成要素を以下のように定義する。表示レイアウトは各Convention文書が定義する。

Ruleは **Header** と **Body** の二層で構成する。

### Header（必須）

HeaderはRule全体の概要を示す構造データである。記述順序は以下に固定する。

| 順序 | 項目 | 内容 |
| --- | --- | --- |
| 1 | Rule | ルールの内容（簡潔な命令文） |
| 2 | Requirement | 要求レベル（MUST / MUST NOT / SHOULD / SHOULD NOT / MAY） |
| 3 | Source | ルールの根拠（後述のRule Sourcesを参照） |

### Body（任意）

BodyはRuleの理解を補助する説明データである。存在する項目のみ記述し、記述順序は以下に固定する。

| 順序 | 項目 | 内容 |
| --- | --- | --- |
| 1 | Reason | なぜそのルールが必要かの説明 |
| 2 | Examples | 適用例・非適用例 |
| 3 | Notes | 補足事項 |
| 4 | Exceptions | 例外が認められる条件 |

---

## Rule Sources（ルールの根拠）

ルールの根拠となる情報源を以下の3分類で管理する。

### External Standards（外部標準）

外部標準仕様を根拠とするもの。

例: CommonMark・GitHub Flavored Markdown・markdownlint・RFC

### Internal Standards（内部標準）

プロジェクト内の設計文書を根拠とするもの。

例: Repository Philosophy・Documentation Philosophy・Repository Architecture・Documentation Architecture

### Project Conventions（プロジェクト規約）

外部仕様では定義されない、このプロジェクト固有の運用ルールを根拠とするもの。

---

## Rule ID（ルールID）

Rule IDは、人間および機械的処理主体が一意にルールを識別・参照するための識別子である。

各ルールには以下の形式でIDを付与する。

```text
<Convention>-<Category>-<Number>
```

### Convention Identifier（Convention識別子）

| Convention | 識別子 |
| --- | --- |
| Markdown | MD |
| Writing | WR |
| Naming | NM |
| Git | GT |

CategoryおよびNumberの採番方法は各Convention文書で定義する。本書ではRule ID構造のみを管理する。

---

## Convention Responsibilities（各Conventionの責務）

各Convention文書の責務を以下に定義する。固有のルールは各Convention文書で扱い、本書では責務の定義のみを行う。

### Markdown Convention（Markdown規約）

Markdown記法およびMarkdownによる表現方法を定義する。

実装: `markdown.md`

### Writing Convention（文章規約）

文章表現・言語表記・用語・文体を定義する。

実装: `writing.md`

### Naming Convention（命名規約）

ファイル名・ディレクトリ名・ドキュメント名・ブランチ名・ADR番号などの命名規則を定義する。

実装: `naming.md`

### Future Conventions（将来のConvention）

必要に応じてGit・Branch・Commit・Pull Request・Issue・Labelなどに関するConventionを追加できる。追加時は既存Conventionへ統合できないことを確認した上で設計する。

---

## Design Principles（設計原則）

### Consolidate Common Items in README（共通事項はREADMEへ集約する）

各Convention文書に共通事項を重複して記述しない。共通事項の変更は本書のみへ反映し、各Convention文書への重複を防ぐ。

### Individual Conventions Do Not Redefine README（個別ConventionはREADMEを再定義しない）

Requirement Levels・Rule Components・Rule Sourcesは本書で一元管理する。各Convention文書はこれらを再定義・再掲載せず、必要な場合は本書を参照する。Single Source of Truthの原則をConventions層にも適用する。

### Separate by Responsibility（責務によって分離する）

各Conventionは責務によって分離し、互いの責務を侵食しない。同一のルールが複数のConventionに属するように見える場合は、責務の境界を見直す。

### Write for Human and Machine Reference（人間・機械的処理主体の双方が参照できる形式で記述する）

ルールは、人間が読んで理解できるだけでなく、機械的処理主体が参照・適用できる明確な形式で記述する。曖昧な表現を避け、判断基準を明示する。

### Maintain Consistency with Upper Design（上位設計との一貫性を保つ）

Conventionsは、Philosophy・Architectureで定義された思想・構造を運用へ落とし込む層である。上位設計と矛盾するルールを定義しない。ルールの根拠は常にRule Sourcesとして明示する。

本書は、すべてのConvention文書の設計判断の出発点である。
