# リポジトリ共通設定・開発規約

開発規約・テンプレート集です。
このリポジトリの内容は、各リポジトリに共通の Issue テンプレート・PR テンプレート・規約ドキュメントとして機能します。

---

## このリポジトリの役割

- **Issue / PR テンプレート** を各リポジトリに提供する
- **開発規約ドキュメント** を一元管理する
- **GitHub Actions ワークフロー**（ラベル同期など）を管理する

---

## ドキュメント

| ドキュメント | 内容 |
| --- | --- |
| [CONTRIBUTING.md](.github/CONTRIBUTING.md) | 開発参加規定・規約ナビゲーション |
| [WORKFLOW_CONVENTION.md](docs/WORKFLOW_CONVENTION.md) | ブランチ・Issue・PR・リリースの運用フロー |
| [COMMIT_CONVENTION.md](docs/COMMIT_CONVENTION.md) | コミットメッセージのフォーマット・ルール |
| [PROJECT_CONVENTION.md](docs/PROJECT_CONVENTION.md) | GitHub Projects の階層構造・フィールド・自動化 |
| [REPOSITORY_CONVENTION.md](docs/REPOSITORY_CONVENTION.md) | リポジトリ設定・Rulesets・ラベル・Actions |

---

## Issue テンプレート

| テンプレート | プレフィックス | 用途 |
| --- | --- | --- |
| `epic.yml` | `【Epic】` | 複数の機能をまとめる大項目 |
| `feature.yml` | `【Feat】` | 特定の機能を実現する単位 |
| `task.yml` | `【Task】` | 具体的な実装・作業の単位 |
| `bug-report.yml` | `【Bug】` | 予期しない動作・エラーの報告 |
| `enhancement.yml` | `【Enh】` | 機能・仕様・構成などの改善提案 |

Issue 作成後は、Project 上で **Layer / Area / Priority** を設定してください。

---

## Issueラベル

`type:` カテゴリのみを使用します。Status・Priority の管理は GitHub Projects のフィールドで行います。

| ラベル | 説明 |
| --- | --- |
| `type:epic` | 複数の機能やタスクをまとめた単位 |
| `type:feature` | 特定の機能を実現する単位 |
| `type:task` | 具体的な実装や対応を行う単位 |
| `type:bug` | 予期しない動作・エラーの報告 |
| `type:enhancement` | 既存の機能・仕様・構成などの改善提案 |

ラベルの定義は `.github/labels.yml` で管理し、`Sync Labels` ワークフローで同期します。

---

## コミットメッセージの基本形

```text
<gitmoji> <type>(<scope>): <subject>

# Why
<変更の背景・目的（省略可）>

# What
- <変更内容>

Refs: #<issue番号>
```

### Gitmoji + Type 対応表（抜粋）

| Gitmoji | Type | 用途 |
| --- | --- | --- |
| ✨ | `feat` | 新機能 |
| 🐛 | `fix` | バグ修正 |
| 📝 | `docs` | ドキュメントのみの変更 |
| ♻️ | `refactor` | リファクタリング |
| 🔧 | `chore` | 設定・ツール・ファイル削除 |
| 📦 | `build` | 依存関係・パッケージの変更 |
| 👷 | `ci` | CI/CD の設定変更 |

全 Type 一覧は [COMMIT_CONVENTION.md](docs/COMMIT_CONVENTION.md) を参照してください。

---

## 開発フロー（概要）

```text
Issue 作成
  └─ ブランチ作成（type/{issue番号}-{説明}）
       └─ 実装・コミット
            └─ PR 作成
                 └─ レビュー・CI 通過
                      └─ Squash merge → main
                           └─ ブランチ削除 → Issue クローズ（自動）
```

### ブランチ命名規則

```text
feature/42-google-oauth
fix/88-token-race-condition
docs/12-update-readme
chore/5-setup-eslint
```

### PR タイトル規則（コミットと同フォーマット）

```text
✨ feat(auth): Google OAuthログインを追加
🐛 fix(auth): トークン検証の競合状態を修正
```

詳細は [WORKFLOW_CONVENTION.md](docs/WORKFLOW_CONVENTION.md) を参照してください。

---

## ファイル構成

```text
.github/
├── CONTRIBUTING.md
├── CODEOWNERS
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── SUPPORT.md
├── FUNDING.yml
├── labels.yml
├── ISSUE_TEMPLATE/
│   ├── config.yml
│   ├── epic.yml
│   ├── feature.yml
│   ├── task.yml
│   ├── bug-report.yml
│   └── enhancement.yml
├── PULL_REQUEST_TEMPLATE.md
└── workflows/
    ├── ci-pr.yml
    ├── label-sync.yml
    └── release-draft.yml
docs/
├── WORKFLOW_CONVENTION.md
├── COMMIT_CONVENTION.md
├── PROJECT_CONVENTION.md
└── REPOSITORY_CONVENTION.md
```

---

## はじめに確認すること

新しくリポジトリに参加する場合は、以下の順番でドキュメントを確認してください。

1. [WORKFLOW_CONVENTION.md](docs/WORKFLOW_CONVENTION.md) — ブランチの切り方・Issue の立て方・PR の出し方
2. [COMMIT_CONVENTION.md](docs/COMMIT_CONVENTION.md) — コミットメッセージの書き方
3. [PROJECT_CONVENTION.md](docs/PROJECT_CONVENTION.md) — GitHub Projects の使い方
4. [REPOSITORY_CONVENTION.md](docs/REPOSITORY_CONVENTION.md) — リポジトリ設定・フォルダ構成（主に管理者向け）
