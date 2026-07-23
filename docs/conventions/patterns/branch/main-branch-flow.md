# Main Branch Flow（メインブランチフロー）

## Purpose（目的）

Main Branch Flowは、Branch ConventionのPattern Conventionである。`main`を正本かつ通常の作業場所とし、`main`への直接Commit／Pushを許可するBranching Modelを定義する。

GitHub Projectで管理する作業には、Task Issue・Work Branch・Pull Requestを使用する厳格な変更経路を適用する。GitHub Projectで管理しない作業では、Task Issueの有無にかかわらず、`main`への直接Commit／PushまたはWork Branchによる隔離のいずれかを選択できる。

本書は、`docs/conventions/branch.md`（Base Branch Convention）で定義された共通Ruleを前提とし、複製しない。本書が定義するのは、Main Branch Flow固有の内容だけである。

---

## Scope（適用範囲）

本書は、Repository ManifestでMain Branch Flowを選択したリポジトリにおける、`main`とWork Branchの構成、変更経路、Task Issue・GitHub Projectとの対応、Branch Protection方針に適用する。

以下は本書の対象外とする。

- Branch Conventionが定義する共通原則（Branch名の使用文字、Branch寿命の分類、一時Branchの終了条件など） → `docs/conventions/branch.md`
- GitHub Projectで管理する作業のStatus運用およびManaged Work Rule → `docs/conventions/github-project.md`
- Epic／Feature／Taskの意味・階層 → `docs/specifications/github-project-setup.md`
- Pull Requestの本文・レビュー方法
- Commitメッセージの記述方法 → `docs/conventions/commit.md`
- Gitコマンドを含む具体的な作業手順
- リポジトリ固有の例外・追加要件 → Repository Convention

---

## Relationships（関係性）

### Base Branch Conventionとの関係

Main Branch Flowは、Base Branch Convention（`docs/conventions/branch.md`）を前提とし、次を参照する。複製はしない。

- `BR-BS-BM-001`〜`BR-BS-BM-003`：Branching Modelの選択・準拠・定義要件
- `BR-BS-BM-004`：Task IssueとWork Branchを対応させる場合の1対1原則
- `BR-BS-NM-001`〜`BR-BS-NM-002`：Branch名の使用文字、目的識別可能性
- `BR-BS-LC-001`〜`BR-BS-LC-003`：Branch寿命の分類、一時Branchの終了条件、ライフサイクル完了
- `BR-BS-EX-001`：Repository固有拡張の境界

### GitHub Project Conventionとの関係

GitHub Projectで管理する作業のTask Issue・Work Branch・Pull Request対応は、`docs/conventions/github-project.md`の`GP-BS-MW-001`（Managed Work Rule）に従う。Project Statusの値、Status遷移、Reviewへの移行条件、Done条件は本書で再定義しない。

### GitHub Project Setupとの関係

Epic・Feature・Taskの意味および階層は、`docs/specifications/github-project-setup.md`を正本とする。本書はTask Issueという型を参照するのみで、その意味を再定義しない。

### Repository Conventionとの関係

Repository Conventionは、Main Branch Flowの基本構造（`main`を唯一の永続Branchとすること、`main`への直接Commit／Pushを許可すること、GitHub Project管理作業でWork BranchとPull Requestを必須とすること）を維持する範囲で調整できる。この中心的構造を変更する場合は、Repository Conventionではなく新しいBranching Modelとして扱う。

---

## Rule Groups と Rule ID Categories（ルールグループと識別子）

| Rule Group | Category | 対象 |
| --- | --- | --- |
| Model Structure | MS | `main`とWork Branchの構造 |
| Change Path | CP | 直接変更・Branch統合経路 |
| Issue Relationship | IS | Issue・Project・Work Branchの関係 |
| Branch Naming | NM | Work Branch命名 |
| Branch Lifecycle | LC | Work Branchの終了と削除 |

