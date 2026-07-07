# Branch Convention（ブランチ規約）

## Purpose（目的）

本書は、このプロジェクトにおけるブランチの命名規則・ライフサイクル・作成・削除タイミングを定義する。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、このリポジトリで作成するすべてのブランチに適用される。

以下は本書の対象外とする。

- GitHub上での作業ライフサイクル全体
- Commitメッセージ規約 → `docs/conventions/commit.md`
- Pull Request規約 → `templates/pull-request-templates/`
- GitHub Project運用 → GitHub Project Operation

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Commit Conventionとの関係

ブランチ名に使用するTypeはCommit ConventionのType定義（CM-TG-002）と対応させる。

---

## Design Principles（設計原則）

### Design When Needed（必要になったら設計する）

実際の利用場面が明確でないブランチ種別・命名パターンは追加しない。

### Single Source of Truth（単一情報源）

ブランチに関する情報はBranch Conventionで一元管理する。GitHub Workflow・Repository Setup・Project Operationとの重複を避ける。

### Human Readable（人間が読める）

ブランチ名はIssue番号と目的から、作業内容が一読で把握できるものとする。

### Tool Compatible（ツール互換性）

GitHub・Git・CI/CDツールが正しく解釈できる形式で命名する。スペース・特殊文字など、ツールが誤動作する文字は使用しない。

### Responsibility Separation（責務の分離）

ブランチはIssueと1対1で対応させる。複数の作業を1つのブランチで扱わない。

---

## Rule Groups と Rule ID Categories（ルールグループと識別子）

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Branch Naming | NM | ブランチ命名規則 |
| Branch Types | TY | ブランチ種別の定義 |
| Branch Lifecycle | LC | ブランチのライフサイクル |
| Branch Creation | CR | ブランチ作成タイミングと原則 |
| Branch Deletion | DL | ブランチ削除タイミングと原則 |
| Exceptions | EX | 例外運用 |

Rule IDはREADMEで定義された `BR-<Category>-<Number>` 形式に従う。

---

## Branch Naming（ブランチ命名）

### BR-NM-001: Branch Name Format（ブランチ名の基本形式）

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は `<type>/<issue-number>-<short-description>` の形式とする |
| Requirement | MUST |
| Source | Naming Convention (NM-FN-002), Project Conventions |

**Reason:**

Type・Issue番号・説明の3要素を含めることで、ブランチ名のみで作業種別・Issueとの対応・内容が一読で把握できるため。

**Examples:**

```text
feature/123-add-login
fix/124-handle-null-response
docs/125-add-branch-convention
chore/126-update-template
```

---

### BR-NM-002: Branch Name Character Set（ブランチ名の使用文字）

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチ名は小文字・英数字・ハイフン（`-`）のみを使用する |
| Requirement | MUST |
| Source | Naming Convention (NM-FN-001, NM-FN-002), Project Conventions |

**Reason:**

大文字・スペース・特殊文字はOS・Git・GitHub・CI/CDツールで予期しない動作を引き起こす可能性があるため。

**Notes:**

スラッシュ（`/`）はTypeとそれ以降を区切るために使用する唯一の例外とする。

---

## Branch Types（ブランチ種別）

### BR-TY-001: Standard Branch Types（標準ブランチ種別）

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチのTypeはCommit Conventionの共通Type候補（CM-TG-002）から選択する |
| Requirement | MUST |
| Source | Commit Convention (CM-TG-002), Project Conventions |

**Reason:**

ブランチのTypeとCommitのTypeを一致させることで、作業種別の一貫性を維持し、Git履歴とブランチ名の対応を明確にするため。

**Examples:**

| Type | 用途 |
| --- | --- |
| `feat` | 新機能 |
| `fix` | バグ修正・セキュリティ修正 |
| `docs` | ドキュメントのみの変更 |
| `chore` | 設定・ツール・不要ファイル削除 |

**Notes:**

標準Type候補に含まれないTypeが必要な場合は、Commit Conventionと合わせてRepository Overrideで定義する。

---

## Branch Lifecycle（ブランチライフサイクル）

### BR-LC-001: Branch Lifecycle（ブランチのライフサイクル）

| 項目 | 内容 |
| --- | --- |
| Rule | ブランチはIssue作成からMerge・削除までを1つのライフサイクルとして扱う |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

ブランチを作業単位（Work）と対応させることで、ブランチの目的と有効期間を明確にするため。

**Examples:**

```text
Issue
    ↓
Create Branch
    ↓
Commit
    ↓
Pull Request
    ↓
Merge
    ↓
Delete Branch
```

---

## Branch Creation（ブランチ作成）

### BR-CR-001: Create Branch at Work Start（作業開始時のブランチ作成）

| 項目 | 内容 |
| --- | --- |
| Rule | BranchとPull Requestを使用する運用では、作業開始時にIssueに対応するBranchを作成する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

作業の開始と同時にブランチを作成することで、変更がmainブランチへ直接混入することを防ぎ、Pull Requestによるレビューを可能にするため。

---

### BR-CR-002: One Branch per Issue（1 Issue = 1 Branch）

| 項目 | 内容 |
| --- | --- |
| Rule | 1つのIssueに対して1つのBranchを作成する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

複数のIssueを1つのBranchで扱うと、Pull Requestのレビュー範囲が曖昧になり、完了条件との対応が不明確になるため。

---

## Branch Deletion（ブランチ削除）

### BR-DL-001: Delete Branch after Merge（Merge後のブランチ削除）

| 項目 | 内容 |
| --- | --- |
| Rule | MergeされたBranchは削除する |
| Requirement | MUST |
| Source | Project Conventions |

---

### BR-DL-002: No Long-Lived Work Branches（長期作業ブランチの禁止）

| 項目 | 内容 |
| --- | --- |
| Rule | 長期間利用する作業ブランチを作らない |
| Requirement | SHOULD NOT |
| Source | Project Conventions |

**Reason:**

長期ブランチはmainブランチとの乖離が大きくなり、Mergeコストが増大する。作業は小さい単位に分割し、Issueと1対1で対応させることで解消する。

---

## Exceptions（例外）

### BR-EX-001: Repository Override（リポジトリ固有の例外）

| 項目 | 内容 |
| --- | --- |
| Rule | リポジトリ固有の事情による例外はRepository Overrideとして各リポジトリのドキュメントに明示する |
| Requirement | MUST |
| Source | Repository Philosophy, Project Conventions |

**Reason:**

暗黙の例外は運用の一貫性を損なうため、例外は常に明文化する。

**Examples:**

- 初期構築段階（main-only運用）
- 緊急修正（通常のIssueフローを経ない場合）
- main-onlyリポジトリ（Branch運用を採用しない場合）

---

## Review Checklist（レビューチェックリスト）

- [ ] ブランチ名は `<type>/<issue-number>-<short-description>` の形式か
- [ ] TypeはCommit ConventionのType候補から選択しているか
- [ ] ブランチ名にIssue番号が含まれているか
- [ ] ブランチ名の文字は小文字・英数字・ハイフンのみか
- [ ] ブランチ名から作業の目的が読み取れるか
- [ ] 1 Issue = 1 Branch の原則を満たしているか
- [ ] Merge後にブランチを削除する運用になっているか
