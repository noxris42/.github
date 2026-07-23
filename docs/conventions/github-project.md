# GitHub Project Convention（GitHubプロジェクト運用規約）

## Purpose（目的）

本書は、GitHub Projectsの日常運用ルールを定義する。

Projectの構築方法を定義する文書ではなく、GitHub Projectで管理する作業の基本フローと、構築済みProjectのStatusをいつ・どのように変更するかを定義する運用規約である。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、GitHub Projectへ登録して管理するIssueおよびPull Requestの日常運用に適用する。

対象は以下を含む。

- Status変更タイミング
- Review移行・完了条件
- Blocked条件・解除条件
- Done条件

以下は本書の対象外とする。

- ProjectのField・View・Automation構築方法
- IssueおよびPull Requestの詳細手順
- GitHub ProjectのField定義・Status値定義

### Task IssueとGitHub Projectの関係

本書の適用にあたり、Task IssueとGitHub Projectの関係を次のとおり扱う。

- Task Issueの作成自体はGitHub Projectでの管理を必須としない
- Projectへ登録しないTask Issueの変更経路はBranching Modelが定義する
- Issueなし作業は本書の対象外
- Projectへ登録した作業には本書のStatus Ruleを厳格に適用する

---

## Relationships（関係性）

### Conventions READMEとの関係

本書は `docs/conventions/README.md` を前提とする。Requirement Levels・Rule Components・Rule Sources・Rule ID構造はREADMEで定義されており、本書では再定義しない。

### Branch Conventionとの関係

Branch Conventionおよび選択されたBranching Modelは、Branch構成、変更経路、Issueとの対応関係およびBranchのライフサイクルを定義する。本書は、GitHub Projectで管理するTask Issueについて、その変更経路に対応したStatus遷移を定義する。GitHub Projectで管理する作業は、Task Issue・Work Branch・Pull Requestを共通フローとして使用するため、Status遷移をBranching Modelごとに分岐させない。

---

## Design Principles（設計原則）

### Single Source of Truth（単一情報源）

Project運用ルールは本書で一元管理する。Status変更タイミング・Review条件・Blocked条件・Done条件を他文書へ重複して記載しない。

### Responsibility Separation（責務の分離）

本書は、GitHub Projectで管理する作業の共通フローとStatus運用を扱う。ProjectのField・View構築方法は本書の対象外であり、本書では扱わない。Branchの具体的な構成、分岐元、統合先、命名、終了条件などのBranchライフサイクルはBranch ConventionおよびBranching Modelの責務とし、本書では再定義しない。

### Human Readable（人間が読める）

Status遷移のタイミングは、誰が見ても判断できる基準で定義する。主観的な解釈が生じる表現を避ける。

### Tool Compatible（ツール互換性）

GitHub Projectsの標準機能で実現できる運用を基本とする。カスタム自動化を前提とした運用ルールは追加しない。

---

## Rule Groups と Rule ID Categories（ルールグループと識別子）

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Managed Work | MW | Projectで管理する作業単位と変更経路 |
| Status | ST | Status変更タイミング |
| Review | RV | Review移行・完了条件 |
| Blocked | BL | Blocked条件・解除条件 |
| Done | DN | Done条件 |
| Exceptions | EX | 例外運用 |

Rule IDはREADMEで定義された `GP-<Scope>-<Category>-<Number>` 形式に従う。本Conventionで新規定義するRuleのScopeには`BS`を使用する。

---

## Managed Work Operation（管理作業運用）

### GP-BS-MW-001: Use Managed Work Flow（Project管理作業の標準フロー）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理する作業はTask Issueとして登録し、Branch Conventionに従って対応するWork Branchを作成し、そのWork Branchの変更を1つのPull Requestとして統合する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Task Issue・Work Branch・Pull Requestを対応させることで、Project上の作業単位、Branch上の変更範囲およびレビュー対象を一致させ、Status運用の前提を安定させるため。

**Notes:**

- Task Issueの作成だけでは、GitHub Projectでの管理を意味しない
- GitHub Projectで管理しないTask Issueは本Ruleの対象外
- Task IssueとWork Branchの1対1対応はBranch Conventionに従う
- Projectで管理する作業は、1 Task Issue・1 Work Branch・1 Pull Requestを対応単位とする
- DraftからReady for reviewへの変更は、同一のPull Requestの状態変更として扱う
- Pull Requestの再作成が必要な場合は、旧Pull Requestと新Pull Requestの対応関係および再作成理由を記録する。継続的に異なる運用を採用する場合は、Repository Conventionで明示する
- Work Branchの分岐元、統合先、命名および具体的な統合方法はBranching Modelに従う
- Pull Requestの本文・レビュー方法はPull Request Conventionまたは関連文書に従う
- EpicおよびFeatureは階層管理単位であり、本RuleのWork BranchおよびPull Request対応単位にはしない

---

## Status Operation（Status運用）

