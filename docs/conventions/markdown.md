# Markdown Convention（Markdown規約）

## Purpose（目的）

本書は、このプロジェクトにおけるMarkdownの利用方針・表現ルール・運用原則を定義する。

Markdownで何ができるかを説明する文書ではなく、このプロジェクトでMarkdownをどのように使用するかを定義する運用規約である。一貫性・可読性・保守性を実現するための利用ルールを定義することを目的とする。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、このリポジトリで管理するすべてのMarkdownファイルに適用される。

対象はMarkdownによる表現方法のみとし、以下は対象外とする。

- 文体・用語・文章表現 → Writing Convention
- ファイル名・ディレクトリ名 → Naming Convention

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Writing Conventionとの境界

Writing Conventionは文体・用語・文章表現を扱う。本書はそれらをMarkdownでどのように表現するかのみを定義し、文章内容・言語表記・用語の選択は扱わない。

### Naming Conventionとの境界

Naming Conventionはファイル名・ディレクトリ名・ブランチ名などの命名規則を扱う。本書はMarkdown内でのリンク記法や参照形式を定義するが、参照先の名称そのものは扱わない。

---

## Design Principles（設計原則）

### Information First（情報優先）

Markdownは情報を表現する手段である。Markdownの表現よりも情報構造を優先する。

### Readability over Compactness（簡潔さより読みやすさ）

短く書くことよりも読みやすさを優先する。

### Consistency over Preference（好みより一貫性）

個人の好みではなく、プロジェクト全体の一貫性を優先する。

### Standard First（標準記法優先）

CommonMarkおよびGitHub Flavored Markdownで表現できる場合は、標準記法を優先する。独自記法は必要最小限とする。

### HTML as Last Resort（HTML最終手段）

Markdownで表現可能な場合はHTMLを使用しない。HTMLはMarkdownで表現できない場合のみ使用する。

### Automation Friendly（自動化への配慮）

Markdownは、人間だけでなく機械的処理主体による解析・変換・レビューを考慮して記述する。曖昧な構造・省略・慣習的表記は、機械的処理での誤解釈を招く。明確な記法と一貫した構造を維持することで、人間と機械的処理主体の双方にとって信頼性の高い文書になる。

---

## Rule Groups と Rule ID Categories

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Document Structure | DS | 文書全体を構成するルール |
| Content Organization | CO | 内容を整理するルール |
| Code Representation | CR | コード・設定情報を表現するルール |
| References | RF | 参照情報を表現するルール |
| Project Style | PS | プロジェクト固有の表現ルール |

Rule IDはREADMEで定義された `MD-<Category>-<Number>` 形式に従う。

---

## Document Structure（文書構造）

### MD-DS-001: Document Title

| 項目 | 内容 |
| --- | --- |
| Rule | 文書の先頭にH1(`#`)をタイトルとして配置する |
| Requirement | MUST |
| Source | Documentation Architecture, Project Conventions |

**Reason:**

文書の識別および機械的処理での参照を一意にするため。

---

### MD-DS-002: Heading Hierarchy

| 項目 | 内容 |
| --- | --- |
| Rule | 見出しレベルを順序通りに使用する。レベルを飛ばしてはならない |
| Requirement | MUST |
| Source | CommonMark, markdownlint (MD001) |

**Reason:**

構造の一貫性と機械的処理での解析精度を保つため。

**Examples:**

```text
# H1
## H2
### H3   ← 許可

# H1
### H3   ← 不可（H2をスキップ）
```

---

### MD-DS-003: Single H1

| 項目 | 内容 |
| --- | --- |
| Rule | H1は文書内に1つのみ使用する |
| Requirement | MUST |
| Source | markdownlint (MD025), Project Conventions |

**Reason:**

文書タイトルの一意性を保ち、機械的処理での文書識別を明確にするため。

---

### MD-DS-004: Section Separation

| 項目 | 内容 |
| --- | --- |
| Rule | 主要セクションの区切りに水平線(`---`)を使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

セクション境界を視覚的・構造的に明確にするため。

---

### MD-DS-005: Heading Spacing

| 項目 | 内容 |
| --- | --- |
| Rule | 見出しの前後に1行の空白行を置く |
| Requirement | MUST |
| Source | markdownlint (MD022) |

**Reason:**

視認性の向上と、レンダリング環境による差異を防ぐため。

---

### MD-DS-006: Unique Headings

| 項目 | 内容 |
| --- | --- |
| Rule | 同一文書内で同じ見出し名を重複して使用しない |
| Requirement | SHOULD |
| Source | markdownlint (MD024), Project Conventions |