Rule IDは`docs/conventions/README.md`および`docs/specifications/convention-extension.md`で定義された`<Convention>-<Scope>-<Category>-<Number>`形式に従う。本書はPattern Conventionであるため、新規定義するRuleのScopeには`MB`を使用する。

---

## Model Structure（モデル構造）

### BR-MB-MS-001: Use Main as Persistent Branch（mainを永続Branchとして使用する）

| 項目 | 内容 |
| --- | --- |
| Rule | `main`を唯一の永続Branchとして使用する。`main`は正本かつ通常の作業場所であり、分岐元・統合先を持たない |
| Requirement | MUST |
| Source | Branch Convention (BR-BS-LC-001), Project Conventions |

**Reason:**

`main`を単一の正本かつ通常の作業場所とすることで、追加の永続Branchを介さずに変更を反映できる単純な構造を維持するため。

**Notes:**

- 役割：正本および通常の作業場所
- 作成条件：Repository作成時
- 分岐元／統合先：なし
- Base Branch Convention（`BR-BS-LC-001`）の永続Branch分類に基づき、`main`は終了条件を持たない
- `main`は通常の作業場所として使用できる。専用のWork Branchを経由しなければ変更できない構造ではない

---

### BR-MB-MS-002: Use Optional Work Branches（Work Branchの使用）

| 項目 | 内容 |
| --- | --- |
| Rule | Main Branch Flowで使用するWork Branchは、`main`から分岐し`main`へ統合する一時Branchとして定義する |
| Requirement | MUST |
| Source | Branch Convention (BR-BS-LC-001), Project Conventions |

**Reason:**

独立した作業単位の変更を`main`から隔離する必要がある場合に、一貫した分岐元・統合先を持つBranchとして扱うため。

**Notes:**

- 役割：独立した作業単位の変更を`main`から隔離する
- 分岐元：`main`
- 統合先：`main`
- 作成条件：変更の隔離、段階的作業、差分確認、CI確認などが必要な場合
- Base Branch Convention上のWork Branch定義（`BR-BS-LC-001`）に基づく一時Branchとして分類する
- 個々の作業でWork Branchを使用するかどうかは、`BR-MB-CP-001`〜`BR-MB-CP-003`が定める。GitHub Project管理作業では使用がMUSTとなる（`BR-MB-CP-002`）

---

### BR-MB-MS-003: Exclude Additional Persistent Branches（追加の永続Branchを使用しない）

| 項目 | 内容 |
| --- | --- |
| Rule | Main Branch Flowでは、`main`以外の永続Branchを使用しない |
| Requirement | MUST |
| Source | Project Conventions |

**Reason:**

`develop`、release Branch、保守Branchなどの追加永続Branchは、`main`を唯一の永続Branchとする本Modelの基本構造と矛盾するため。

**Notes:**

- 使用しないBranch：`develop`、release Branch、hotfix専用Branch、保守Branch、次期バージョン開発用の永続Branch
- 緊急変更専用のhotfix経路は設けない。緊急変更も、`main`への直接変更またはWork Branchから`main`への統合のいずれかを使用する
- Repository固有の事情により、`main`以外の永続Branchまたは本書で定義していない変更経路が必要な場合は、Repository Conventionではなく新しいBranching Modelとして定義する

---

## Change Path（変更経路）

### BR-MB-CP-001: Allow Direct Main Changes（mainへの直接変更を許可する）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理しない作業については、`main`への直接Commit／Pushを許可する |
| Requirement | MAY |
| Source | Project Conventions |

**Reason:**

GitHub Projectで管理しない小規模な変更まで一律にWork Branchへ隔離すると、`main`を正本かつ通常の作業場所とする本Modelの前提と矛盾するため。

**Notes:**

