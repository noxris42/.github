# Repository Setup（リポジトリ構築仕様）

## Purpose（目的）

本書は、個別リポジトリを構築するための標準プロセスを定義する。

Repository Setupは、共通ConventionとTemplate部品を利用し、リポジトリの初期構成を一貫した形で整えることを目的とする。

---

## Scope（適用範囲）

本書は、リポジトリの初期構築時に行う設計・構築・確認に適用する。

以下は本書の対象外とする。

- Template部品そのものの構造 → `docs/architecture/template.md`
- Convention本文の定義 → `docs/conventions/`
- GitHub Projectの詳細設定
- 個別リポジトリ運用開始後の運用ルール

---

## Repository Setup Phases（構築フェーズ）

Repository Setupは、以下の3フェーズで行う。

```text
Design
  ↓
Build
  ↓
Validate
```

---

## Phase 1 — Design（設計）

リポジトリを構築する前に、必要な設計判断を行う。

### Repository Design Decisions（リポジトリ設計判断）

初期段階では、以下を決定する。

| 項目 | 内容 |
| --- | --- |
| Management Target | リポジトリが主に管理する対象 |
| Workflow | ブランチ・作業フロー |
| Project | GitHub Projectsを使うか |
| Visibility | private / public |
| Scope | コミットやProjectで使用するscope |

### Design Principles（設計原則）

- 必要になった設計判断のみを追加する。
- Template選択または構築手順に影響しない項目は追加しない。
- 新しいリポジトリ種別・作業フロー・構築パターンが必要になった場合は、個別リポジトリへ適用する前に `.github` リポジトリで設計する。
- Scopeはリポジトリ構築時に定義し、Commit・Project・Issue・Pull Requestで一貫して使用する。

---

## Phase 2 — Build（構築）

Designで決定した内容に基づき、リポジトリの初期構成を作成する。

### Select Template Components（Template部品の選択）

Repository Design Decisionsに基づき、必要なTemplate部品を選択する。

各Design DecisionがどのTemplate部品に対応するかは、Template Selection Rulesを参照する。

### Apply Template Components（Template部品の適用）

選択したTemplate部品をリポジトリへ取得し、必要に応じて編集する。

Templateファイルの末端ファイル名は、原則として配置先のファイル名と一致する。

**Examples:**

```text
templates/labels/project/labels.yml
→ <repository>/.github/labels.yml

templates/issue-templates/documentation/task.yml
→ <repository>/.github/ISSUE_TEMPLATE/task.yml
```

### Configure Repository（リポジトリ構成）

Template適用後、リポジトリ固有の情報を設定する。

- READMEのリポジトリ名・目的を更新する
- CONTRIBUTINGの参照先を更新する
- Issue Template内の説明を必要に応じて調整する
- Scope一覧をリポジトリに合わせて定義する

### Configure GitHub（GitHub設定）

必要に応じてGitHub側の設定を行う。

- default branchを確認する
- labels同期Workflowを実行する
- GitHub Projectsを紐づける
- 必要なRepository Settingsを確認する

---

## Phase 3 — Validate（確認）

構築後、リポジトリが設計どおりに構成されているか確認する。

### Verification Checklist（確認項目）

- [ ] Repository Design Decisionsが明確になっているか
- [ ] 必要なTemplate部品が選択されているか
- [ ] Template部品が正しい配置先に適用されているか
- [ ] リポジトリ固有情報が編集されているか
- [ ] Scopeが一貫して定義されているか
- [ ] labels同期Workflowが必要に応じて利用できるか
- [ ] GitHub Projectsを使う場合、Issue Templateとラベルが整合しているか
- [ ] 不要なTemplate部品を配置していないか

---

## Notes（補足）

Repository Setupは初期構築のみを対象とする。

運用開始後の変更は、Repository Setupではなく、適切なConvention・Template・または個別リポジトリのドキュメントで管理する。
