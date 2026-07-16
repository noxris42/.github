# label-sync（ラベル同期呼び出し側Workflow）

本ディレクトリは、`noxris42/.github` が提供するLabel Sync Reusable Workflowを、個別リポジトリから呼び出すためのWorkflow Templateを管理する。

Reusable Workflow本体は `.github` リポジトリ自身の `.github/workflows/sync-labels.yml` として実装され、本Templateはそれを呼び出す個別リポジトリ側のエントリポイントのみを提供する。

## 構成

| ファイル | 用途 |
| --- | --- |
| `sync-labels.yml` | Label Sync Reusable Workflowを手動実行するための呼び出し側Workflow |

## 配置先

```text
templates/workflows/label-sync/sync-labels.yml
→ .github/workflows/sync-labels.yml
```

## 前提

- 個別リポジトリが独自のラベル体系を必要とする場合は `.github/labels.yml` を配置する。存在しない場合は `noxris42/.github` の共通ラベル定義が使用される
- 手動実行（`workflow_dispatch`）のみに対応し、push・pull_request・scheduleによる自動実行は行わない
