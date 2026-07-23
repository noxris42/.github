# Branch Convention（ブランチ規約）

## Purpose（目的）

本書は、Branch Conventionの共通原則と、各リポジトリが選択するBranching Modelに求める基本要件を定義する。

Convention Extension Architecture上では、リポジトリごとに選択する標準的な拡張をPattern Conventionと呼ぶ。Branch Conventionでは、そのPattern Conventionの実体をBranching Modelと呼ぶ。

Requirement Levels・Rule Components・Rule Sourcesの定義は `docs/conventions/README.md` を参照する。本書では再定義しない。

---

## Scope（適用範囲）

本書は、Branch Conventionを適用するリポジトリ、選択されるBranching Model、リポジトリで使用されるBranch名の共通制約、Branchの役割・寿命・ライフサイクルを定義する際の共通要件、およびTask IssueとWork Branchを対応させる場合の共通契約に適用される。

以下は本書の対象外とする。

- 個別のBranching Modelの具体的な運用
- Commitメッセージ → `docs/conventions/commit.md`
- Pull Requestの記述・レビュー方法
- GitHub ProjectのStatus・管理作業運用 → GitHub Project Convention
- Epic／Feature／Taskの意味・階層構造 → GitHub Project Setup
- Issueテンプレートの構造・内容（現時点で参照文書なし）
- GitHub Projectへの登録、優先度・Milestoneなど、Issueの日常運用 → GitHub Project Convention
- Release／Versioningの詳細
- GitHub Actionsの実装
- Gitコマンドを含む具体的な作業手順
- Repository固有の例外・追加要件 → Repository Convention

Pull Requestを使用するかどうか自体はBranching Modelが定義する事項であり、本書全体の対象外とはしない。ただし、Pull Requestの本文・レビュー方法・テンプレートは対象外とする。

Task IssueとWork Branchを対応させる場合の1対1原則、およびBranching ModelがIssueとBranchの関係を定義するための共通契約も、本書の対象とする。ただし、Issue・Branch・Pull Requestの使用そのものを必須化するものではない。

---

## Relationships（関係性）

### Convention Extension Architectureとの関係

Base Branch Conventionは、Branching Modelに依存しない共通Ruleを定義する。各リポジトリは、Pattern ConventionとしてBranching Modelを1つ選択する。Repository Conventionは、選択したBranching Modelに対するリポジトリ固有の変更を定義する。Effective Branch Conventionは、これらを適用した結果として成立する。

### Repository Manifestとの関係

リポジトリが選択したBranching Modelは、Repository Manifestで宣言する。ManifestはRule本文を保持しない。選択されたBranching Modelを定義するPattern Convention文書が、そのRuleの正本である。

### 他Conventionとの関係

- Naming Convention：Branch名を含む一般的な命名原則を定義する。本書はBranch名固有の制約のみを定義する
- Commit Convention：Commitメッセージの構造・記述方法を定義する
- Pull Request Convention（将来）：Pull Requestの作成・記述・レビューを定義する
- GitHub Project Setup：Epic・Feature・Taskの意味と階層を定義する。本書のTask Issueは、GitHub Project Setupが定義するTask Issueを指す
- GitHub Project Convention：GitHub Projectへ登録して管理する作業のStatus運用を定義する。本書は、Task IssueをWork Branchと対応させる場合のBranch側の原則のみを定義する
- Release／Versioning関連文書（将来）：リリースとバージョン管理を定義する

---

## Design Principles（設計原則）

### Model Independence（Modelからの独立）

Base Ruleは、特定のBranching Modelを前提としない。特定の運用パターンに固有の前提は、Base Ruleへ持ち込まない。

### Complete Model Definition（Modelの完全な定義）

Branching Modelは、リポジトリのBranch運用を一意に判断できるだけの情報を定義する。Base Branch ConventionとBranching Modelを合わせて参照すれば、そのリポジトリのBranch運用が一意に定まる状態を維持する。

### Single Source of Truth（単一情報源）

共通原則はBase Branch Conventionへ、Model固有の運用はBranching Modelへ、Repository固有差異はRepository Conventionへ、操作手順は運用手順書へ、それぞれ分離する。同じ情報を複数の文書で重複管理しない。

### Human Readable（人間が読める）

Branch名から、そのBranchの役割または作業目的を識別できるようにする。Issue番号を必須要素とはしない。

### Tool Compatible（ツール互換性）

Git・GitHub・CI/CDなどのツールが安全に扱えるBranch名を使用する。

### Explicit Lifecycle（明示的なライフサイクル）

使用する各Branchについて存在理由を明示し、一時Branchについて終了条件を明示する。

---

## Rule Groups と Rule ID Categories（ルールグループと識別子）

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Branching Model | BM | Branching Modelの選択と定義要件 |
| Branch Naming | NM | Branch名の共通原則 |
| Branch Lifecycle | LC | Branchの寿命と終了条件 |
| Repository Extension | EX | Repository固有の拡張 |