**Reason:**

GitHubアンカーの重複を防ぎ、アウトラインの可読性と機械的処理での参照精度を維持するため。

**Notes:**

同じ語を使う必要がある場合は、文脈が分かるように見出し名を具体化する。

---

### MD-DS-007: No Emphasis as Heading

| 項目 | 内容 |
| --- | --- |
| Rule | 強調記法を見出しの代わりとして使用しない |
| Requirement | MUST NOT |
| Source | markdownlint (MD036), Project Conventions |

**Reason:**

Markdownのアウトライン構造を維持し、人間・機械的処理主体が文書構造を正しく解釈できるようにするため。

**Examples:**

```text
### Notes          ← 良い例
**Notes:**         ← 避ける例（見出しの代わりに強調を使用）
```

**Notes:**

局所的な補助ラベルとしてのDocument Labelsとは区別する。

---

## Content Organization（内容整理）

### MD-CO-001: Unordered Lists

| 項目 | 内容 |
| --- | --- |
| Rule | 順序に意味がない列挙には箇条書き(`-`)を使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

順序の有無を明示し、情報の関係性を正確に伝えるため。

**Notes:**

リストマーカーは `-` に統一する。

---

### MD-CO-002: Ordered Lists

| 項目 | 内容 |
| --- | --- |
| Rule | 順序に意味がある列挙には番号付きリスト(`1.`)を使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

手順・優先順位など、順序が意味を持つ場合に誤解を防ぐため。

---

### MD-CO-003: List Nesting

| 項目 | 内容 |
| --- | --- |
| Rule | リストのネストは2階層までとする |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

深いネストは可読性を損ない、情報構造の再設計が必要なことを示すため。

**Notes:**

3階層以上が必要な場合はセクション分割を検討する。

---

### MD-CO-004: Tables

| 項目 | 内容 |
| --- | --- |
| Rule | 構造化された比較・対応関係の表現にはテーブルを使用する |
| Requirement | SHOULD |
| Source | GitHub Flavored Markdown |

**Reason:**

対応関係を視覚的に明確にし、機械的処理での参照を容易にするため。

---

### MD-CO-005: Blockquotes

| 項目 | 内容 |
| --- | --- |
| Rule | 外部からの引用には引用ブロック(`>`)を使用する |
| Requirement | SHOULD |
| Source | CommonMark |

**Reason:**

引用元との区別を明確にし、著作権上の明示義務を果たすため。

**Notes:**

強調や注意書きへの装飾目的での使用は避ける。

---

### MD-CO-006: Blank Lines Around Lists

| 項目 | 内容 |
| --- | --- |
| Rule | リストの前後には1行の空白行を置く |
| Requirement | MUST |
| Source | markdownlint (MD032) |

**Reason:**

リストと前後の文章が空白行なく連続すると、Markdownレンダラーによってはリストとして認識されない場合がある。空白行で区切ることで、レンダリング環境による差異を防ぐ。

**Examples:**

```text
良い例:
本文の説明。

- 項目1
- 項目2

次の本文。

避ける例:
本文の説明。
- 項目1
- 項目2
次の本文。
```

---

## Code Representation（コード表現）

### MD-CR-001: Fenced Code Blocks

| 項目 | 内容 |
| --- | --- |
| Rule | コードブロックにはフェンス形式(` ``` `)を使用する |
| Requirement | MUST |
| Source | CommonMark, Documentation Philosophy, Project Conventions |

**Reason:**

インデント形式より視覚的に明確であり、言語指定が可能なため。

---

### MD-CR-002: Language Identifier

| 項目 | 内容 |
| --- | --- |
| Rule | コードブロックには言語識別子を指定する |
| Requirement | MUST |
| Source | markdownlint (MD040), Documentation Philosophy, Project Conventions |

**Reason:**

シンタックスハイライトを有効にし、機械的処理での言語判定精度を高めるため。

**Examples:**

````text
```bash
git status
```

```yaml
name: CI
```

```text
言語が特定できない場合
```
````

**Notes:**

言語が特定できない場合は `text` を使用する。

---

### MD-CR-003: Inline Code

| 項目 | 内容 |
| --- | --- |
| Rule | ファイル名・コマンド・変数・設定値などの技術的な文字列にはインラインコード(`` ` ``)を使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

通常テキストと技術的な文字列を明確に区別するため。

**Examples:**

`README.md`、`git commit`、`true`

---

## References（参照）

