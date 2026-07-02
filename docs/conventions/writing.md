# Writing Convention（文章規約）

## Purpose（目的）

本書は、このプロジェクトにおける文章表現・言語表記・用語利用の運用ルールを定義する。

文章を上手く書く方法を解説する文書ではなく、このプロジェクトでどのような文章表現を採用するかを定義する運用規約である。一貫性・可読性・保守性・機械可読性を実現するための文章ルールを定義することを目的とする。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、このリポジトリで管理するすべての文書の文章表現に適用される。

対象は文章表現のみとし、以下は対象外とする。

- Markdown記法・見出し・コードブロック・リンク・表 → Markdown Convention
- ファイル名・ディレクトリ名・Rule ID・ブランチ名 → Naming Convention
- 正式用語一覧・用語定義・翻訳一覧 → Glossary（将来）

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Markdown Conventionとの境界

Markdown記法・見出し・コードブロック・リンク・表などの表現方法はMarkdown Conventionが管理する。本書はそのMarkdown上でどのような文章を書くかを定義する。

### Naming Conventionとの境界

ファイル名・ディレクトリ名・Rule ID・ブランチ名などの命名規則はNaming Conventionが管理する。本書は人間が読む文章表現のみを対象とする。

### Glossaryとの境界（将来）

正式な用語一覧・定義・訳語はGlossaryで管理する。本書では「用語を統一して使用する」という原則のみを定義し、具体的な用語一覧は扱わない。

---

## Design Principles（設計原則）

### Information First（情報優先）

文章は装飾ではなく情報を伝えるために記述する。表現より情報の正確性を優先する。

### Clarity over Elegance（優雅さより明確さ）

美しい文章よりも、誤解のない文章を優先する。

### Consistency over Style（文体より一貫性）

文体や表現技法よりも、一貫性を優先する。同一文書・同一リポジトリでは文体・表記・用語を統一する。

### Explicit over Implicit（暗黙より明示）

暗黙の前提や推測に頼らず、必要な情報は明示する。曖昧な指示語や省略を避ける。

### Human and Machine Readability（人間と機械の可読性）

文章は、人間だけでなく機械的処理主体も解釈できる形で記述する。自然言語として読みやすく、同時に解析しやすい文章を目指す。

### Reader First（読者優先）

文章表現は執筆者ではなく読者を基準に決定する。主言語・補助言語・専門用語の補足は、対象読者が理解しやすいことを優先する。

---

## Rule Groups と Rule ID Categories

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Language | LG | 使用言語・日英併記・英語表記に関するルール |
| Terminology | TM | 用語利用に関する原則 |
| Writing Style | WS | 文章表現・文体に関するルール |
| Sentence Structure | SS | 文章構造に関するルール |
| Project Writing | PW | プロジェクト固有の文章表現ルール |

Rule IDはREADMEで定義された `WR-<Category>-<Number>` 形式に従う。

---

## Language（言語）

### WR-LG-001: Primary Language

| 項目 | 内容 |
| --- | --- |
| Rule | 文書の主言語は対象読者に応じて選択する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

主言語は情報の正確な理解と伝達を最優先として決定する。このリポジトリでは主要利用者が日本語話者であるため、日本語を主言語として採用する。

---

### WR-LG-002: English Terms

| 項目 | 内容 |
| --- | --- |
| Rule | 技術用語・固有名詞・概念名は英語表記を優先する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

翻訳による意味のずれを防ぎ、外部仕様・ツール・ドキュメントとの一貫性を保つため。

**Examples:**

```text
良い例: Repository Philosophy、Markdown Convention、Pull Request
避ける例: リポジトリ哲学、マークダウン規約、プルリクエスト
```

**Notes:**

日本語での補足説明が必要な場合は、英語表記の後に括弧書きで補足する。

---

### WR-LG-003: Bilingual Headings

| 項目 | 内容 |
| --- | --- |
| Rule | 見出しは英語識別子と日本語説明を併記する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

英語は機械的処理主体による識別に、日本語は人間による理解に資するため、双方を満たす表記を採用する。

**Examples:**

```text
## Purpose（目的）
## Scope（適用範囲）
## Design Principles（設計原則）
```

---

### WR-LG-004: Abbreviations

| 項目 | 内容 |
| --- | --- |
| Rule | 略語は初出時にフルスペルを明記する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

略語の意味を読者が推測する必要をなくし、文書の自己完結性を高めるため。

**Examples:**

```text
良い例: Single Source of Truth（SSOT）。以降はSSOTと表記する。
避ける例: SSOTを維持する。（初出で説明なし）
```

---

## Terminology（用語）

### WR-TM-001: Consistent Terminology

| 項目 | 内容 |
| --- | --- |
| Rule | 同一概念には同一用語を使用する |
| Requirement | MUST |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

同一概念に複数の用語が混在すると、読者および機械的処理主体が別概念として解釈するリスクが生じるため。

**Examples:**

```text
良い例: 「責務」で統一する
避ける例: 「責務」「役割」「担当」を混在させる
```

---

### WR-TM-002: Glossary Reference

| 項目 | 内容 |
| --- | --- |
| Rule | Glossaryで定義された用語はGlossaryの定義に従って使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

用語の定義をSSOTで管理し、文書間の一貫性を保つため。

**Notes:**

Glossaryが未整備の期間は、各文書内で初出時に定義を明示することで代替する。

---

## Writing Style（文体）

### WR-WS-001: Writing Form

| 項目 | 内容 |
| --- | --- |
| Rule | 文末は「である調」に統一する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

「です・ます調」と「である調」の混在は文書全体の一貫性を損なうため。設計文書としての客観性を保つため「である調」を採用する。

