# ワークフロー規約

本ドキュメントは、リポジトリにおける開発フローのルールを定義します。
ブランチ・Issue・Pull Request・リリースの運用はすべて本規約に従ってください。

---

## 目次

1. [基本フロー](#1-基本フロー)
2. [Branch](#2-branch)
3. [Issue](#3-issue)
4. [Pull Request](#4-pull-request)
5. [Release](#5-release)
6. [ルール](#6-ルール)

---

## 1. 基本フロー

```text
Issue作成
  └─ ブランチ作成（type/{issue番号}-{説明}）
       └─ 実装・コミット
            └─ PR作成
                 └─ レビュー・CI通過
                      └─ Squash merge → main
                           └─ ブランチ削除
                                └─ Issueクローズ
```

---

## 2. Branch

### 2-1. 命名規則

```text
<type>/{issue番号}-{kebab-case-description}
```

> 複数TaskをまとめるPRまたはFeature単位のPRを作成する場合は、親FeatureのIssue番号をブランチ名に採用します。

#### 例

```text
feature/42-google-oauth
fix/88-token-race-condition
hotfix/101-critical-auth-bypass
docs/12-update-readme
chore/5-setup-eslint
refactor/33-auth-module
release/v1.2.0
```

### 2-2. Type 一覧

| Type | 用途 |
| --- | --- |
| `feature` | 新機能の開発 |
| `fix` | バグ修正（計画的・Issue起票して対応） |
| `hotfix` | 本番障害の緊急修正（`main` から直接分岐） |
| `refactor` | リファクタリング（機能変更なし） |
| `docs` | ドキュメントのみの変更 |
| `chore` | 設定・依存関係・ツールの変更 |
| `release` | リリース準備（バージョン更新など） |

> `fix` と `hotfix` の違いは緊急度です。`hotfix` は本番障害など即時対応が必要な場合にのみ使用します。通常のバグ修正は `fix` を使用してください。

<!-- -->

> `bug` Issueから派生した作業のブランチtypeは、緊急度に応じて選択します（通常は `fix/`、本番障害は `hotfix/`）。

<!-- -->

> `enhancement` Issueから派生した作業のブランチtypeは、作業内容に応じて選択します（`feature/` / `chore/` / `refactor/` / `fix/` など）。

### 2-3. 常設ブランチ

| ブランチ | 役割 |
| --- | --- |
| `main` | 常にリリース可能な状態を維持する本番ブランチ |

> 本プロジェクトは **GitHub Flow** を採用します。`develop` ブランチは使用しません。

### 2-4. ライフサイクル

- 作業ブランチは `main` から作成します
- マージ完了後は速やかに削除します
- `hotfix` ブランチは `main` から作成し、マージ後に削除します

---

## 3. Issue

### 3-1. テンプレート

リポジトリには以下のIssueテンプレートを用意します。

| テンプレート | ラベル | 用途 |
| --- | --- | --- |
| `epic.yml` | `type:epic` | 大項目（複数の機能やタスクをまとめた単位） |
| `feature.yml` | `type:feature` | 機能単位（特定の機能を実現する単位） |
| `task.yml` | `type:task` | 作業単位（具体的な実装や対応を行う単位） |
| `bug-report.yml` | `type:bug` | 不具合報告（予期しない動作・エラーの報告） |
| `enhancement.yml` | `type:enhancement` | 改善提案（既存の機能・仕様・構成などの改善提案） |

各テンプレートはIssue作成時にラベルを自動付与します。
作成後、Project上でLayer / Priority / Areaを設定してください。

### 3-2. タイトル規則

各テンプレートにはタイトルのプレフィックスが設定されています。

| テンプレート | プレフィックス |
| --- | --- |
| `epic.yml` | `【Epic】` |
| `feature.yml` | `【Feat】` |
| `task.yml` | `【Task】` |
| `bug-report.yml` | `【Bug】` |
| `enhancement.yml` | `【Enh】` |

#### 3-2. タイトル規則の例

```text
【Epic】ユーザー認証機能を実装する
【Feat】Google OAuthログインを実装する
【Task】OAuthコールバックエンドポイントを実装する
【Bug】ログインボタンを押すと500エラーが返る
【Enh】task.yml の完了条件フィールドのidを統一する
```

### 3-3. ラベル

`type:` ラベルのみを使用します。Status・Priorityの管理はGitHub Projectsのフィールドで行います。詳細は [REPOSITORY_CONVENTION.md](./REPOSITORY_CONVENTION.md) を参照してください。

| ラベル名 | 説明 |
| --- | --- |
| `type:epic` | 大項目（複数の機能やタスクをまとめた単位） |
| `type:feature` | 機能単位（特定の機能を実現する単位） |
| `type:task` | 作業単位（具体的な実装や対応を行う単位） |
| `type:bug` | 不具合報告（予期しない動作・エラーの報告） |
| `type:enhancement` | 改善提案（既存の機能・仕様・構成などの改善提案） |

### 3-4. アサイン

- 着手する際に自身をアサインします
- 未着手のIssueはアサインしません

### 3-5. クローズ

- TaskのIssueはPRのマージ時に自動でクローズします（`Closes #<n>` による）
- Epic・FeatureのIssueは配下の作業がすべて完了した後に手動でクローズします
- コミット時点ではクローズしません

---

## 4. Pull Request

### 4-1. タイトル規則

コミットメッセージの1行目と同じフォーマットを使用します。

```text
<gitmoji> <type>(<scope>): <subject>
```

#### 4-1. タイトル規則の例

```text
✨ feat(auth): Google OAuthログインを追加
🐛 fix(auth): トークン検証の競合状態を修正
```

### 4-2. テンプレート構成

| セクション | 必須 | 説明 |
| --- | :---: | --- |
| 🔗 関連Issue | ✅ | `Closes #<番号>` でマージ時に自動クローズ。途中対応は `Refs #<番号>` |
| 🏷️ 変更タイプ | ✅ | コミット規約のtypeに対応するチェックボックス |
| 📌 概要 | ✅ | 変更内容を1〜2文で説明 |
| 🎯 Why | ➖ | 変更の理由・背景。設計・ロジック・挙動の変更がある場合は必須 |
| 🔧 What | ✅ | 変更内容の詳細（箇条書き） |
| ✅ 動作確認 | ✅ | ローカル確認・既存機能への影響・テストのチェックボックス |
| 📝 Notes | ➖ | 設計判断・制約・既知の問題・今後の課題などの補足情報 |
| 💥 BREAKING CHANGE | ✅ | 破壊的変更の有無。ありの場合は内容を記載 |

> ✅ 必須　➖ 任意

#### 関連Issueの記載ルール

- `Closes #<番号>` は1行ずつ記載します（スペース区切りの複数指定は誤動作の原因になります）
- Feature単位のPRの場合はTaskのIssue番号を列挙します。FeatureのIssueは全Task完了後に手動でCloseします
- 途中対応の場合は `Refs #<番号>` を使用します

### 4-3. レビュールール

- PRのレビューは任意です（個人開発のため承認必須としません）
- レビュワーがいる場合はコメントから3営業日以内に対応します

### 4-4. ドラフトPR

- 実装途中・方針確認・CIの動作確認など、レビュー前の状態ではドラフトPRを使用します
- 完成したらドラフトを解除してレビュー依頼します

### 4-5. マージ方法

**Squash merge** を使用します。

| マージ方法 | 採用 | 理由 |
| --- | :---: | --- |
| Merge commit | ❌ | マージコミットが増えてhistoryが煩雑になる |
| Squash merge | ✅ | ブランチ内の試行錯誤コミットを1つに集約できる |
| Rebase merge | ❌ | コミットハッシュが変わり、追跡が困難になる |

> Squash merge後のコミットメッセージは、PRタイトルと同じフォーマットで記述します。

### 4-6. マージの前提条件

以下をすべて満たした場合にマージできます。

- [ ] すべてのCIチェック通過
- [ ] `main` との差分（コンフリクト）なし

### 4-7. PRのサイズと対応単位

基本形は **1PR = 1Issue（Task単位）** です。ただし規模に応じて以下の運用も可能です。

| 規模 | PR単位 | ブランチのIssue番号 | Issueのクローズ |
| --- | --- | --- | --- |
| 小規模Task | 1PR = 1Task | TaskのIssue番号 | PRマージ時に自動クローズ（`Closes #<n>`） |
| 複数Taskをまとめる | 1PR = 複数Task | 親FeatureのIssue番号 | 各TaskをPR本文に列挙して自動クローズ |
| Feature単位でまとめる | 1PR = 1Feature | FeatureのIssue番号 | Feature配下のTaskをPR本文に列挙して自動クローズ |

#### Epic・FeatureのIssueクローズについて

- EpicおよびFeatureのIssueは **手動でクローズ** します
- 配下のすべてのTask・Feature完了を確認してからクローズしてください
- `Closes #<n>` による自動クローズはTaskのみに使用します

> 変更が大きい場合はIssueを分割してPRを分けることを優先します。

---

## 5. Release

### 5-1. バージョニング

[Semantic Versioning](https://semver.org/lang/ja/) に従います。

```text
v{major}.{minor}.{patch}
```

| バージョン | 上げるタイミング |
| --- | --- |
| `major` | 後方互換性のない破壊的変更（`BREAKING CHANGE`） |
| `minor` | 後方互換性のある新機能追加 |
| `patch` | 後方互換性のあるバグ修正 |

#### 5-1. バージョニングの例

```text
v1.0.0
v1.2.3
v2.0.0
```

### 5-2. リリースタグ

- GitHubのReleasesからタグを作成します
- タグ名は `v{major}.{minor}.{patch}` 形式とします
- タグは `main` ブランチの最新コミットに対して作成します

### 5-3. リリースノート

- `release-draft.yml` ワークフローでドラフトリリースを自動生成します
- 生成後に内容を確認し、必要に応じて加筆・修正します
- `BREAKING CHANGE` がある場合は冒頭に明記します

> 本リポジトリはPRラベルによる管理を行っていないため、GitHubのRelease自動生成機能には非対応です。リリースノートの生成は必ず `release-draft.yml` を使用してください。

### 5-4. リリース手順

```text
【リリース準備】
1. release/{バージョン} ブランチを main から作成する
2. バージョン番号を更新する（package.json など）
3. PR作成 → レビュー → Squash merge

【リリース生成】
4. release-draft ワークフローを実行する
   （Actions → 🏷️ Release Draft → Run workflow）
   - version: リリースバージョンを入力（例: 1.2.0 または v1.2.0）
   - previous_tag: 前回タグを入力（空欄で自動検出）
5. 生成されたドラフトリリースを確認・加筆修正する
   - BREAKING CHANGE がある場合は冒頭に明記する

【リリース確定】
6. Publish release でリリースを公開する
7. release ブランチを削除する
```

---

## 6. ルール

### Branch

- ✅ ブランチは必ず `main` から作成する
- ✅ 命名規則（`type/{issue番号}-{説明}`）に従う
- ✅ マージ後はブランチを削除する
- ❌ `main` に直接 push しない

#### Issue

- ✅ 作業着手時に自身をアサインする
- ✅ TaskのIssueクローズはPRのマージで行う（`Closes #<n>`）
- ✅ Epic・FeatureのIssueは全作業完了後に手動でクローズする
- ❌ 着手前のIssueをアサインしない

#### Pull Request

- ✅ Squash merge を使用する
- ✅ PRタイトルはコミットフォーマットに従う
- ✅ `Closes #<issue番号>` を本文に記述する
- ❌ CIが失敗したままマージしない
- ❌ コンフリクトを解消せずにマージしない

#### Release

- ✅ タグはSemantic Versioning形式で付与する
- ✅ タグは `main` ブランチの最新コミットに付与する
- ✅ `BREAKING CHANGE` はリリースノートの冒頭に明記する