### MD-RF-001: Link Text

| 項目 | 内容 |
| --- | --- |
| Rule | リンクテキストはリンク先の内容を説明する文言にする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

リンクテキストのみで参照先を判断できるようにするため。

**Examples:**

```text
良い例: [Repository Philosophy](../philosophy/repository.md)
避ける例: [こちら](../philosophy/repository.md)
```

---

### MD-RF-002: Internal Links

| 項目 | 内容 |
| --- | --- |
| Rule | リポジトリ内のファイルへの参照には相対パスを使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

リポジトリ移動・フォーク時にリンクの有効性を維持するため。

---

### MD-RF-003: Image Alt Text

| 項目 | 内容 |
| --- | --- |
| Rule | 画像にはalt属性を記述する |
| Requirement | MUST |
| Source | CommonMark, Project Conventions |

**Reason:**

画像を表示できない環境や機械的処理での内容把握を可能にするため。

---

## Project Style（プロジェクトスタイル）

### MD-PS-001: Blank Lines Between Sections

| 項目 | 内容 |
| --- | --- |
| Rule | セクション間には1行の空白行を置く |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

セクション境界を明確にし、視認性を高めるため。

---

### MD-PS-002: No Trailing Spaces

| 項目 | 内容 |
| --- | --- |
| Rule | 行末にスペースを残さない |
| Requirement | MUST |
| Source | markdownlint (MD009) |

**Reason:**

意図しない改行の発生を防ぎ、差分管理を容易にするため。

---

### MD-PS-003: No HTML

| 項目 | 内容 |
| --- | --- |
| Rule | Markdownで表現可能な場合はHTMLを使用しない |
| Requirement | MUST NOT |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

Markdownの可搬性・可読性・機械的処理互換性を維持するため。

**Exceptions:**

Markdownでは表現できない要素（折りたたみ `<details>` 等）を使用する場合。

---

### MD-PS-004: Line Length

| 項目 | 内容 |
| --- | --- |
| Rule | 1行の文字数に上限を設けない |
| Requirement | MAY |
| Source | Project Conventions |

**Reason:**

日本語を含む文書では折り返し位置の管理が複雑になるため、エディタの折り返し表示に委ねる。

---

### MD-PS-005: File Encoding

| 項目 | 内容 |
| --- | --- |
| Rule | ファイルエンコーディングはUTF-8(BOMなし)を使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

多言語対応と機械的処理での互換性を確保するため。

---

## Review Checklist（レビューチェックリスト）

以下のチェックリストを使用して、Markdownファイルの品質を確認する。セルフレビューおよび機械的処理主体による品質確認の両方に利用できる。

### Document Structure の確認

- [ ] H1が文書の先頭に1つだけ配置されているか
- [ ] 見出しレベルが順序通りに使用されているか（スキップなし）
- [ ] 見出しの前後に空白行が置かれているか
- [ ] 同一文書内で見出し名が不必要に重複していないか
- [ ] 強調記法を見出しの代わりに使用していないか

### Content Organization の確認

- [ ] 順序のない列挙に箇条書き(`-`)を使用しているか
- [ ] 順序のある列挙に番号付きリストを使用しているか
- [ ] リストのネストが2階層以内か
- [ ] リストの前後に空白行が置かれているか

### Code Representation の確認

- [ ] コードブロックにフェンス形式を使用しているか
- [ ] すべてのコードブロックに言語識別子が指定されているか
- [ ] 技術的な文字列にインラインコードを使用しているか

### References の確認

- [ ] リンクテキストがリンク先の内容を説明しているか
- [ ] 内部リンクに相対パスを使用しているか
- [ ] 画像にalt属性が記述されているか

### Project Style の確認

- [ ] 行末にスペースがないか
- [ ] Markdownで表現できる要素にHTMLを使用していないか
- [ ] ファイルエンコーディングがUTF-8(BOMなし)か

---

## Appendix: External Rule Mapping（外部ルール対応表）

Markdown Convention と外部ツールルールの対応関係を示す。

| Project Rule | External Rule |
| --- | --- |
| MD-DS-002 | markdownlint (MD001) |
| MD-DS-003 | markdownlint (MD025) |
| MD-DS-005 | markdownlint (MD022) |
| MD-DS-006 | markdownlint (MD024) |
| MD-DS-007 | markdownlint (MD036) |
| MD-CO-006 | markdownlint (MD032) |
| MD-CR-002 | markdownlint (MD040) |
| MD-PS-002 | markdownlint (MD009) |