**Examples:**

```text
良い例: 本書は運用ルールを定義する。
避ける例: 本書は運用ルールを定義します。
```

---

### WR-WS-002: Imperative Rule Statements

| 項目 | 内容 |
| --- | --- |
| Rule | Rule Headerのルール本文は命令文で記述する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

ルールとして何をすべきかを明確に伝えるため。説明文ではなく命令文とすることで、ルールの意図が一読で伝わる。

**Examples:**

```text
良い例: 文書の先頭にH1をタイトルとして配置する
避ける例: H1はタイトルとして使われるものです
```

---

### WR-WS-003: Active Voice

| 項目 | 内容 |
| --- | --- |
| Rule | 能動態を優先する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

能動態は主語・動詞・目的語の関係が明確であり、機械的処理主体による解析精度を高めるため。

**Examples:**

```text
良い例: Architectureは責務を定義する。
避ける例: 責務はArchitectureによって定義される。
```

---

## Sentence Structure（文章構造）

### WR-SS-001: One Sentence One Idea

| 項目 | 内容 |
| --- | --- |
| Rule | 一文に一つの意味を持たせる |
| Requirement | SHOULD |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

一文に複数の意味が含まれると、読者および機械的処理主体が意図を誤って解釈するリスクが高まるため。

**Examples:**

```text
良い例:
責務を先に定義する。
構造は責務の結果として決定する。

避ける例:
責務を先に定義し、その結果として構造を決定するが、例外もある。
```

---

### WR-SS-002: Avoid Ambiguous References

| 項目 | 内容 |
| --- | --- |
| Rule | 曖昧な指示語・代名詞を避け、対象を明示する |
| Requirement | SHOULD |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

「これ」「それ」「あれ」などの指示語は、文脈によって参照先が変わるため、機械的処理主体による解析を妨げる。

**Examples:**

```text
良い例: Markdown Conventionは記法を定義する。
避ける例: これは記法を定義する。
```

---

### WR-SS-003: Explicit List Usage

| 項目 | 内容 |
| --- | --- |
| Rule | 3つ以上の項目を列挙する場合は箇条書きを使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

文中での列挙は読みにくく、項目数が増えると解析も困難になるため。箇条書きにすることで構造が明確になる。

**Examples:**

```text
良い例:
対象は以下を含む。
- Philosophy
- Architecture
- Conventions

避ける例:
対象はPhilosophy、Architecture、Conventionsを含む。
```

---

## Project Writing（プロジェクト文章表現）

### WR-PW-001: Purpose Section

| 項目 | 内容 |
| --- | --- |
| Rule | Purposeセクションは「この文書が何を定義するか」を最初の一文で示す |
| Requirement | MUST |
| Source | Documentation Architecture, Project Conventions |

**Reason:**

読者が文書の目的を冒頭で把握できるようにするため。Purposeは文書全体の出発点であり、最初の一文で方向性を示す必要がある。

**Examples:**

```text
良い例: 本書は、このプロジェクトにおける〇〇の運用ルールを定義する。
避ける例: 〇〇についてさまざまな観点から説明する。
```

---

### WR-PW-002: Scope Section

| 項目 | 内容 |
| --- | --- |
| Rule | Scopeセクションは適用対象と対象外を明示する |
| Requirement | MUST |
| Source | Documentation Architecture, Project Conventions |

**Reason:**

文書の適用範囲が不明確だと、読者が誤った文書を参照するリスクがあるため。対象外の明示は、他のConvention・Architectureとの責務境界を保つために必要である。

---

### WR-PW-003: Rule Header Writing

| 項目 | 内容 |
| --- | --- |
| Rule | Rule HeaderのRule欄は簡潔な命令文で記述する。一文に収める |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Rule HeaderはHeaderだけで概要を把握できる構造データである。詳細な説明はBodyのReasonに委ねるため、Ruleは簡潔に保つ。

---

### WR-PW-004: Reason Writing

| 項目 | 内容 |
| --- | --- |
| Rule | ReasonはなぜそのRuleが必要かを説明する。実装方法・手順は含めない |
| Requirement | MUST |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

Reasonは「Why」を提供する領域であり、「How」はRule本文またはExamplesに委ねる。Why/Howが混在すると、Ruleの根拠が不明確になる。

---

## Review Checklist（レビューチェックリスト）

以下のチェックリストを使用して、文章表現の品質を確認する。セルフレビューおよび機械的処理主体による品質確認の両方に利用できる。

### Language の確認

- [ ] 主言語は対象読者に適した言語を選択しているか
- [ ] 技術用語・固有名詞は英語表記を使用しているか
- [ ] 見出しは英語識別子と日本語説明を併記しているか
- [ ] 略語は初出時にフルスペルを明記しているか

### Terminology の確認

- [ ] 同一概念に同一用語を使用しているか
- [ ] Glossaryで定義された用語はGlossaryの定義に従っているか

### Writing Style の確認

- [ ] 文末が「である調」に統一されているか
- [ ] Rule Headerのルール本文は命令文か
- [ ] 能動態を優先しているか

### Sentence Structure の確認

- [ ] 一文に一つの意味を持たせているか
- [ ] 曖昧な指示語・代名詞を使用していないか
- [ ] 3つ以上の列挙に箇条書きを使用しているか

### Project Writing の確認

- [ ] Purposeセクションの最初の一文で文書の目的を示しているか
- [ ] Scopeセクションで適用対象と対象外を明示しているか
- [ ] Rule HeaderのRule欄は一文の命令文か
- [ ] ReasonはWhyのみを説明しているか
