# Naming Convention（命名規約）

## Purpose（目的）

本書は、このプロジェクトにおける命名規則を定義する。

名前を付ける技法を解説する文書ではなく、このプロジェクトでどのような命名規則を採用するかを定義する運用規約である。一貫性・可読性・検索性・保守性・機械可読性を実現するための命名ルールを定義することを目的とする。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、このリポジトリで管理するすべての識別子・ファイル名・ディレクトリ名・文書名に適用される。

対象は命名規則のみとし、以下は対象外とする。

- Markdown記法・見出し・リンク → Markdown Convention
- 文章表現・用語利用・日英表記 → Writing Convention
- 用語一覧・用語定義 → Glossary（将来）
- ディレクトリ構造・責務設計 → Repository Architecture
- プログラミング言語固有の命名規則（変数名・関数名・クラス名）

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Markdown Conventionとの境界

Markdown記法・見出し・リンク・表などの表現方法はMarkdown Conventionが管理する。本書はそれらで使用する名前・識別子のみを対象とする。

### Writing Conventionとの境界

文章表現・文体・用語利用・日英表記など、人間が読む文章に関するルールはWriting Conventionが管理する。本書は識別子・ファイル名・ディレクトリ名などの命名規則のみを定義する。

### Glossaryとの境界（将来）

正式な用語一覧・定義・訳語はGlossaryで管理する。本書はその用語をどのような命名へ適用するかのみを扱う。

---

## Design Principles（設計原則）

### Consistency over Preference（好みより一貫性）

個人の好みよりも、一貫した命名規則を優先する。

### Descriptive over Clever（巧みさより明確さ）

印象的な名前よりも、責務が理解できる名前を優先する。

### Stable over Temporary（一時性より安定性）

一時的な状態や実装都合ではなく、長期的に意味が変わりにくい名前を採用する。

### Human and Machine Readability（人間と機械の可読性）

命名は、人間が理解しやすく、同時に機械的処理主体が解析しやすいことを両立する。

### Responsibility First（責務優先）

名前は実装ではなく責務を表現する。構造変更に影響されにくい命名を優先する。

---

## Rule Groups と Rule ID Categories

| Rule Group | Category | 対象 |
| --- | --- | --- |
| File Naming | FN | ファイル名の命名規則 |
| Directory Naming | DN | ディレクトリ名の命名規則 |
| Document Naming | DC | 文書タイトル・表示名の命名規則 |
| Identifier Naming | ID | Rule ID・ADR番号などの識別子 |
| GitHub Naming | GH | GitHub上で使用する識別名 |

Rule IDはREADMEで定義された `NM-<Category>-<Number>` 形式に従う。

---

## File Naming（ファイル命名）

### NM-FN-001: Lowercase File Names

| 項目 | 内容 |
| --- | --- |
| Rule | ファイル名は小文字を使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

大文字・小文字の混在はOSやツールによる大文字小文字の扱いの差異によって、参照エラーや重複を引き起こすリスクがあるため。

**Examples:**

```text
良い例: repository.md、markdown.md
避ける例: Repository.md、MarkdownConvention.md
```

**Notes:**

GitHubが定める標準ファイル（`README.md`・`CONTRIBUTING.md`・`SECURITY.md` 等）はこのルールの例外とし、GitHub標準の命名に従う。

---

### NM-FN-002: Kebab Case

| 項目 | 内容 |
| --- | --- |
| Rule | 複数単語を含むファイル名の区切りにはハイフン(`-`)を使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

スペースはURLエンコードが必要になり、アンダースコアは視認性が低く、キャメルケースは大文字小文字の混在を招く。ハイフン区切り（kebab-case）は可読性・機械可読性・URL安全性を同時に満たす。

**Examples:**

```text
良い例: getting-started.md、pull-request-template.md
避ける例: gettingStarted.md、getting_started.md
```

---

### NM-FN-003: Meaningful File Names

| 項目 | 内容 |
| --- | --- |
| Rule | ファイル名はそのファイルの責務を表す名前にする |
| Requirement | MUST |
| Source | Repository Architecture, Project Conventions |

**Reason:**

ファイル名はディレクトリとともに責務を表現する手段である。責務が読み取れない名前は、検索性・保守性を損なう。

**Examples:**

```text
良い例: repository.md（リポジトリに関する文書）、markdown.md（Markdown規約）
避ける例: doc1.md、new-file.md、temp.md
```

---

### NM-FN-004: Stable File Names

| 項目 | 内容 |
| --- | --- |
| Rule | 実装の都合や一時的な状態を名前に含めない |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

実装都合に依存した名前は、変更のたびにリンク・参照の修正が必要になり保守コストを増大させる。名前は責務に基づいて付け、長期的に安定させる。

**Examples:**

```text
良い例: architecture.md
避ける例: architecture-v2.md、architecture-new.md、architecture-wip.md
```

---

## Directory Naming（ディレクトリ命名）

### NM-DN-001: Lowercase Directory Names

| 項目 | 内容 |
| --- | --- |
| Rule | ディレクトリ名は小文字を使用する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

NM-FN-001と同じ理由による。ファイル名とディレクトリ名の命名規則を統一することで、パス全体の一貫性を保つ。

**Examples:**

```text
良い例: docs/、philosophy/、conventions/
避ける例: Docs/、Philosophy/、Conventions/
```

---

### NM-DN-002: Responsibility-Based Directory Names

| 項目 | 内容 |
| --- | --- |
| Rule | ディレクトリ名は管理する情報の責務を表す名前にする |
| Requirement | MUST |
| Source | Repository Architecture, Documentation Architecture, Project Conventions |

**Reason:**

ディレクトリは責務領域を表現する手段である。ディレクトリ名が責務を示すことで、ファイルを配置する前に適切な場所を判断できる。

