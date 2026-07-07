# GitHub Workflow（GitHub運用ワークフロー）

## Purpose（目的）

本書は、GitHub上での作業ライフサイクルを定義する。

GitHub WorkflowはIssueを起点として作業を管理するIssue駆動運用を採用する。各要素の責務を明確にし、作業の開始から完了までを一貫した運用として定義することを目的とする。

---

## Scope（適用範囲）

本書は、GitHub上での作業ライフサイクルに適用する。

対象は以下を含む。

- Issue
- Branch
- Commit
- Pull Request
- Review
- Merge
- Close Issue

以下は本書の対象外とする。

- Commitメッセージの詳細規約 → `docs/conventions/commit.md`
- Branch命名規則の詳細 → Naming Convention
- Pull Request Templateの内容 → `templates/pull-request-templates/`
- GitHub ProjectのField設定 → `docs/specifications/github-project-setup.md`
- Repository初期構築手順 → `docs/specifications/repository-setup.md`

---

## Core Concept（基本概念）

### Issue-Driven Workflow（Issue駆動運用）

GitHub Workflowは、Issueを起点とする。

すべての作業はIssueから始まり、Issueの完了をもって終わる。Issueが存在しない作業は、原則として開始しない。

```text
Issue → Work → Commit → Merge → Close Issue
```

BranchとPull Requestを使用する運用では、以下の流れとなる。

```text
Issue → Branch → Commit → Pull Request → Review → Merge → Close Issue
```

### Work Unit（作業単位）

Workとは、1つのIssueを完了させるために必要な一連の作業である。

作業単位は1 Issueを基本とする。

```text
1 Issue = 1 Work
```

BranchとPull Requestを使用する運用では、以下を標準とする。

```text
1 Issue = 1 Work = 1 Branch = 1 Pull Request
```

この原則により、IssueのDescriptionおよび完了条件とPull Requestのレビュー対象を一致させる。複数の作業が1つのPull Requestに混在すると、レビューの焦点が分散し、完了条件との対応が曖昧になる。

---

## Workflow Lifecycle（ワークフローライフサイクル）

### 1. Create Issue（Issue作成）

作業を開始する前に、Issueを作成する。

Issueは「何をするか」を定義する要素である。以下を明確にする。

- 作業のDescription（何を実現するか）
- 完了条件（何が満たされたら完了か）

背景・理由・補足はIssueに記載し、Branch・Commit・Pull Requestへ重複して記載しない。

### 2. Start Work（作業開始）

Issueが明確になった段階で作業を開始する。

GitHub Projectを利用する場合は、Project Operationに従いStatusを更新する。

### 3. Create Branch（Branch作成）

BranchとPull Requestを使用する運用では、Issueに対応するBranchを作成する。

BranchはIssueを実現するための作業空間である。Branchは1つのIssueに対応させる。

### 4. Commit Changes（変更のCommit）

作業の進捗をCommitとして記録する。

CommitはIssueに対応する作業履歴である。CommitはIssueの完了条件を満たすための変更を記録する。Commitメッセージの規約は `docs/conventions/commit.md` を参照する。

### 5. Open Pull Request（Pull Request作成）

作業が完了したら、Pull Requestを作成する。

Pull RequestはIssueをどう実現したかを示すレビュー対象である。Closing Keywordを使用して関連IssueをPull Requestと紐づける。

| Closing Keyword | 用途 |
| --- | --- |
| `Closes #<number>` | Merge時にIssueを自動クローズする |
| `Refs #<number>` | Issueへの参照のみ行う（クローズしない） |

Pull Requestの内容はIssueの内容を複製しない。差分の説明（Summary）に留める。

### 6. Review（レビュー）

Pull Requestが作成されたら、レビューを実施する。

ReviewはIssueの完了条件を満たしているかを確認する工程である。コードの正確性とともに、Issueに定義された完了条件との対応を確認する。

GitHub Projectを利用する場合は、Project Operationに従いStatusを更新する。

### 7. Merge（マージ）

Reviewが承認されたら、Pull RequestをMergeする。

MergeはIssueに対応する作業完了の確定点である。Merge後、BranchはGitHub上で削除する。

### 8. Close Issue（Issue完了）

Closing Keywordを使用している場合、MergeによりIssueは自動的にクローズされる。

Issue CloseはMergeの結果として発生し、Workflow全体の終点である。Closing Keywordを使用していない場合は手動でクローズする。GitHub Projectを利用する場合は、Project Operationに従いStatusを更新する。

---

## Principles（運用原則）

### Issue First（Issue優先）

作業はIssueの作成から始める。Issueが存在しない作業は、原則として開始しない。

### Single Responsibility per Issue（Issue単位の責務分離）

1つのIssueは1つの作業を担う。複数の作業を1つのIssueにまとめない。

### Information Stays at Source（情報の単一管理）

作業の目的・背景・完了条件はIssueで管理する。Branch・Commit・Pull Requestへ重複して記載しない。

### Complete with Close（クローズで完結）

作業はIssue Closeをもって完了とする。Mergeのみで完了とせず、IssueがCloseされるまでをWorkflowの範囲とする。

---

## Exceptions（例外）

### Initial Repository Setup（初期構築時の例外）

リポジトリの基盤を整備する最初期段階では、以下の例外を認める。

```text
main-only / no-branch / no-PR
```

これは初期構築・設計の試行錯誤段階に限定した運用である。通常運用への移行後は、Issue駆動運用へ切り替える。

例外を適用する期間および条件は、各リポジトリのドキュメントで明示する。

---

## Review Checklist（確認項目）

### Issue作成時

- [ ] Descriptionに「何を実現するか」が記載されているか
- [ ] 完了条件が定義されているか

### Branch・PR作成時

- [ ] BranchはIssueと1対1で対応しているか
- [ ] Pull RequestにClosing Keywordでイシューが紐づいているか
- [ ] Pull RequestのSummaryがIssueの内容を複製していないか

### Review時

- [ ] IssueのDescriptionと完了条件を確認したか
- [ ] 完了条件がすべて満たされているか

### Merge・Close時の確認

- [ ] Mergeが完了しているか
- [ ] IssueがCloseされているか

### 原則の確認

- [ ] 1 Issue = 1 Work の原則が維持されているか

---

## Notes（補足）

本書はGitHub Workflowの操作手順書ではない。各要素の責務とライフサイクルを定義するSpecificationである。

GitHub UIの具体的な操作方法は、各リポジトリのドキュメントまたはGitHubの公式ドキュメントを参照する。
