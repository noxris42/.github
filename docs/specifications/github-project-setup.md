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

GitHub Projectsで管理するIssueは、以下の階層構造を標準とする。

```text
Epic
  └── Feature
        └── Task
```

この構造は固定された必須階層ではない。プロジェクトの規模・性質に応じて、上位階層または中間階層を省略できる。

許容する構造は以下とする。

```text
Epic → Feature → Task
Epic → Task
Feature → Task
Task only
```

**Epic:**

複数のFeatureまたはTaskを束ねる、大きな開発テーマ・目標を表す。

**Feature:**

複数のTaskを束ねる機能単位・成果物単位を表す。Epic配下に置くことも、上位Epicを持たずに使用することもできる。

**Task:**

実際の作業単位を表す。最小のトラッキング粒度であり、子Issueは持たない。

**Parent-Child Relationship（親子関係）:**

以下の親子関係を許容する。

- EpicとFeature
- EpicとTask
- FeatureとTask

親子関係はSub-issueで管理する。Issue本文への親Issue記載は行わない。

以下の構造は許容しない。

- Epic→Epic、Feature→Feature（同一Type間の階層）
- Feature→Epic、Task→Feature、Task→Epic（階層方向の逆転）
- Taskが子Issueを持つ構造

**Hierarchy Omission（階層の省略）:**

階層はIssue数を増やすための形式要件ではなく、管理対象の規模とまとまりを表現するために使用する。

- 大規模なテーマで複数成果物を含む場合はEpic → Feature → Task
- 複数作業をまとめるテーマだがFeatureへ分ける必要がない場合はEpic → Task
- 一つの成果物を複数作業へ分解する場合はFeature → Task
- 単発または小規模な作業はTask only

不要な上位Issueや中間Issueを、階層を満たす目的だけで作成しない。

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
- 階層を満たす目的だけで、不要なEpicまたはFeatureを作成しない。
- Issueの規模・性質に応じて必要な階層のみを使用する。
- 親子関係の方向と各Typeの責務は維持する。

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
- [ ] Issueの規模・性質に応じて必要な階層が選択されているか
- [ ] Epic・Feature・Taskの親子関係が許容された方向になっているか
- [ ] 不要なEpicまたはFeatureを階層維持のためだけに作成していないか
- [ ] 親子関係がSub-issueで管理されているか
- [ ] 標準仕様にない独自Fieldを不必要に追加していないか

---

## Notes（補足）

GitHub Project Setupは初期構築のみを対象とする。

運用開始後の変更は、GitHub Project Setupではなく、適切なConvention・または個別リポジトリのドキュメントで管理する。
