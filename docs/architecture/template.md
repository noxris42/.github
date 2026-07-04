# Template Architecture（テンプレートアーキテクチャ）

## Purpose（目的）

本書は、`templates/` 領域の内部構造と各ディレクトリの責務を定義する。

`templates/` は、リポジトリ構築時に選択・コピー・編集して利用するTemplate部品を管理する領域である。分類軸ではなく成果物の種類によってディレクトリを構成し、再利用可能な部品を提供する。

---

## Scope（適用範囲）

本書は、`templates/` 配下のディレクトリ構成とTemplate部品の責務に適用される。

以下は本書の対象外とする。

- Templateの設計思想 → `docs/philosophy/template.md`
- Convention本文の定義 → `docs/conventions/`
- 個別Templateファイルの詳細仕様 → Specifications
- どのTemplate部品をどのリポジトリへ適用するかの判断 → Repository Setup Guide
- 個別リポジトリ固有の運用ルール → 各リポジトリのドキュメント

---

## Design Concept（設計思想）

### Artifact-Based Organization（成果物単位の管理）

`templates/` は成果物の種類によってディレクトリを構成する。成果物単位で管理することで、Template部品の再利用性と独立性を維持する。

### Obtain, Edit, and Use（取得・編集・利用）

Template部品は、リポジトリ構築時に取得し、必要に応じて編集して利用することを前提とする。Templateは完成済みの規約を提供するのではなく、編集可能な初期雛形を提供する。取得方法はコピー・参照・生成など、利用形態に応じて選択する。

---

## Directory Structure（ディレクトリ構造）

以下は初期段階における代表的な構成例である。固定の構成ではなく、Extension Policyに従い成果物の種類に応じて追加できる。

```text
templates/
├── workflows/
├── actions/
├── labels/
├── issue-templates/
├── pull-request-templates/
├── documents/
└── community/
```

---

## Template Directory Design Principles（テンプレートディレクトリ設計原則）

### Express Differences Through Directory Hierarchy（差分はディレクトリ階層で表現する）

Templateの違いは、末端ファイル名ではなくディレクトリ階層によって表現する。同じ種類のTemplate部品であっても、用途の差分はディレクトリで区別する。

### Match Terminal Filename to Deployment Destination（末端ファイル名は配置先と一致させる）

Template部品の末端ファイル名は、配置先のファイル名と一致させる。リポジトリ構築時にリネームを前提としない構成を維持する。

**Examples:**

```text
templates/
└── issue-templates/
    ├── documentation-management/
    │   └── task.yml       ← 配置先: .github/ISSUE_TEMPLATE/task.yml
    └── software-development/
        └── task.yml       ← 配置先: .github/ISSUE_TEMPLATE/task.yml
```

ディレクトリを選択してファイルをそのまま取得することで、リネーム不要で配置できる。

### Independent from Repository Setup（Repository Setupから独立した設計）

Template部品の構造はRepository Setupの判断に依存しない。Template部品は、Repository Setupがどのように部品を選択・配置するかに関わらず、単独で意味を持つ構造として設計する。

この原則はIssue Templateに限らず、Workflows・Actions・Labels・Pull Request Template・Documentsなど、すべてのTemplate部品カテゴリに共通して適用する。

---

## Directory Responsibilities（各ディレクトリの責務）

### `workflows/`（ワークフロー）

GitHub Actionsのワークフローファイルを管理する。

**Responsibility（責務）:**

- CI・CD・Releaseなどの自動化ワークフローの雛形を提供する
- 利用するリポジトリの構成に応じて編集可能な形で提供する

**Non-Responsibility（責務外）:**

- ワークフローの実行環境の管理
- リポジトリごとの自動化設定の決定

---

### `actions/`（アクション）

再利用可能なGitHub Actionsのアクション定義を管理する。

**Responsibility（責務）:**

- 複数ワークフローで共通して使用するアクションの雛形を提供する

**Non-Responsibility（責務外）:**

- アクションのデプロイや公開管理

---

### `labels/`（ラベル）

GitHub Issueラベルの設定ファイルを管理する。

**Responsibility（責務）:**