- GitHub Project管理作業には適用しない。Project管理作業は`BR-MB-CP-002`に従う
- `main`への直接Commit／Pushを禁止するBranch Protectionは、本Modelの標準設定として要求しない
- Force Push禁止、Branch削除禁止、Status Checkなど、直接Commitを妨げない保護設定の利用は妨げない
- `main`へ採否未確認の変更を無制限に置くことを許可する趣旨ではない

---

### BR-MB-CP-002: Integrate Project-Managed Work（Project管理作業の統合経路）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理する作業は、Task IssueをGitHub Projectへ登録し、`main`から分岐したWork Branchを作成し、Pull Requestを使用して`main`へ統合する |
| Requirement | MUST |
| Source | GitHub Project Convention (GP-BS-MW-001), Branch Convention (BR-BS-BM-004) |

**Reason:**

GitHub Project管理作業では`main`への直接Commitによる完了を防ぎ、Work Branchの分岐元・統合先および対応関係を一貫させるため。

**Notes:**

- Work Branchは`main`から分岐する
- Work Branchの統合先は`main`
- Pull Requestを必須とする
- `main`への直接CommitでGitHub Project管理Taskを完了しない
- Work BranchはMerge後に削除する（`BR-MB-LC-001`に従う）
- Task Issue・Work Branch・Pull Requestの対応は、GitHub Project Convention（`GP-BS-MW-001`）およびBase Branch Convention（`BR-BS-BM-004`）に従う
- GitHub Project ConventionのStatus・Review・Done Ruleは本書で複製しない

---

### BR-MB-CP-003: Integrate Project-Unmanaged Work Branches（Project管理外Work Branchの統合）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectで管理しないWork Branchを`main`へ統合する場合は、Pull Requestを使用する |
| Requirement | SHOULD |
| Source | Project Conventions |

**Reason:**

レビュー可能性と変更履歴の一貫性を保ちつつ、Project管理外作業まで一律に必須化しないことで運用上の柔軟性を維持するため。

**Notes:**

- Pull Requestを使用しない統合も許可される
- Pull Requestを使用しない場合でも、統合前に差分を確認する
- Pull Requestを使用しない場合の具体的なGit操作手順は本書で定義しない
- 継続的にPull Request必須へ厳格化する場合は、Repository Conventionで定義できる
- GitHub Project管理作業ではこの任意性を適用せず、GitHub Project Conventionに従ってPull Requestを必須とする（`BR-MB-CP-002`）

---

## Issue Relationship（Issueとの関係）

### BR-MB-IS-001: Allow Project-Unmanaged Task Issues（Project未登録Task Issueを許可する）

| 項目 | 内容 |
| --- | --- |
| Rule | GitHub Projectへ登録していないTask Issueは、Work Branchの有無にかかわらず作成・完了できる |
| Requirement | MAY |
| Source | Branch Convention (BR-BS-BM-004), Project Conventions |

**Reason:**

Task Issueの作成とGitHub Projectでの管理は独立した判断であり、Project管理外の作業まで一律にProject登録やWork Branchを要求しないため。

**Notes:**

- Project未登録Task IssueはWork Branchなしで完了できる
- Project未登録Task IssueにWork Branchを対応させることもできる
- Task IssueとWork Branchを対応させる場合は、Base Branch Convention（`BR-BS-BM-004`）の1対1原則に従う
- Project登録済みTask IssueにはWork Branchを必須とする（`BR-MB-CP-002`）
- Epic／Feature／Taskの意味はGitHub Project Setupを参照し、本書で再定義しない

---

### BR-MB-IS-002: Allow Issue-Free Work Branches（IssueなしWork Branchを許可する）

| 項目 | 内容 |
| --- | --- |
| Rule | Task Issueと対応しないWork Branchの作成を許可する |
| Requirement | MAY |
| Source | Branch Convention (BR-BS-LC-001), Project Conventions |

**Reason:**

Issueを起票するほどではない作業でも、変更を隔離する目的でWork Branchを使用できるようにするため。

**Notes:**