### GP-BS-ST-001: Status Must Reflect Current State（Statusは現在の状態を反映する）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectへ登録されたIssueのStatusは、常に現在の作業状態を反映させる |
| Requirement | MUST |
| Source | Repository Philosophy, Project Conventions |

**Reason:**

Statusが実態と乖離すると、Projectの状態管理としての価値を失うため。

---

### GP-BS-ST-002: Ready to In Progress（作業開始時のStatus変更）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectへ登録されたIssueについて、作業を開始したらStatusを `In Progress` へ変更する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

作業開始のタイミングをStatusに反映することで、誰が何に着手しているかを一読で把握できるようにするため。

---

### GP-BS-ST-003: In Progress to Review（Review移行時のStatus変更）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectへ登録されたIssueについて、ReviewへのStatus変更条件はGP-BS-RV-001に従う |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Review移行の条件はGP-BS-RV-001で定義するため、本ルールはその参照として機能する。Status変更のタイミングとReview移行の条件を同一ルールで定義することを避け、責務を分離する。

---

## Review Operation（Review運用）

### GP-BS-RV-001: Review Transition Condition（Review移行条件）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理するTask Issueについて、作業内容が完了条件を満たした状態でPull Requestを作成した時点でReviewへ移行する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

完了条件を満たさない状態でReviewへ移行すると、レビューの焦点が定まらないため。

---

### GP-BS-RV-002: Review Completion Condition（Review完了条件）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理するTask Issueについて、対応するPull Requestが承認されMergeされた時点でReviewを完了とする |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Mergeをもって変更が確定するため、MergeをReview完了の基準とする。

---

## Blocked Operation（Blocked運用）

### GP-BS-BL-001: Blocked Transition Condition（Blocked移行条件）

| 項目 | 内容 |
| --- | --- |
| Rule | 以下のいずれかに該当する場合にStatusを `Blocked` へ変更する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Blockedを明示することで、作業が停止している理由と対応が必要な状態を可視化するため。

**Examples:**

- 外部レビュー・承認待ちで作業を進められない場合
- 依存するIssueが完了していない場合
- 外部要因（ツール障害・情報不足・仕様未確定）により作業を継続できない場合

---

### GP-BS-BL-002: Blocked Resolution Condition（Blocked解除条件）

| 項目 | 内容 |
| --- | --- |
| Rule | ブロッカーが解消された時点でStatusを `In Progress` または `Ready` へ戻す |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

ブロッカー解消後にStatusを更新しないと、実態と乖離したまま放置されるため。

**Notes:**

解消後に即座に着手する場合は `In Progress`、着手待ちの場合は `Ready` へ変更する。

---

## Done Operation（Done運用）

### GP-BS-DN-001: Done Transition Condition（Done移行条件）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理するTask Issueについて、Pull RequestのMergeが完了しIssueがCloseされた時点でStatusを `Done` へ変更する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

MergeとIssue Closeの両方が完了した状態をProject上の完了とすることで、作業完了の定義を一意にするため。

---

### GP-BS-DN-002: Done Is Project Status（DoneはProject上の状態である）

| 項目 | 内容 |
| --- | --- |
| Rule | DoneはProject上の状態管理であり、Issue Closeとは独立して管理する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

Closing Keywordによる自動クローズが発生した場合でも、ProjectのStatusは手動で `Done` へ変更する必要がある。IssueのCloseとProjectのStatusは別の管理軸であるため。

**Notes:**

Project Automationを導入してMerge時にDoneへ自動遷移する設定を行う場合は、Repository Overrideとして明示することで本ルールを変更できる。

---

## Exceptions（例外）

### GP-BS-EX-001: Repository Override（リポジトリ固有の例外）

| 項目 | 内容 |
| --- | --- |
| Rule | リポジトリ固有の事情による例外はRepository Overrideとして各リポジトリのドキュメントに明示する |
| Requirement | MUST |
| Source | Repository Philosophy, Project Conventions |

**Reason:**

暗黙の例外は運用の一貫性を損なうため、例外は常に明文化する。

**Examples:**

- GitHub Projectsを利用しないリポジトリ（Status管理不要）
- 簡略Status運用（Backlog・In Progress・Doneのみ）
- リポジトリ固有のStatus値追加

---

## Review Checklist（レビューチェックリスト）

- [ ] Status変更タイミングがすべての状態について明確か
- [ ] Review移行条件は完了条件ベースで定義されているか
- [ ] Review完了条件が明確か
- [ ] Blocked条件が具体的に列挙されているか
- [ ] Blocked解除後の遷移先が定義されているか
- [ ] Done移行条件がIssue Closeとの関係を含めて明確か
- [ ] ProjectのField・View構築方法を本書に記載していないか
- [ ] Branchの具体的な構成・分岐元・統合先・命名・終了条件など、Branchライフサイクルを再定義していないか
- [ ] GitHub Projectで管理する作業がTask Issueとして登録され、対応するWork BranchおよびPull Requestが使用されているか
- [ ] Task Issueの作成だけを理由にGitHub Projectへの登録を必須としていないか
- [ ] Project管理外の作業経路を本書で再定義していないか
