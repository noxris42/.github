# Commit Convention（コミット規約）

## Purpose（目的）

本書は、このプロジェクトにおけるコミットメッセージの構造・記述方法・運用ルールを定義する。

コミットメッセージを書く技法を解説する文書ではなく、このプロジェクトで採用するコミットメッセージの運用規約を定義する文書である。Git履歴を長期的な設計資産として維持し、可読性・保守性・解析性・ツール互換性を実現することを目的とする。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、このリポジトリへのすべてのコミットメッセージに適用される。

対象はコミットメッセージの構造・内容のみとし、以下は対象外とする。

- 文章表現・文体・用語利用 → Writing Convention
- 識別子・名称の命名規則 → Naming Convention
- Git Flow・Branch Strategy・Release Flow → 将来のGit Convention
- Issue・Pull Request・Projects・Actions → 将来のGitHub Convention
- Changelog生成・Release Notes自動化

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Writing Conventionとの関係

文章表現・文体・用語利用はWriting Conventionが管理する。本書はコミットメッセージ固有の文章構造のみを定義し、文章表現の一般原則はWriting Conventionを参照する。

### Naming Conventionとの関係

Type・Scopeなどで使用する名称はNaming Conventionの命名原則に従う。本書では命名の具体的な規則は定義せず、コミットメッセージ内での使用方法のみを定義する。

### GitHub Convention（将来）との関係

Issue・Pull Request・Release・ProjectsなどGitHub運用全体は将来のGitHub Conventionで管理する。本書ではコミットメッセージとGitHub機能との接点（Refs・Closing Keywordsなど）のみを扱う。

---

## Design Principles（設計原則）

### Human and Machine Readability（人間と機械の可読性）

コミットメッセージは人間および機械的処理主体の双方が理解できることを優先する。

### Ensure Tool Compatibility（ツール互換性の確保）

Git・GitHub・CI・解析ツールが正しく解釈できる形式で記述する。ツールとの互換性を損なう構造は避ける。

### What / Why / Relationship（何・なぜ・関係）

Headerは変更内容（What）を表現する。Bodyは変更理由（Why）を表現する。Footerは関連情報（Relationship）を表現する。

### Repository Independence（リポジトリ独立性）

Commit ConventionはRepositoryに依存しない共通規約とする。Repository固有のLanguage・Type・Scopeのみ上書きを許可する。

---

## Rule Groups と Rule ID Categories（ルールグループと識別子）

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Message Structure | MS | コミットメッセージ全体の構造 |
| Language | LG | 使用言語 |
| Type & Gitmoji | TG | TypeおよびGitmojiの使用方法 |
| Scope | SC | Scopeの使用方法 |
| Subject | SB | Header Subjectの記述方法 |
| Body | BD | Bodyの記述方法 |
| Footer | FT | Footerの記述方法 |
| Tool Compatibility | TC | ツール互換性維持のためのルール |
| Repository Override | RO | Repositoryごとに上書き可能な項目 |

Rule IDはREADMEで定義された `CM-<Category>-<Number>` 形式に従う。

---

## Message Structure（メッセージ構造）

### CM-MS-001: Message Format（メッセージ形式）

| 項目 | 内容 |
| --- | --- |
| Rule | コミットメッセージはHeader・Body・Footerの三層で構成する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

三層構造によって変更内容（What）・変更理由（Why）・関連情報（Relationship）を明確に分離し、人間・機械的処理主体の双方が情報を正確に取得できるようにするため。

**Examples:**

```text
feat(auth): add OAuth2 login support

Implement OAuth2 authorization flow to support third-party
login providers. This replaces the legacy session-based
authentication approach.

Refs #42
```

---

### CM-MS-002: Section Separation（セクション区切り）

| 項目 | 内容 |
| --- | --- |
| Rule | Header・Body・Footerの各セクションは1行の空白行で区切る |
| Requirement | MUST |
| Source | Conventional Commits, Project Conventions |

**Reason:**

空白行による区切りはGit・GitHub・解析ツールがセクションを正確に判定するための標準的な方法であるため。

---

### CM-MS-003: Required Sections（必須セクション）

| 項目 | 内容 |
| --- | --- |
| Rule | Headerは必須とする。BodyおよびFooterは省略可能とする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

すべてのコミットに変更内容（What）を示すHeaderを必須とすることで、Git履歴の最低限の可読性を保証するため。

---

## Language（言語）

### CM-LG-001: Language Selection（言語選択）

| 項目 | 内容 |
| --- | --- |
| Rule | コミットメッセージの言語は対象読者およびRepository Profileに応じて選択する |
| Requirement | MUST |
| Source | Writing Convention (WR-LG-001), Project Conventions |

