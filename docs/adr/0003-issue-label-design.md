# 0003. Issueラベルの設計

日付：2025-04-14
状態：採用

---

## 背景

IssueにどのようなラベルをつけてStatus・Priority・Typeを管理するか方針を決める必要があった。また、ラベル名のフォーマット（スペースの有無）についても統一が必要だった。

## 決定

- ラベルは **`type:` カテゴリのみ** を使用する（5種類）
- Status・Priorityの管理は **GitHub Projectsのフィールド** で行う
- ラベル名は **スペースなし形式**（`type:epic` / `type:feature` 等）を採用する

| ラベル名 | 説明 |
| --- | --- |
| `type:epic` | 複数の機能やタスクをまとめた単位 |
| `type:feature` | 特定の機能を実現する単位 |
| `type:task` | 具体的な実装や対応を行う単位 |
| `type:bug` | 予期しない動作・エラーの報告 |
| `type:enhancement` | 既存の機能・仕様・構成などの改善提案 |

## 理由

**`type:` のみ採用**：StatusとPriorityはGitHub Projectsで一元管理するため、ラベルで重複管理する必要がない。ラベルの役割をIssueの種別識別に絞ることで管理対象を最小化できる。

**スペースなし形式**：ラベル名にスペースが含まれると、GitHubのフィルター構文でクォートが必要になり（`label:"type: epic"`）、URLエンコードも必要な場面が増える。スペースなし（`label:type:epic`）の方が扱いやすい。

**`type:feature` と `type:enhancement` の分離**：`type:feature` は新規機能、`type:enhancement` は既存機能の改善・拡張と役割を分離した。

## 却下した案

**`status:` / `priority:` ラベルも使用する案**：ラベルとProjectsフィールドで二重管理が発生し、同期コストが高くなるため却下。

**スペースあり形式（`type: epic`）**：フィルター・API・自動化スクリプトでの扱いが煩雑になるため却下。

**`type:feature` と `type:enhancement` を統合**：新規機能と改善を区別できた方が進捗管理の粒度が上がると判断し分離を維持した。

## 影響・注意点

- `type:bug` と `type:enhancement` はProjectの `Layer` フィールドに対応しないため、Issue作成後にLayerを手動設定する必要がある
- `Auto-add to project` のフィルターに `has:label` を使用しているため、Issue作成時にラベルが付与されないとProjectに追加されない。`config.yml` の `blank_issues_enabled: false` と組み合わせて運用する
- ラベルの定義は `.github/labels.yml` で管理し、`Sync Labels` ワークフローで同期する