- IssueなしWork Branchは、GitHub Projectで管理する作業には該当しない
- 命名は`BR-MB-NM-001`に従う

---

## Branch Naming（Branch命名）

### BR-MB-NM-001: Name Work Branches（Work Branchを命名する）

| 項目 | 内容 |
| --- | --- |
| Rule | Work Branch名は、Task Issueと対応しない場合は`<type>/<short-description>`、Task Issueと対応する場合は`<type>/<issue-number>-<short-description>`の形式とする |
| Requirement | MUST |
| Source | Branch Convention (BR-BS-NM-001, BR-BS-NM-002), Commit Convention, Project Conventions |

**Reason:**

Issueの有無に応じて、Work Branch名からIssueとの対応関係と作業目的の両方を識別できるようにするため。

**Examples:**

```text
docs/update-branch-convention
chore/update-label-template
docs/123-update-project-convention
```

**Notes:**

- Task Issueと対応する場合はIssue番号を含める
- IssueなしWork BranchにはIssue番号を含めない
- `<type>`はCommit Conventionで採用しているTypeから選択する
- `<short-description>`は小文字のkebab-caseとする
- 使用文字はBase Branch Convention（`BR-BS-NM-001`）の制約に従う
- Branch名から作業目的を識別できるようにする（`BR-BS-NM-002`）

---

## Branch Lifecycle（Branchライフサイクル）

### BR-MB-LC-001: Complete Work Branch Lifecycle（Work Branchライフサイクルの完了）

| 項目 | 内容 |
| --- | --- |
| Rule | Work Branchは、`main`への統合または作業中止のいずれかをもって目的完了とし、完了後は速やかに削除する |
| Requirement | MUST |
| Source | Branch Convention (BR-BS-LC-002, BR-BS-LC-003), Project Conventions |

**Reason:**

明確な終了条件を持たせ、Base Branch Conventionの一時Branchライフサイクル完了原則（`BR-BS-LC-003`）に従って不要なWork Branchの残存を防ぐため。

**Notes:**

- 終了条件：`main`への統合、または作業中止
- 終了後：削除
- 削除以外の保持・アーカイブ扱いは本Modelの標準では定義しない。必要な場合はRepository Conventionで定義する

---

## Branch Protection（Branch保護方針）

Main Branch FlowにおけるBranch Protectionの方針は次のとおりとする。

- `main`への直接Commit／Pushを許可する（`BR-MB-MS-001`、`BR-MB-CP-001`）
- Pull Requestを必須とするBranch Protectionは、本Modelの標準設定として要求しない
- GitHub Project管理作業については、運用RuleとしてPull Requestを必須とする（`BR-MB-CP-002`）。これはBranch Protectionの設定ではなく、運用Ruleとして扱う
- Force Push禁止、Branch削除禁止、Status Checkなど、直接Commitを妨げない保護設定は利用できる
- Repository Conventionは、`main`への直接Commitを全面禁止してはならない。全面禁止は本Modelの中心的構造を変更することになるため、新しいBranching Modelとして扱う

---

## Review Checklist（レビューチェックリスト）

- [ ] Repository ManifestでMain Branch Flowが選択されているか
- [ ] `main`が唯一の永続Branchとして使用されているか
- [ ] Work Branchが`main`から分岐し、`main`へ統合されているか
- [ ] GitHub Project管理作業でTask Issue・Work Branch・Pull Requestが使用されているか
- [ ] GitHub Project管理作業を`main`への直接Commitで完了していないか
- [ ] Project管理外のTask IssueまたはIssueなし作業が、Main Branch Flowで許可された経路を使用しているか
- [ ] Task IssueとWork Branchを対応させる場合に1対1になっているか
- [ ] Work Branch名がIssueの有無に応じた形式になっているか
- [ ] Work Branchが統合または作業中止後に削除されているか
- [ ] `main`以外の永続Branchや未定義の変更経路を使用していないか