**Examples:**

```text
良い例: philosophy/（思想を管理）、conventions/（規約を管理）
避ける例: misc/、other/、stuff/
```

---

### NM-DN-003: Stable Directory Names

| 項目 | 内容 |
| --- | --- |
| Rule | ディレクトリ名は長期的に安定した責務名を使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

ディレクトリ名の変更は、配下の全ファイルの参照パスに影響する。責務が変わらない限りディレクトリ名を変えない設計を採用する。

---

## Document Naming（文書命名）

### NM-DC-001: English Base Title

| 項目 | 内容 |
| --- | --- |
| Rule | 文書タイトル（H1）は英語を基本とする |
| Requirement | SHOULD |
| Source | Writing Convention, Project Conventions |

**Reason:**

英語タイトルは機械的処理主体による識別・検索・参照に適している。日本語補足が必要な場合はWR-LG-003に従い括弧書きで付記する。

**Examples:**

```text
良い例: # Repository Philosophy
良い例（補足あり）: # Repository Philosophy（リポジトリ哲学）
避ける例: # リポジトリ哲学
```

---

### NM-DC-002: Title Matches File Responsibility

| 項目 | 内容 |
| --- | --- |
| Rule | 文書タイトルはファイルの責務と一致させる |
| Requirement | MUST |
| Source | Documentation Architecture, Project Conventions |

**Reason:**

ファイル名・ディレクトリ・文書タイトルが一致して初めて、名前だけで内容を判断できる。不一致は混乱と検索ミスを招く。

**Examples:**

```text
良い例: docs/philosophy/repository.md → # Repository Philosophy
避ける例: docs/philosophy/repository.md → # GitHub運用について
```

---

## Identifier Naming（識別子命名）

### NM-ID-001: Rule ID Format

| 項目 | 内容 |
| --- | --- |
| Rule | Rule IDはConventions READMEで定義された `<Convention>-<Category>-<Number>` 形式に従う |
| Requirement | MUST |
| Source | Conventions README |

**Reason:**

Rule IDはルールを一意に識別・参照するための識別子である。形式を統一することで、人間および機械的処理主体が効率よくルールを参照できる。

**Examples:**

```text
良い例: MD-DS-001、WR-LG-001、NM-FN-001
避ける例: MD001、MarkdownRule1、rule-ds-001
```

---

### NM-ID-002: Sequential Rule Numbering

| 項目 | 内容 |
| --- | --- |
| Rule | Rule Numberは各CategoryごとにゼロパディングしてNumberは3桁で採番する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

3桁のゼロパディングにより、ソート順と視覚的な整列が一致し、機械的処理での数値比較も安定する。

**Examples:**

```text
良い例: MD-DS-001、MD-DS-002、MD-DS-010
避ける例: MD-DS-1、MD-DS-2、MD-DS-10
```

---

### NM-ID-003: Stable Rule IDs

| 項目 | 内容 |
| --- | --- |
| Rule | 一度付与したRule IDは変更しない |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Rule IDは文書間の参照・チェックリスト・外部ツール設定などで使用される。IDの変更はすべての参照箇所の更新を必要とし、保守コストを増大させる。

**Notes:**

ルールを廃止する場合はIDを削除するのではなく、廃止済みとしてマークしIDを欠番として扱う。

---

### NM-ID-004: ADR Sequential Numbering

| 項目 | 内容 |
| --- | --- |
| Rule | ADR番号は4桁のゼロパディングで連番採番する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

連番により識別性と一貫性を維持する。番号の意味（作成順・論理構造順など）は、ADRの設計思想に従う。

**Examples:**

```text
良い例: adr/0001-adopt-markdown-convention.md、adr/0002-rule-id-format.md
避ける例: adr/markdown.md、adr/rule-id.md
```

---

## GitHub Naming（GitHub命名）

### NM-GH-001: Branch Name Format

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名はkebab-caseを使用し、作業の種類と対象を含める |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

ブランチ名は作業内容を一読で把握できる識別子として機能する。種類と対象を含めることで、複数のブランチが並存する状況でも混乱を防ぐ。

**Examples:**

```text
良い例: docs/add-markdown-convention、fix/rule-id-format、feat/adr-template
避ける例: my-branch、update、fix
```

**Notes:**

GitHub Namingは今後のGitHub運用設計に応じて拡張する。本書では命名原則のみを定義し、具体的なブランチ戦略はGit Conventionで扱う。

---

## Review Checklist（レビューチェックリスト）

以下のチェックリストを使用して、命名の品質を確認する。セルフレビューおよび機械的処理主体による品質確認の両方に利用できる。

### File Naming の確認

- [ ] ファイル名は小文字か
- [ ] 複数単語の区切りにハイフンを使用しているか
- [ ] ファイル名はそのファイルの責務を表しているか
- [ ] 実装都合や一時的な状態を名前に含んでいないか

### Directory Naming の確認

- [ ] ディレクトリ名は小文字か
- [ ] ディレクトリ名は管理する情報の責務を表しているか
- [ ] 長期的に安定した責務名を使用しているか

### Document Naming の確認

- [ ] 文書タイトルは英語を基本としているか
- [ ] 文書タイトルはファイルの責務と一致しているか

### Identifier Naming の確認

- [ ] Rule IDは `<Convention>-<Category>-<Number>` 形式に従っているか
- [ ] Rule Numberは3桁のゼロパディングで採番しているか
- [ ] 既存のRule IDを変更していないか
- [ ] ADR番号は4桁のゼロパディングで連番採番されているか

### GitHub Naming の確認

- [ ] ブランチ名はkebab-caseを使用しているか
- [ ] ブランチ名に作業の種類と対象が含まれているか
