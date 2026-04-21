# リポジトリ規約

本ドキュメントは、リポジトリの設定・構成・管理に関するルールを定義します。
新規リポジトリの作成時およびリポジトリ設定の変更時に参照してください。

---

## 目次

1. [命名規則](#1-命名規則)（[リポジトリ名](#1-1-リポジトリ名) / [ブランチ名](#1-2-ブランチ名)→WORKFLOW_CONVENTION参照）
2. [初期設定チェックリスト](#2-初期設定チェックリスト)
3. [Rulesets](#3-rulesets)
4. [CODEOWNERS](#4-codeowners)
5. [Issueラベル](#5-issueラベル)
6. [GitHub Actions](#6-github-actions)
7. [シークレット・環境変数](#7-シークレット環境変数)
8. [フォルダ構成](#8-フォルダ構成)

---

## 1. 命名規則

### 1-1. リポジトリ名

```text
{prefix}-{kebab-case-description}
```

| Prefix | 用途 |
| --- | --- |
| `app-` | アプリケーション本体 |
| `template-` | テンプレートリポジトリ |
| `lib-` | 共有ライブラリ・パッケージ |
| `infra-` | インフラ・IaC構成 |
| `docs-` | ドキュメントサイト |

#### ルール

- リポジトリ名は**名詞（モノの名前）**で表現します
- 動詞（`add` / `create` / `update` など）は含めません
- `{description}` 部分は kebab-case（小文字・ハイフン区切り）で記述します

#### 例

```text
app-news-aggregator
template-devenv-payload-monolith
lib-ui-components
infra-vps-setup
```

---

### 1-2. ブランチ名

ブランチの命名規則・Type一覧は [WORKFLOW_CONVENTION.md](./WORKFLOW_CONVENTION.md#2-branch) を参照してください。

---

## 2. 初期設定チェックリスト

新規リポジトリ作成後に以下を設定します。

### General

#### Features

- [ ] `Wikis` は任意（ドキュメントは `docs/` で管理するため基本不要）
- [ ] `Issues` を有効化する
- [ ] `Discussions` を無効化する
- [ ] `Projects` を有効化する
- [ ] `Pull requests` を有効化する
- [ ] `Pull request permissions` を `Collaborators only` に設定する

#### Pull Requests

- [ ] `Allow merge commits` を無効化する
- [ ] `Allow squash merging` を有効化する
- [ ] `Allow rebase merging` を無効化する
- [ ] `Automatically delete head branches` を有効化する

#### Issues

- [ ] `Auto-close issues with merged linked pull requests` を有効化する

### Collaborators and teams

- [ ] 必要なメンバー・チームにアクセス権を付与する

### Rulesets

- [ ] Rules → Rulesets → New branch ruleset で `Protect main` を作成する（詳細は [Rulesets](#3-rulesets) を参照）

### Issueラベル

- [ ] デフォルトラベルを削除する
- [ ] [Issueラベル](#5-issueラベル) を作成する（`Sync Labels` ワークフローを使用）

### GitHub Projects

- [ ] プロジェクトを作成する（または既存のプロジェクトを使用する）
- [ ] リポジトリをプロジェクトに紐付ける（Project → Settings → Linked repositories）
- [ ] `Auto-add to project` workflowのフィルターにリポジトリを指定する（詳細は下記）
- [ ] Workflows の有効/無効を [PROJECT_CONVENTION.md](./PROJECT_CONVENTION.md) の設定に従って確認する

#### Auto-add to project のフィルター設定

Project → Workflows → Auto-add to project を開き、以下のフィルターを設定します。

```text
repository:<オーナー名>/<リポジトリ名> is:issue is:open has:label
```

#### GitHub Projectsの例

```text
repository:username/app-news-aggregator is:issue is:open has:label
```

> 複数リポジトリを同一プロジェクトで管理する場合は `OR` でつなぎます。
>
> ```text
> repository:username/app-news-aggregator OR repository:username/app-another is:issue is:open has:label
> ```

---

## 3. Rulesets

`main` ブランチに対して以下のRulesetを設定します。

Rules → Rulesets → New ruleset → **New branch ruleset** で作成します。

### 設定値

| 項目 | 設定値 |
| --- | --- |
| Ruleset name | `Protect main` |
| Enforcement status | `Active` |
| Target branches | `Include default branch` |
| Restrict deletions | ✅ |
| Require linear history | ✅ |
| Require a pull request before merging | ✅ |
| └─ Required approvals | `0`（個人開発のため無効） |
| └─ Dismiss stale pull request approvals when new commits are pushed | ✅ |
| └─ Require review from Code Owners | ❌（個人開発のため無効。チーム開発移行時に有効化を検討） |
| └─ Allowed merge methods | Squash のみ有効（Merge・Rebase は無効） |
| Require status checks to pass | ❌（個人開発のため無効。`ci-pr.yml` のチェックを必須化する場合は有効化を検討） |
| Block force pushes | ✅ |

---

## 4. CODEOWNERS

`.github/CODEOWNERS` で各ディレクトリのオーナーを定義します。

### 記述形式

```text
# パス  オーナー（GitHubユーザー名 or チーム名）
*                   @username
/docs/              @username
/src/components/    @username
```

### 運用ルール

- 全ファイルのデフォルトオーナーを `*` で指定します
- ディレクトリごとに必要に応じてオーナーを上書きします
- オーナーはPR作成時に自動でレビュワーとしてリクエストされます

---

## 5. Issueラベル

ラベルは `type:` カテゴリのみを使用します。Status・Priorityの管理はGitHub Projectsのフィールドで行うため、ラベルでは管理しません。

ラベルの定義は `.github/labels.yml` で管理し、`Sync Labels` ワークフローで同期します。

> **配置について**
> `labels.yml` はGitHubが自動参照する特殊ファイルではありませんが、GitHub運用に関する設定ファイルとして `.github/` に配置します。`docs/` はドキュメント、`config/` は別途設けないという方針から、`.github/` への配置を例外的な措置として採用しています。

### 5-1. ラベル一覧

| ラベル名 | カラー | 説明 | 対応Layer |
| --- | --- | --- | --- |
| `type:epic` | `#5319e7` | 複数の機能やタスクをまとめた単位 | Epic |
| `type:feature` | `#1d76db` | 特定の機能を実現する単位 | Feature |
| `type:task` | `#0e8a16` | 具体的な実装や対応を行う単位 | Task |
| `type:bug` | `#d73a4a` | 予期しない動作・エラーの報告 | — |
| `type:enhancement` | `#e4c442` | 既存の機能・仕様・構成などの改善提案 | — |

> `type:bug` と `type:enhancement` はProjectのLayerに対応しない例外ラベルです。対応規模に応じてLayerフィールドを別途設定してください。

### 5-2. labels.yml の形式

`.github/labels.yml` に以下の形式で定義します。

```yaml
- name: "type:epic"
  color: "5319e7"
  description: "複数の機能やタスクをまとめた単位"

- name: "type:feature"
  color: "1d76db"
  description: "特定の機能を実現する単位"

- name: "type:task"
  color: "0e8a16"
  description: "具体的な実装や対応を行う単位"

- name: "type:bug"
  color: "d73a4a"
  description: "予期しない動作・エラーの報告"

- name: "type:enhancement"
  color: "e4c442"
  description: "既存の機能・仕様・構成などの改善提案"
```

---

## 6. GitHub Actions

### 6-1. ワークフローファイルの命名規則

```text
.github/workflows/{目的}-{トリガー}.yml
```

#### 6-1. ワークフローファイルの命名規則の例

```text
ci-pr.yml            # CIチェック（PR時）
label-pr.yml         # PRの自動ラベリング
label-issue.yml      # Issueの自動ラベリング
release-draft.yml    # ドラフトリリースの生成
label-sync.yml       # ラベルの同期
```

### 6-2. 標準ワークフロー

| ワークフロー | トリガー | 内容 |
| --- | --- | --- |
| `ci-pr.yml` | PR（作成・編集・同期・再オープン） | PRタイトル・ブランチ名を検証 |
| `label-sync.yml` | 手動（`workflow_dispatch`） | `labels.yml` からラベルを同期 |
| `release-draft.yml` | 手動（`workflow_dispatch`） | ドラフトリリースを生成 |

#### `ci-pr.yml`

- **トリガー**：PR作成・編集・同期・再オープン時
- **処理**：以下の2項目を検証する
  - **PRタイトル**：`<gitmoji> <type>(<scope>): <subject>` 形式であること。gitmoji・typeはコミット規約の対応表に従う
  - **ブランチ名**：命名規則（`<type>/<issue番号>-<description>` など）に従っていること
- **検証失敗時**：CIチェックが失敗しマージがブロックされる（Rulesets で `Require status checks to pass` を有効化後）

#### `label-sync.yml`

- **トリガー**：手動（`workflow_dispatch`）
- **処理**：`.github/labels.yml` の定義をリポジトリのIssueラベルに同期する。定義にないラベルは作成、差異があるラベルは更新、定義にないラベルは削除する
- **用途**：ラベルの初期設定・定義変更後の反映

#### `release-draft.yml`

- **トリガー**：手動（`workflow_dispatch`）
- **入力パラメータ**：
  - `version`：リリースバージョン（例: `1.2.0` または `v1.2.0`）
  - `previous_tag`：前回タグ（空欄で自動検出）
- **処理**：前回タグ以降にmainへマージされたPRをタイトルのtypeでカテゴリ分類し、ドラフトリリースを作成する。BREAKING CHANGEはPRテンプレートのチェックボックスで検出する
- **出力**：GitHubのReleasesにドラフトリリースが作成される
- **用途**：リリースノートの生成（詳細は `WORKFLOW_CONVENTION.md` 5-3・5-4 を参照）

### 6-3. 使用するシークレット

| シークレット名 | 用途 |
| --- | --- |
| `GITHUB_TOKEN` | GitHub Actions標準トークン（自動付与） |
| `CR_PAT` | GHCR（GitHub Container Registry）へのpull用PAT |

> `GITHUB_TOKEN` はGHCRへのpullには使用できません。VPS側からGHCRイメージをpullする際は `CR_PAT`（Personal Access Token）を使用してください。

---

## 7. シークレット・環境変数

### 7-1. 管理方針

- シークレットはGitHubの `Settings > Secrets and variables > Actions` で管理します
- `.env` ファイルをリポジトリにコミットしません
- `.env.example` に変数名のみ（値は空）を記載してリポジトリで管理します

### 7-2. 環境の分離

| 環境名 | 用途 |
| --- | --- |
| `staging` | ステージング環境用のシークレット |
| `production` | 本番環境用のシークレット |

### 7-3. 命名規則

```text
{カテゴリ}_{名前}
```

#### 7-3. 命名規則の例

```text
DATABASE_URI
NEXTAUTH_SECRET
CR_PAT
RESEND_API_KEY
```

---

## 8. フォルダ構成

リポジトリのルートには以下のフォルダ・ファイルを配置します。

```text
{repository-root}/
├── .github/
│   ├── CONTRIBUTING.md           # 開発参加規定
│   ├── CODEOWNERS                # コードオーナー定義
│   ├── CODE_OF_CONDUCT.md        # 行動規範（個人開発のため最小構成）
│   ├── FUNDING.yml               # スポンサーシップ設定
│   ├── SECURITY.md               # セキュリティポリシー
│   ├── SUPPORT.md                # サポート窓口（個人開発のため最小構成）
│   ├── labels.yml                # Issueラベル定義（※GitHubの自動参照対象外・例外配置）
│   ├── ISSUE_TEMPLATE/
│   │   ├── config.yml            # テンプレート選択画面の設定
│   │   ├── epic.yml
│   │   ├── feature.yml
│   │   ├── task.yml
│   │   ├── bug-report.yml
│   │   └── enhancement.yml
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       ├── ci-pr.yml             # CIチェック（PR時）
│       ├── label-sync.yml        # ラベル同期
│       └── release-draft.yml     # ドラフトリリース生成
└── docs/
    ├── COMMIT_CONVENTION.md
    ├── WORKFLOW_CONVENTION.md
    ├── PROJECT_CONVENTION.md
    └── REPOSITORY_CONVENTION.md
```
