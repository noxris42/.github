# プロジェクト規約

本ドキュメントは、GitHub Projectsの運用ルールを定義します。
計画・進捗管理はすべて本規約に従ってください。

---

## 目次

1. [基本方針](#1-基本方針)
2. [基本フロー](#2-基本フロー)
3. [階層構造](#3-階層構造)
4. [フィールド定義](#4-フィールド定義)
5. [Milestone](#5-milestone)
6. [View](#6-view)
7. [Workflows 自動化](#7-workflows-自動化)
8. [ルール](#8-ルール)

---

## 1. 基本方針

- GitHub Projects を唯一の進捗管理ツールとして使用します
- すべての作業はIssueとして起票し、Projectsで管理します
- Issue はやること（What / How）を書く場所、Project は管理する場所（Status / Priority / Area / Layer）です
- IssueとProjectsの紐付けは作成時に行います

---

## 2. 基本フロー

### Statusの遷移

```text
Backlog → Ready → In Progress → Review → Ready（差し戻し）
                                       → Ready（承認・マージ待ち）→ Done
```

Statusは基本的に自動遷移しますが、以下は手動で変更します。

| 遷移 | タイミング | 操作 |
| --- | --- | --- |
| `Backlog` → `Ready` | 着手可能な状態になったとき | 手動 |
| `Ready` → `In Progress` | 作業を開始するとき | 手動 |
| `In Progress` → `Review` | PRがIssueに紐付けられたとき | 自動（⑦） |
| `Review` → `Ready` | Changes requestedレビューが付いたとき（差し戻し） | 自動（⑩） |
| `Review` → `Ready` | PRが承認されたとき（マージ待ち） | 自動（⑪） |
| `Ready` → `Done` | PRがマージされたとき / Issueがクローズされたとき | 自動（⑧⑤） |

#### 実行フロー

```text
1. IssueをReadyに移動する（着手可能になったタイミング）
2. ブランチを作成して実装を開始する（StatusをIn Progressに変更）
3. PRを作成する（StatusがReviewに自動変更）
4a. Changes requested → StatusがReadyに自動変更 → 修正してPRを更新
4b. Approved → StatusがReadyに自動変更 → マージ実行
5. マージ（StatusがDoneに自動変更）
```

---

## 3. 階層構造

### 3-1. 基本構造

作業はSub-issue機能で以下の3階層に分解して管理します。

```text
Epic
  └─ Feature
       └─ Task
```

| Layer | 区分 | 説明 | 粒度の目安 |
| --- | --- | --- | --- |
| `Epic` | 【大項目】 | 複数の機能やタスクをまとめた単位 | 複数スプリントにまたがる |
| `Feature` | 【機能】 | 特定の機能を実現する単位 | 1〜2スプリントで完結 |
| `Task` | 【作業】 | 具体的な実装や対応を行う単位 | 1〜3時間で完結 |

> **Bug について**
> BugはLayerの概念外です。対応規模に応じてLayerを設定してください。
> 小規模な修正 → `Task` / 機能改修が必要 → `Feature` または `Epic`

<!-- -->

> **Enhancement について**
> EnhancementはLayerの概念外です。起票後にトリアージを行い、対応規模に応じてLayerを設定してください。
>
> - 小規模 → `Task` として着手
> - 中規模 → `Feature` に昇格、またはFeature配下にTaskを作成
> - 大規模 → `Epic` を新設してFeature・Taskに分解

### 3-2. 小規模時の省略

以下の場合はFeatureを省略できます。

```text
Epic → Task
```

- Taskが少数（目安：1〜3）
- 機能として分割する必要がない
- ドキュメントや軽微な作業

必要に応じて後からFeatureを追加して再構造化します。

### 3-3. 親子関係ルール

- EpicはFeatureまたはTaskを子に持ちます
- FeatureはTaskを子に持ちます
- Taskは親を持ちますが、子は持ちません
- **親子関係はSub-issue機能で管理します。Issueテンプレートへの親Issue記載は行いません（二重管理防止）**

---

## 4. フィールド定義

### 4-1. フィールド一覧

| フィールド | 種別 | 必須 | 説明 |
| --- | --- | :---: | --- |
| `Title` | テキスト | ✅ | Issueタイトル（自動連携） |
| `Status` | 単一選択 | ✅ | 現在の作業状態 |
| `Layer` | 単一選択 | ✅ | 作業の粒度・階層区分 |
| `Area` | 単一選択 | ✅ | 影響するシステム領域 |
| `Priority` | 単一選択 | ✅ | 優先度 |
| `Milestone` | マイルストーン | ➖ | 関連するマイルストーン（Epic/Featureに設定） |
| `Assignees` | ユーザー | ➖ | 担当者（自動連携） |

> ✅ 必須　➖ 任意

---

### 4-2. Status（状態）

タスクの進行状況を表します。

| 値 | 区分 | 説明 |
| --- | --- | --- |
| `Backlog` | 【未整理】 | 未着手・検討中の状態 |
| `Ready` | 【着手可能】 | 作業を開始できる状態。差し戻し後の修正待ち・承認後のマージ待ちも含む |
| `In Progress` | 【作業中】 | 作業が進行中の状態 |
| `Review` | 【確認中】 | PRレビュー・確認を行っている状態 |
| `Done` | 【完了】 | 作業が完了した状態 |
| `Blocked` | 【停滞】 | 進行できない状態 |

---

### 4-3. Layer（単位）

作業の粒度を表します。階層構造はSub-issue機能で管理します。

| 値 | 区分 | 説明 |
| --- | --- | --- |
| `Epic` | 【大項目】 | 複数の機能やタスクをまとめた単位 |
| `Feature` | 【機能】 | 特定の機能を実現する単位 |
| `Task` | 【作業】 | 具体的な実装や対応を行う単位 |

---

### 4-4. Area（領域）

コミット規約の `<scope>` と同じ値を使用します（詳細は [COMMIT_CONVENTION.md](./COMMIT_CONVENTION.md) を参照）。

| 値 | 区分 | 説明 |
| --- | --- | --- |
| `frontend` | 【UI】 | ユーザーインターフェース・UXに関する領域 |
| `backend` | 【処理】 | サーバーサイドの処理・ロジックに関する領域 |
| `content` | 【コンテンツ】 | 記事・CMS・メディア管理に関する領域 |
| `data` | 【データ】 | データベース・モデル・データ処理に関する領域 |
| `auth` | 【認証】 | ユーザー認証・認可・セキュリティに関する領域 |
| `infra` | 【基盤】 | インフラ・デプロイ・環境構築に関する領域 |
| `integration` | 【連携】 | 外部サービス・API連携に関する領域 |
| `cli` | 【ツール】 | CLI・開発支援ツールに関する領域 |
| `docs` | 【文書】 | ドキュメント・設計資料に関する領域 |

---

### 4-5. Priority（優先度）

今やるべきかの指標です。

| 値 | 区分 | 説明 |
| --- | --- | --- |
| `High` | 【高】 | 最優先（すぐ対応する） |
| `Medium` | 【中】 | 通常（順序通り進める） |
| `Low` | 【低】 | 後回し（余裕があれば対応） |

---

## 5. Milestone

「ここまで終われば一区切り」というゴールを表します。

- **Issue**：やること（作業）
- **Milestone**：到達点（ゴール）

### 5-1. 紐付け対象

MilestoneはEpicまたはFeatureに紐づけます。TaskはEpic/Feature経由で管理するため原則不要です。

### 5-2. 命名例

Milestoneはリリース単位・Phase単位・期間単位のいずれかで作成します。

#### リリース単位

バージョン番号は3桁形式（`v{major}.{minor}.{patch}`）を使用します。

```text
v0.1.0 初期版
v0.2.0 機能追加
v1.0.0 正式リリース
```

#### Phase単位

```text
Phase 1: MVP
Phase 2: 投稿機能
Phase 3: セキュリティ強化
```

#### 期間単位

```text
2025-Q1
2025-Q2
```

### 5-3. 運用ルール

- 同時に進めるMilestoneは1つに絞ります
- 完了したら次のMilestoneへ進みます

---

## 6. View

プロジェクトには目的ごとに4つのViewを用意します。

| View名 | 形式 | 用途 |
| --- | --- | --- |
| `進捗` | ボード | 全体の進行状況を把握する（メインボード） |
| `作業` | ボード | Taskのみを表示して実作業に集中する |
| `構造` | テーブル | Epic → Feature → Taskの分解状態を確認する |
| `一覧` | テーブル | 全アイテムをPriority順で一覧・管理する |

### 各Viewの使い方

#### 進捗（メインボード）

- Statusごとにタスクを確認する
- 次に着手するタスクをReadyに移動する
- Blockedがないか確認する

#### 作業（タスクボード）

- Taskのみを表示する
- 作業中はこのViewをメインに使用する
- In Progressのタスクを中心に進める

#### 構造（Layerビュー）

- Sub-issueによりEpic → Feature → Taskの構造になっているか確認する
- Taskが不足していないか確認する
- 粒度が適切かを見直す

#### 一覧（テーブル）

- Priority順で並び替えて優先度を確認する
- 抜け漏れや未設定項目をチェックする
- 全体のバランスを把握する

### 使い分けの指針

| 場面 | 使うView |
| --- | --- |
| 作業中 | 作業 |
| 進捗確認 | 進捗 |
| 設計・整理 | 構造 |
| 管理・確認 | 一覧 |

---

## 7. Workflows 自動化

GitHub ProjectsのDefault workflowsで以下を設定します。

| # | Workflow名 | トリガー | アクション | 有効 |
| --- | --- | --- | --- | :---: |
| ① | Auto-add sub-issues to project | プロジェクト内のアイテムにSub-issueが追加されたとき | Sub-issueをプロジェクトに追加する | ✅ |
| ② | Auto-add to project | フィルターに一致するIssueが作成・更新されたとき | アイテムをプロジェクトに追加する | ✅ |
| ③ | Auto-close issue | StatusがDoneに更新されたとき | Issueをクローズする | ✅ |
| ④ | Item added to project | アイテムがプロジェクトに追加されたとき（Issue） | Statusを `Backlog` に設定する | ✅ |
| ⑤ | Item closed | アイテムがクローズされたとき（Issue / PR） | Statusを `Done` に設定する | ✅ |
| ⑥ | Item reopened | アイテムが再オープンされたとき（Issue / PR） | Statusを `Ready` に設定する | ✅ |
| ⑦ | Pull request linked to issue | PRがIssueに紐付けられたとき | Statusを `Review` に設定する | ✅ |
| ⑧ | Pull request merged | PRがマージされたとき | Statusを `Done` に設定する | ✅ |
| ⑨ | Auto-archive items | フィルターに一致するアイテム | アイテムをアーカイブする | ❌ |
| ⑩ | Code changes requested | PRにchanges requestedレビューが付いたとき | Statusを `Ready` に設定する | ✅ |
| ⑪ | Code review approved | PRが承認されたとき | Statusを `Ready` に設定する | ✅ |

### ②Auto-add to project のフィルター設定

```text
repository:<オーナー名>/<リポジトリ名> is:issue is:open has:label
```

> ラベルが付与されたオープンIssueのみを自動追加します。ラベルなしのIssueは追加されないため、Issue作成時に必ずラベルを設定してください。
>
> フィルターのリポジトリ指定は新規リポジトリ作成時に設定が必要です。設定手順は [REPOSITORY_CONVENTION.md](./REPOSITORY_CONVENTION.md) の初期設定チェックリストを参照してください。

### ⑨Auto-archive items のフィルター設定

```text
is:issue is:closed updated:<@today-2w
```

> クローズ済みかつ2週間以上更新のないIssueを自動アーカイブします。過去のIssueを参照・再オープンする運用のためOFFにしています。

### 手動変更が必要なStatus遷移

自動化でカバーできない以下の遷移は手動で変更します。

| 遷移 | タイミング |
| --- | --- |
| `Backlog` → `Ready` | 着手可能な状態になったとき |
| `Ready` → `In Progress` | 作業を開始するとき |

---

## 8. ルール

- ✅ すべての作業はIssueとして起票してからブランチを作成する
- ✅ Issue作成時に Layer / Area / Priority を設定する
- ✅ 親子関係はSub-issue機能で管理する（テンプレートへの親記載はしない）
- ✅ `Backlog → Ready` および `Ready → In Progress` は手動で変更する
- ✅ Taskは1〜3時間で完了する粒度にする（超える場合は分割を検討する）
- ✅ EpicはFeature / Taskに分解してから作業する（Epicに直接着手しない）
- ✅ `Area` の値はコミットの `<scope>` と統一する
- ✅ Blockedになった場合はNotesに原因を記録し、解消できない場合はBacklogに戻す
- ❌ 完了していないIssueを `Done` にしない