Rule IDはREADMEで定義された `BR-<Scope>-<Category>-<Number>` 形式に従う。本Conventionで新規定義するRuleのScopeには`BS`を使用する。

---

## Branching Model（Branching Model）

### BR-BS-BM-001: Select Branching Model（Branching Modelの選択）

| 項目 | 内容 |
| --- | --- |
| Rule | Branch Conventionを適用する各リポジトリは、適用するBranching Modelを正確に1つ選択する |
| Requirement | MUST |
| Source | Convention Extension Architecture, Repository Manifest Specification |

**Reason:**

Branch構成とライフサイクルを一意に決定するため。

**Notes:**

- 選択結果はRepository Manifestで宣言する
- Repository ConventionはBranching Modelの代わりにはならない
- Repository固有差異は、Branching Modelを選択した後にRepository Conventionで定義する

---

### BR-BS-BM-002: Follow Selected Branching Model（選択Modelへの準拠）

| 項目 | 内容 |
| --- | --- |
| Rule | リポジトリのBranch運用は、選択したBranching Modelに従う |
| Requirement | MUST |
| Source | Convention Extension Architecture |

**Reason:**

Branching Modelを宣言するだけで、実際の運用がそれと異なる状態を防ぐため。

---

### BR-BS-BM-003: Define Branching Model（Branching Modelの定義要件）

| 項目 | 内容 |
| --- | --- |
| Rule | Branching Modelは、使用する各Branchの役割、寿命、作成条件、分岐元、統合先および変更経路を定義し、一時Branchについては終了条件を定義する |
| Requirement | MUST |
| Source | Convention Extension Architecture, Project Conventions |

**Reason:**

リポジトリのBranch運用を一意に判断できる状態を保つため（Complete Model Definition）。永続Branchには終了条件が存在しない場合があるため、終了条件の定義対象は一時Branchに限定し、BR-BS-LC-001・BR-BS-LC-002と矛盾しない表現とする。

**Notes:**

- Branching Modelは、必要に応じて次も定義対象にできる
  - mainなどデフォルトBranchへの直接Commit／Pushの可否
  - Pull Requestの要否
  - Issueとの対応関係
  - Branch Protectionの設定方針
  - release・hotfix・保守Branchの構成
- すべてのBranching Modelにrelease・hotfixの構成を必須とはしない
- Branching Modelが特定のBranchまたは運用経路を使用しない場合は、必要に応じて使用しないことを明示する
- Branching Modelは、使用する一時Branchのうち、どのBranchをWork Branchとして扱うかを定義する。Task IssueとWork Branchの対応原則は`BR-BS-BM-004`が定義する

---

### BR-BS-BM-004: Maintain Task Issue and Work Branch Correspondence（Task IssueとWork Branchの対応）

| 項目 | 内容 |
| --- | --- |
| Rule | Task IssueとWork Branchを対応させる場合は、1つのTask Issueに1つのWork Branchを対応させ、1つのWork Branchを複数のTask Issueに対応させない |
| Requirement | MUST |
| Source | GitHub Project Setup, Project Conventions |

**Reason:**

- Task Issueを独立した作業単位として扱うため
- 1つのWork Branchへ複数Taskの変更が混在することを防ぐため
- Task Issueの完了条件とBranch上の変更範囲を一致させるため
- 差分確認、変更追跡、作業中止、統合判断を明確にするため

**Notes:**

- 本Ruleは、Task IssueまたはWork Branchの作成を必須としない
- IssueなしでWork Branchを作成できるかは、Branching Modelが定義する
- Task IssueをWork Branchなしで完了できるかは、Branching Modelが定義する
- Work Branchと対応できるIssue種別は、GitHub Project Setupで実際の作業単位として定義されたTask Issueとする
- Work BranchをデフォルトBranchなどへ統合する方法は、Branching Modelが定義する
- Pull Requestの要否およびWork BranchとPull Requestの対応関係は、Branching Modelが定義する
- release・hotfix・保守・移行などの特殊Branchは、Branching ModelがWork Branchとして分類した場合に限り本Ruleの対象となる

---

## Branch Naming（Branch命名）

### BR-BS-NM-001: Branch Name Character Set（Branch名の使用文字）

| 項目 | 内容 |
| --- | --- |
| Rule | Branch名には、英小文字、数字、ハイフンおよび階層区切りのスラッシュを使用する。その他の文字は、選択したBranching Modelが明示的に許可する場合に限り使用できる |
| Requirement | MUST |
| Source | Naming Convention (NM-BS-FN-001, NM-BS-FN-002), Project Conventions |

**Reason:**

大文字・スペース・特殊文字はOS・Git・GitHub・CI/CDツールで予期しない動作を引き起こす可能性があるため。

**Notes:**