**Reason:**

コミット履歴の可読性は対象読者が理解できる言語で最大化されるため。言語の選択はWR-LG-001の原則に従い、Repository Overrideで明示する。

---

## Type & Gitmoji（タイプとGitmoji）

### CM-TG-001: Type Required（Type必須）

| 項目 | 内容 |
| --- | --- |
| Rule | HeaderにはTypeを必ず含める |
| Requirement | MUST |
| Source | Conventional Commits, Project Conventions |

**Reason:**

TypeはコミットメッセージをCHANGELOG生成・フィルタリング・解析ツールが分類するための主要な識別子であるため。

---

### CM-TG-002: Common Type Candidates（共通Type候補）

| 項目 | 内容 |
| --- | --- |
| Rule | 以下の共通Type候補からRepositoryで採用するTypeを選択して使用する |
| Requirement | SHOULD |
| Source | Conventional Commits, Project Conventions |

**Reason:**

Typeをプロジェクト全体で共通候補として定義することで、リポジトリをまたいだGit履歴の一貫性を保つ。各Repositoryは共通候補の中から採用するTypeを選択し、Repository Overrideとして明示する。

**Examples:**

| Gitmoji | Type | 用途 |
| :---: | --- | --- |
| ✨ | `feat` | 新機能 |
| 🐛 | `fix` | バグ修正・セキュリティ修正 |
| ⚡️ | `perf` | パフォーマンス改善 |
| 📦 | `build` | 依存関係・パッケージ・Dockerfile・デプロイ構成の変更 |
| ⏩ | `revert` | 変更の取り消し |
| 📝 | `docs` | ドキュメントのみの変更 |
| ♻️ | `refactor` | リファクタリング・コード削除 |
| 💄 | `style` | フォーマット・スタイル変更（動作に影響しない） |
| ✅ | `test` | テストの追加・修正 |
| 🔧 | `chore` | 設定・ツール・CI/CD・不要ファイル削除 |
| 👷 | `ci` | CI/CDの設定変更 |

**Notes:**

`build` と `chore` の判断基準: リリース成果物や依存関係に影響するなら `build`、それ以外の内部作業なら `chore`。

---

### CM-TG-003: Gitmoji Placement（Gitmoji配置）

| 項目 | 内容 |
| --- | --- |
| Rule | TypeにGitmojiを付与し、Typeの前に配置する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

GitmojiはTypeの視覚的な補助として機能し、Git履歴の一覧性と可読性を高める。標準で必須とすることで、Repositoryをまたいだコミット履歴の視覚的一貫性を保証する。

**Examples:**

```text
✨ feat(ui): add dark mode toggle
🐛 fix(auth): resolve token expiration handling
📝 docs: update README installation steps
```

**Notes:**

Gitmojiを任意または無効にしたい場合はRepository Overrideで明示する。

---

### CM-TG-004: Gitmoji-Type One-to-One（Gitmoji-Type 1対1対応）

| 項目 | 内容 |
| --- | --- |
| Rule | GitmojiとTypeは共通対応表に従い1対1で対応させる |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

GitmojiとTypeが1対1に対応することで、どちらか一方を見ただけでもう一方が判断できる。対応がズレると、視覚的な識別と解析ツールの分類が矛盾し、Git履歴の信頼性を損なうため。

**Examples:**

```text
良い例: ✨ feat / 🐛 fix / 📝 docs
避ける例: 📝 feat（docsのGitmojiをfeatに使用）
避ける例: ✨ docs（featのGitmojiをdocsに使用）
```

---

## Scope（スコープ）

### CM-SC-001: Scope Optional（Scope任意）

| 項目 | 内容 |
| --- | --- |
| Rule | Scopeは任意とする |
| Requirement | MAY |
| Source | Conventional Commits, Project Conventions |

**Reason:**

Scopeは変更の影響範囲を示す補助情報であり、小規模なリポジトリや単一責務のコミットでは省略できる柔軟性を持たせるため。

---

### CM-SC-002: Scope Format（Scope形式）

| 項目 | 内容 |
| --- | --- |
| Rule | Scopeは小文字のkebab-caseで記述し、丸括弧で囲む |
| Requirement | MUST |
| Source | Naming Convention (NM-FN-002), Project Conventions |

**Reason:**

Scopeの形式を統一することで、ツールによる解析精度とGit履歴の一貫性を維持するため。

**Examples:**

```text
feat(user-auth): ...
fix(api-client): ...
docs(getting-started): ...
```

