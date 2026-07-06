# standard（標準Issue Template）

本ディレクトリは、個人アカウント全体で使用する標準Issue Templateを管理する。

特定の用途・リポジトリ種別を前提とせず、あらゆるRepositoryで利用できる最小共通構成としている。各Repositoryはこのstandardをベースとしてコピーし、必要に応じて編集して利用する。

## 構成

| ファイル | 用途 |
| --- | --- |
| `epic.yml` | 複数のFeatureやTaskをまとめる大きな目的・テーマの単位 |
| `feature.yml` | 複数のTaskをまとめる成果物単位 |
| `task.yml` | 具体的な作業単位 |

## 配置先

```text
templates/issue-templates/standard/
→ .github/ISSUE_TEMPLATE/
```

## 派生について

将来、特定の用途（Software開発など）に固有のFieldが必要になった場合は、standardを基底としてディレクトリを派生させる。

```text
standard/
    ↓
software/
```

standardそのものは変更せず、派生先で差分のみを追加する。
