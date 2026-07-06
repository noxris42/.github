# standard（標準Pull Request Template）

本ディレクトリは、個人アカウント全体で使用する標準Pull Request Templateを管理する。

特定の用途・リポジトリ種別を前提とせず、あらゆるRepositoryで利用できる最小共通構成としている。各Repositoryはこのstandardをベースとしてコピーし、必要に応じて編集して利用する。

## 設計思想

本TemplateはIssue駆動運用を前提とする。PRは関連Issueを実現した変更をレビューするための成果物であり、Issueの内容を重複して記載しない。

```text
Issue（何をするか）
    ↓
Branch
    ↓
Commit
    ↓
Pull Request（Issueをどう実現したか）
    ↓
Merge
```

| 情報の種類 | 管理場所 |
| --- | --- |
| 目的・背景・完了条件 | Issue |
| 変更内容のSummary | PR本文 |
| レビュー担当者・ラベル・Project | GitHub UI |

## 構成

| ファイル | 用途 |
| --- | --- |
| `PULL_REQUEST_TEMPLATE.md` | 標準PR Template |

## 配置先

```text
templates/pull-request-templates/standard/PULL_REQUEST_TEMPLATE.md
→ <repository>/.github/PULL_REQUEST_TEMPLATE.md
```

## 派生について

将来、特定の用途（Software開発など）に固有のInputが必要になった場合は、standardを基底としてディレクトリを派生させる。

```text
standard/
    ↓
software/
```

standardそのものは変更せず、派生先で差分のみを追加する。