- 共通ラベル定義の雛形を提供する
- ラベルの色・名称・説明の初期値を提供する

**Non-Responsibility（責務外）:**

- ラベルのGitHubへの自動適用
- リポジトリ固有のラベル体系の決定

---

### `issue-templates/`（Issueテンプレート）

GitHub Issue Templateファイルを管理する。

**Responsibility（責務）:**

- バグ報告・機能要望・タスクなどの用途別Issue Template雛形を提供する

**Non-Responsibility（責務外）:**

- どのIssue Templateをどのリポジトリへ適用するかの決定
- リポジトリ固有のIssue運用ルールの定義

---

### `pull-request-templates/`（PRテンプレート）

GitHub Pull Request Templateファイルを管理する。

**Responsibility（責務）:**

- PR記述の一貫性を維持するためのTemplate雛形を提供する

**Non-Responsibility（責務外）:**

- PRレビュープロセスの定義
- マージ戦略の決定

---

### `documents/`（ドキュメント）

README・CONTRIBUTING・CODEOWNERSなどの文書ファイルの雛形を管理する。

**Responsibility（責務）:**

- 各文書の初期構成・プレースホルダーを提供する
- 共通Conventionへの参照リンクを含む案内文を提供する

**Non-Responsibility（責務外）:**

- Convention本文の複製
- リポジトリ固有の記述内容の決定

---

### `community/`（コミュニティ）

SECURITY・SUPPORT・CODE_OF_CONDUCTなどのGitHub Community Health Fileの雛形を管理する。

**Responsibility（責務）:**

- 公開リポジトリ向けのコミュニティ文書の雛形を提供する

**Non-Responsibility（責務外）:**

- セキュリティポリシーの内容決定
- サポート体制の設計

---

## Repository Construction（リポジトリ構築との責務分離）

Template部品の選択・組み合わせ・適用は `templates/` の責務ではない。

どのTemplate部品を採用し、どのように設定値を書き換えるかは、Repository Setup Guideで管理する。

```text
templates/     ← Template部品を管理する
    ↓
Repository Setup Guide  ← 部品の選択・組み合わせ・適用手順を定義する
    ↓
Repository     ← 初期構成が整った状態
```

Repository Setup Guideの詳細はSpecificationsで定義する。

---

## Source of Truth（正本）

TemplateはConvention本文を複製しない。

Templateが参照すべき規約は `docs/conventions/` を正本とする。

Template内に記載できる内容は以下に限定する。

- 初期雛形
- 案内文
- 共通Conventionへのリンク
- プレースホルダー

---

## Extension Policy（拡張方針）

新しいTemplateディレクトリを追加する場合は、以下をすべて満たす必要がある。

- 成果物の種類として明確に区別できる
- 既存ディレクトリでは管理できない差分がある
- Convention本文を複製しない
- 個別リポジトリ固有ルールを一般化しすぎない
- 必要に応じてADRで判断を記録する

---

## Template Lifecycle（テンプレートライフサイクル）

Template部品は以下のライフサイクルで管理する。

```text
Need Identified（必要性の特定）
        ↓
Create Template（Template部品の作成）
        ↓
Reuse（再利用）
        ↓
Repository-specific Edits（リポジトリ固有の編集）
        ↓
If Generalized（共通化できると判断した場合）
        ↓
Update Template（Template部品の更新）
```

個別リポジトリで得られた知見は、共通化できると判断した場合のみTemplateへ反映する。Template部品は運用を通じて継続的に成熟させる。

---

## Review Checklist（確認項目）

- [ ] TemplateはConvention本文を複製していないか
- [ ] ディレクトリは成果物の種類によって分類されているか
- [ ] Template部品の差分はディレクトリ階層で表現されているか
- [ ] 末端ファイル名は配置先のファイル名と一致しているか
- [ ] リネームを前提とした構成になっていないか
- [ ] Template部品はRepository Setupの判断に依存せず単独で意味を持つか
- [ ] Template部品の選択・適用の判断をTemplateに含めていないか
- [ ] 個別リポジトリ固有ルールをTemplateへ戻していないか
- [ ] 共通Conventionへの入口として機能しているか