---

### CM-SC-003: Scope Definition（Scope定義）

| 項目 | 内容 |
| --- | --- |
| Rule | 使用するScope一覧はRepositoryごとに定義する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

Scopeの意味はRepositoryの構造に依存するため、共通Conventionでは形式のみを定義し、値はRepository側で管理するのが適切であるため。

---

## Subject（サブジェクト）

### CM-SB-001: Subject Required（Subject必須）

| 項目 | 内容 |
| --- | --- |
| Rule | Subjectは必須とする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

SubjectはHeaderの核であり、変更内容（What）を示す最低限の情報を提供するため。

---

### CM-SB-002: Subject Content（Subjectの内容）

| 項目 | 内容 |
| --- | --- |
| Rule | Subjectは変更内容（What）を簡潔に表現する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

変更理由（Why）はBodyで説明するため、Subjectに詰め込まない。Subjectが変更内容に集中することでGit履歴の一覧性が高まるため。

**Examples:**

```text
良い例: add OAuth2 login support
避ける例: add OAuth2 login support because the old session auth was slow
```

---

### CM-SB-003: Subject Length（Subject長さ）

| 項目 | 内容 |
| --- | --- |
| Rule | Subjectは一般的なツールの一覧表示で省略されない長さに収める |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

GitHubのコミット一覧・ターミナル・各種ツールでSubjectが省略されずに表示される長さは環境に依存するが、英語で72文字・日本語で36文字程度が目安となる。言語によって表示幅が異なるため、文字数より「省略されないこと」を基準とする。

---

### CM-SB-004: Subject Imperative（Subject命令形）

| 項目 | 内容 |
| --- | --- |
| Rule | 英語で記述する場合、Subjectは動詞の原形（命令形）で始める |
| Requirement | SHOULD |
| Source | Writing Convention (WR-WS-002), Project Conventions |

**Reason:**

Gitのauto-generated commit message（merge commit等）が命令形を使用するため、一貫性を保つ。また命令形は変更を「行動」として表現し、変更の意図が伝わりやすい。

**Examples:**

```text
良い例: add feature, fix bug, update docs, remove unused code
避ける例: added feature, fixing bug, updates docs
```

---

## Body（ボディ）

### CM-BD-001: Body Optional（Body省略可）

| 項目 | 内容 |
| --- | --- |
| Rule | Bodyは省略可能とする |
| Requirement | MAY |
| Source | Project Conventions |

**Reason:**

自明な変更や小規模な修正ではBodyは不要である。Bodyを強制すると形式的な記述が増え、かえってGit履歴の品質を下げるため。

---

### CM-BD-002: Body Content（Bodyの内容）

| 項目 | 内容 |
| --- | --- |
| Rule | Bodyには変更理由（Why）を記述する |
| Requirement | SHOULD |
| Source | Documentation Philosophy, Project Conventions |

**Reason:**

変更内容（What）はコードを見れば分かる。Bodyが価値を持つのは、なぜその変更を行ったか・どのような背景があったかを記録することで、Git履歴を設計資産として機能させるためである。

**Examples:**

```text
良い例:
Replaces the legacy session-based authentication approach.
The OAuth2 flow reduces server-side session management
overhead and enables third-party identity providers.

避ける例:
Fixed the login feature.
```

---

## Footer（フッター）

### CM-FT-001: Footer Optional（Footer省略可）

| 項目 | 内容 |
| --- | --- |
| Rule | Footerは省略可能とする |
| Requirement | MAY |
| Source | Project Conventions |

**Reason:**

すべてのコミットが外部リソースや破壊的変更を持つわけではないため、必要な場合にのみ使用する。

---

### CM-FT-002: Issue Reference（Issue参照）

| 項目 | 内容 |
| --- | --- |
| Rule | Issueを参照する場合は `Refs #<number>` を使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

`Refs` はIssueを参照するが自動クローズを行わない。コミット単体でのIssueクローズは追跡を困難にするため、クローズはPull Requestに委ねる。

**Examples:**

```text
Refs #42
Refs #42, #43
```

---

### CM-FT-003: No Closing Keywords（クローズキーワード禁止）

| 項目 | 内容 |
| --- | --- |
| Rule | `Closes`・`Fixes`・`Resolves` などのIssueクローズキーワードはコミットでは使用しない |
| Requirement | MUST NOT |
| Source | Project Conventions |

**Reason:**

コミットでIssueをクローズすると、Pull Requestのマージ前にIssueが閉じられ、レビュープロセスと整合しなくなるため。IssueクローズはPull Requestで行う。

---

