# GitHub Project Setup（GitHubプロジェクト構築仕様）

## Purpose（目的）

本書は、GitHub Projectsを構築するための標準仕様を定義する。

GitHub Project Setupは、共通のProject構造・Field定義・Repository連携を一貫した形で整えることを目的とする。

---

## Scope（適用範囲）

本書は、GitHub Projectsの初期構築時に行う設計・構成・確認に適用する。

以下は本書の対象外とする。

- GitHub UIの操作手順・画面遷移
- Issue・Pull Requestの運用ルール → 各リポジトリのドキュメント
- Automation・Workflowの詳細仕様 → 別途Specification
- 個別プロジェクト固有のField・View追加ルール

---

## GitHub Project Setup Phases（構築フェーズ）

GitHub Project Setupは、以下の3フェーズで行う。

```text
Design
  ↓
Build
  ↓
Validate
```

---

## Phase 1 — Design（設計）

GitHub Projectsを構築する前に、必要な設計判断を行う。

### Project Structure（プロジェクト構造）

GitHub Projectsで管理するIssueは、以下の階層構造を基本とする。

```text
Epic
  └── Feature
        └── Task
```

**Epic:**

複数のFeatureを束ねる大きな開発テーマ・目標を表す。

**Feature:**

Epicを構成する機能単位・成果物単位を表す。

**Task:**

実際の作業単位を表す。最小のトラッキング粒度である。

**Parent-Child Relationship（親子関係）:**

EpicとFeature、FeatureとTaskの親子関係はSub-issueで管理する。Issue本文への親Issue記載は行わない。

**Task-only Operation（Taskのみの運用）:**

EpicやFeatureを使わず、Taskのみで運用することを許容する。プロジェクトの規模・性質に応じて判断する。

---

### Standard Project Fields（標準プロジェクトフィールド）

すべてのGitHub Projectsで共通して使用するFieldを以下に定義する。

#### Status（ステータス）

| 値 | 意味 |
| --- | --- |
| `Backlog` | 着手待ち。スコープは決まっているが、まだ着手できる状態ではない |
| `Ready` | 着手可能。作業を開始できる状態にある |
| `In Progress` | 作業中 |
| `Review` | 作業完了、レビュー待ち |
| `Done` | 完了 |
| `Blocked` | 外部依存・問題により作業が停止している |

#### Status Transition（ステータス遷移）

基本フロー:

```text
Backlog → Ready → In Progress → Review → Done
```

`Blocked` は `In Progress` または `Review` から遷移する一時状態であり、解消後は `In Progress` または `Ready` に戻る。

| 遷移 | 条件 |
| --- | --- |
| Backlog → Ready | スコープが明確になり、着手可能と判断した場合 |
| Ready → In Progress | 作業を開始した場合 |
| In Progress → Review | 作業が完了し、レビューに出した場合 |
| In Progress → Blocked | 外部依存・問題により作業が停止した場合 |
| Review → Done | レビューが承認された場合 |
| Review → In Progress | 修正が必要と判断された場合 |
| Review → Blocked | レビュー中に外部依存・問題が発生した場合 |
| Blocked → In Progress | ブロッカーが解消され、作業を再開した場合 |
| Blocked → Ready | ブロッカーが解消されたが、まだ着手しない場合 |

#### Priority（優先度）

| 値 | 意味 |
| --- | --- |
| `High` | 高優先度。他の作業より先に着手する |
| `Medium` | 中優先度。通常の順序で着手する |
| `Low` | 低優先度。他の作業が完了してから着手する |

---

### Project Design Principles（プロジェクト設計原則）

- 標準Fieldを基本とし、必要が明確になった場合のみFieldを追加する。
- 親子関係はSub-issueのみで表現し、Issue本文に記載しない。
- Projectは1つ以上のRepositoryに連携する。

---

## Phase 2 — Build（構築）

Designで決定した内容に基づき、GitHub Projectsの初期構成を作成する。

### Configure Project（プロジェクトの構成）

以下の要素を標準仕様に従い構成する。

- StatusフィールドをStandard Project Fieldsの定義に従い設定する
- PriorityフィールドをStandard Project Fieldsの定義に従い設定する

### Connect Repositories（リポジトリの連携）

Projectに連携するRepositoryを設定する。

- 管理対象のIssueが存在するRepositoryを連携する
- 複数Repositoryにまたがる場合はすべて連携する

---

## Phase 3 — Validate（確認）

構築後、GitHub Projectsが標準仕様どおり構成されているか確認する。

### Review Checklist（確認項目）

- [ ] StatusフィールドがStandard Project Fieldsの定義と一致しているか
- [ ] PriorityフィールドがStandard Project Fieldsの定義と一致しているか
- [ ] 管理対象のRepositoryが連携されているか
- [ ] Issue階層（Epic・Feature・Task）が必要に応じて定義されているか
- [ ] 親子関係がSub-issueで管理されているか
- [ ] 標準仕様にない独自Fieldを不必要に追加していないか

---

## Notes（補足）

GitHub Project Setupは初期構築のみを対象とする。

運用開始後の変更は、GitHub Project Setupではなく、適切なConvention・または個別リポジトリのドキュメントで管理する。