- スペースや制御文字を使用しない
- Branching Modelは、バージョン番号のピリオドなど、追加の文字を許可できる
- Repository Conventionは、選択したBranching Modelの制約をさらに厳格化できる
- Gitの技術上使用可能であっても、ツール互換性を損なう文字は使用しない

---

### BR-BS-NM-002: Identify Branch Purpose（Branch目的の識別可能性）

| 項目 | 内容 |
| --- | --- |
| Rule | デフォルトBranch以外のBranchには、その役割または作業目的を識別できる名前を付ける |
| Requirement | MUST |
| Source | Naming Convention, Branch Convention |

**Reason:**

- Branching Modelによってデフォルトブランチの名前が異なる可能性があるため
- Branch一覧だけで用途を判断できるようにするため
- 不要なBranchや誤った統合先を識別しやすくするため

---

## Branch Lifecycle（Branchライフサイクル）

### BR-BS-LC-001: Classify Branch Lifetime（Branch寿命の分類）

| 項目 | 内容 |
| --- | --- |
| Rule | Branching Modelは、使用する各Branchを永続Branchまたは一時Branchとして分類する |
| Requirement | MUST |
| Source | Project Conventions |

**Notes:**

- 永続Branch：Branching Modelが定義する継続的な役割を持ち、個別作業の完了だけでは削除されないBranch
- 一時Branch：特定の作業・リリース・移行など、終了条件を持つBranch
- Work Branch：独立した作業単位の変更を、デフォルトBranchなどから隔離して行うための一時Branch。release Branch、hotfix Branch、保守Branch、移行Branchなどを自動的にWork Branchへ含めるものではなく、使用する各Branchをどれに分類するかはBranching Modelが定義する
- 分類は存在期間の長短だけで決めない。`next`のように長期間存在しうるBranchであっても、移行完了という終了条件を持つ場合は一時Branchになり得る

---

### BR-BS-LC-002: Define Branch End Condition（Branch終了条件の定義）

| 項目 | 内容 |
| --- | --- |
| Rule | Branching Modelは、使用する各一時Branchについて目的完了の条件と、その後の削除または保持方法を定義する |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

- Mergeだけが終了条件とは限らないため
- release完了、移行完了、廃止なども終了条件になり得るため
- 不要な一時Branchの残存を防ぐため

---

### BR-BS-LC-003: Complete Temporary Branch Lifecycle（一時Branchライフサイクルの完了）

| 項目 | 内容 |
| --- | --- |
| Rule | 一時Branchは、Branching Modelで定義された目的と終了条件を満たした後、定義された方法で速やかにライフサイクルを完了する |
| Requirement | MUST |
| Source | Project Conventions |

**Notes:**

- 通常は削除を意味する
- Branching Modelが明示的に保持・アーカイブ相当の扱いを定義する場合は、それに従う
- 作業完了後の無期限放置は許可しない
- 永続Branchは本Ruleの対象外とする

---

## Repository Extension（Repository拡張）

### BR-BS-EX-001: Repository-Specific Branch Rules（リポジトリ固有のBranch Rule）

| 項目 | 内容 |
| --- | --- |
| Rule | 選択したBranching Modelでは表現できないリポジトリ固有のBranch運用は、Repository Conventionとして明示する |
| Requirement | MUST |
| Source | Repository Philosophy, Project Conventions |

**Notes:**

- Repository ConventionはBaseまたはPattern RuleをReplace・Extend・Disableできる
- Repository固有の新規RuleをAddできる
- 暗黙の例外は設けない
- Branching Modelそのものを、Repository Conventionで再定義しない
- 実質的に別Modelとなるほどの変更が必要な場合は、新しいBranching Modelの作成を検討する
- Repository Conventionによる変更は、選択したBranching Modelの基本的なBranch構成および変更経路を維持する範囲に限る。Modelの中心的な構造またはライフサイクルを変更する場合は、新しいBranching Modelとして定義する

---

## Review Checklist（レビューチェックリスト）

- [ ] Repository ManifestでBranching Modelが正確に1つ宣言されているか
- [ ] Branch運用が選択したBranching Modelに従っているか
- [ ] Branching Modelが各Branchの役割と寿命を定義しているか
- [ ] 各Branchの作成条件・分岐元・統合先が定義されているか
- [ ] 各一時Branchの終了条件が定義されているか
- [ ] デフォルトBranch以外のBranch名から役割または作業目的を識別できるか
- [ ] Branch名がGit・GitHub・関連ツールで安全に扱えるか
- [ ] Repository固有の差異がRepository Conventionへ明示されているか
- [ ] Task IssueとWork Branchを対応させる場合、1対1の関係になっているか（GitHub Project Setupで定義されたTask Issue以外にWork Branchを直接対応させていないか含む）
- [ ] Branching ModelがIssueなしWork BranchおよびBranchなしTask Issueの可否を定義しているか
- [ ] Branching ModelがWork Branchの統合方法とPull Requestの要否を定義しているか