### CM-FT-004: Breaking Change（破壊的変更）

| 項目 | 内容 |
| --- | --- |
| Rule | 破壊的変更がある場合は `BREAKING CHANGE: <description>` をFooterの最後に配置する |
| Requirement | MUST |
| Source | Conventional Commits, Project Conventions |

**Reason:**

`BREAKING CHANGE:` はCHANGELOG生成・セマンティックバージョニングツールが破壊的変更を検出するための標準的なキーワードであるため、最後に配置することで解析ツールの誤検出を防ぐ。

**Examples:**

```text
feat(auth)!: replace session auth with OAuth2

Migrate to OAuth2 to support third-party providers.

Refs #42
BREAKING CHANGE: Session-based auth endpoints are removed.
Clients must update to use the OAuth2 flow.
```

---

## Tool Compatibility（ツール互換性）

### CM-TC-001: Footer Key-Value Format（Footerのキーバリュー形式）

| 項目 | 内容 |
| --- | --- |
| Rule | FooterのキーバリューはConventional Commits準拠の `key: value` 形式で記述する |
| Requirement | MUST |
| Source | Conventional Commits, Project Conventions |

**Reason:**

Git・GitHub・解析ツールはConventional Commitsの形式を前提としてFooterを解析する。形式が崩れるとツールが誤検出または無視するリスクがあるため。

---

### CM-TC-002: No Ambiguous Keys（曖昧なキー禁止）

| 項目 | 内容 |
| --- | --- |
| Rule | Footerに解析ツールが誤認識する可能性のある独自の `key: value` 構造を作成しない |
| Requirement | MUST NOT |
| Source | Project Conventions |

**Reason:**

予約済みキー（`BREAKING CHANGE`・`Refs`・`Closes`等）と紛らわしい独自キーを定義すると、ツールが誤った解釈を行い、CI・CHANGELOG生成に影響を与えるため。

---

## Repository Override（リポジトリ上書き）

### CM-RO-001: Override Scope（上書き可能範囲）

| 項目 | 内容 |
| --- | --- |
| Rule | Repositoryごとに上書きを許可する項目はLanguage・Type・Gitmoji・Scopeのみとする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Header構造・Body構造・Footer構造・Tool Compatibilityは共通仕様として維持することで、リポジトリをまたいだ一貫性とツール互換性を保証するため。Language・Type・Gitmoji・ScopeはRepository Profileに依存するため上書きを許可する。

---

### CM-RO-002: Override Documentation（上書きの明文化）

| 項目 | 内容 |
| --- | --- |
| Rule | Repositoryで共通仕様を上書きする場合は、そのRepositoryのドキュメントに明記する |
| Requirement | MUST |
| Source | Repository Philosophy, Project Conventions |

**Reason:**

上書きが暗黙に行われると、Git履歴の一貫性が失われ、新しい貢献者が正しいルールを判断できなくなるため。Knowledge over Tacit Knowledgeの原則に従い、すべての上書きを明文化する。

---

## Review Checklist（レビューチェックリスト）

以下のチェックリストを使用して、コミットメッセージの品質を確認する。セルフレビューおよび機械的処理主体による品質確認の両方に利用できる。

### Message Structure の確認

- [ ] Header・Body・Footerが空白行で正しく区切られているか
- [ ] Headerは存在するか

### Language の確認

- [ ] 言語はRepositoryの定義に従っているか

### Type & Gitmoji の確認

- [ ] TypeはRepository定義の値から選択しているか
- [ ] GitmojiはTypeの前に配置しているか
- [ ] GitmojiとTypeはCM-TG-002の対応表に従い1対1で対応しているか

### Scope の確認

- [ ] Scopeを使用する場合は小文字のkebab-caseか
- [ ] ScopeはRepository定義の値から選択しているか

### Subject の確認

- [ ] Subjectは変更内容（What）を表現しているか
- [ ] Subjectは72文字以内か
- [ ] 英語の場合、Subjectは動詞の原形（命令形）で始まっているか

### Body の確認

- [ ] Bodyがある場合、変更理由（Why）を記述しているか
- [ ] BodyはHeaderと空行で区切られているか

### Footer の確認

- [ ] Issue参照には `Refs #<number>` を使用しているか
- [ ] `Closes`・`Fixes`・`Resolves` をコミットで使用していないか
- [ ] 破壊的変更がある場合は `BREAKING CHANGE:` をFooterの最後に記述しているか

### Tool Compatibility の確認

- [ ] FooterはConventional Commits準拠の `key: value` 形式か
- [ ] 解析ツールが誤認識する独自キーを使用していないか
