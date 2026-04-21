# コミット規約

本ドキュメントは、リポジトリにおけるコミットメッセージのルールを定義します。
すべてのコミットはすべて本規約に従ってください。

---

## 目次

1. [フォーマット](#1-フォーマット)
2. [Gitmoji + Type 対応表](#2-gitmoji--type-対応表)
3. [各要素の説明](#3-各要素の説明)
4. [ルール](#4-ルール)
5. [参考](#5-参考)

---

## 1. フォーマット

```text
<gitmoji> <type>(<scope>): <subject>

# Why
<変更の背景・目的（省略可）>

# What
- <変更内容（箇条書き）>

# Notes
<補足情報・制約・既知の問題・今後の課題（省略可）>

BREAKING CHANGE: <破壊的変更の概要（省略可）>
<破壊的変更の詳細・移行方法（複数行可・省略可）>

Refs: #<issue番号>
```

---

### 例

#### 通常のコミット

```text
✨ feat(auth): Google OAuthログインを追加

# Why
メールログインのみでは認証の選択肢が少ないため。

# What
- Google OAuth 2.0 によるログイン機能を追加
- 既存のメールログインとの共存を確認

Refs: #42
```

#### 小さな変更

```text
📦 build: next.js を 15.3.0 にアップデート

# What
- next.js を 15.3.0 にアップデート

Refs: #7
```

#### 複数Issue参照

```text
🐛 fix(auth): トークン検証の競合状態を修正

# What
- リクエストIDを導入して最新リクエストへの参照を管理
- 競合状態によるトークン無効化を防止

Refs: #88, #91
```

#### 破壊的変更（単行）

```text
♻️ refactor(auth): authレスポンスのtokenフィールドをリネーム

# Why
フィールド名をOAuth標準仕様に合わせるため。

# What
- レスポンスの `token` フィールドを `access_token` にリネーム

BREAKING CHANGE: `token` フィールドが `access_token` にリネームされました。

Refs: #88
```

#### 破壊的変更（複数行）

```text
♻️ refactor(auth): authレスポンスのtokenフィールドをリネーム

# Why
フィールド名をOAuth標準仕様に合わせるため。

# What
- レスポンスの `token` フィールドを `access_token` にリネーム

BREAKING CHANGE: `token` フィールドが `access_token` にリネームされました。

移行手順：
- レスポンスを参照している箇所を `access_token` に変更してください。

影響範囲：
- auth モジュール全体

Refs: #88
```

---

## 2. Gitmoji + Type 対応表

| Gitmoji | Type | 用途 |
| :---: | --- | --- |
| ✨ | `feat` | 新機能 |
| 🐛 | `fix` | バグ修正・セキュリティ修正 |
| 📝 | `docs` | ドキュメントのみの変更 |
| 💄 | `style` | フォーマット・スタイル変更（動作に影響しない） |
| ♻️ | `refactor` | リファクタリング・コード削除 |
| ⚡️ | `perf` | パフォーマンス改善 |
| ✅ | `test` | テストの追加・修正 |
| 🔧 | `chore` | 設定・ツール・ファイル削除 |
| 📦 | `build` | 依存関係・パッケージの変更 |
| 👷 | `ci` | CI/CD の設定変更 |
| ⏪ | `revert` | 変更の取り消し |

---

## 3. 各要素の説明

### 一覧

| 要素 | 必須 | 説明 |
| --- | :---: | --- |
| `<gitmoji>` | ✅ | 変更種別を視覚的に示す絵文字 |
| `<type>` | ✅ | 変更の種別（対応表参照） |
| `<scope>` | ➖ | 変更が影響するモジュール・レイヤー |
| `<subject>` | ✅ | 変更内容の要約 |
| `# Why` | ➖ | 変更の背景・目的 |
| `# What` | ✅ | 変更内容の詳細（箇条書き） |
| `# Notes` | ➖ | 補足情報・制約・既知の問題・今後の課題 |
| `BREAKING CHANGE:` | ➖ | 破壊的変更の明示 |
| `Refs: #<n>` | ✅ | 関連Issueへの参照 |

> ✅ 必須　➖ 任意

---

### `<gitmoji>`

対応表のGitmojiを使用します。絵文字は1つのみ。

### `<type>`

対応表のtypeを使用します。

### `<scope>`

GitHub Projectsの **Areaフィールドの値に従います**。

例：

- frontend
- backend
- content
- data
- auth
- infra
- integration
- cli
- docs

### `<subject>`

- 変更内容を端的に表現する
- 先頭を大文字にしない（英語の場合）
- 末尾にピリオドをつけない
- 72文字以内を目安（日本語は約35文字相当）

#### よく使う動詞

| カテゴリ | 動詞 | 説明 |
| --- | --- | --- |
| 追加・作成 | `add` | ファイル・機能・要素の追加 |
| | `implement` | 機能の実装（大きめの変更） |
| 変更・改善 | `update` | 既存要素の更新 |
| | `improve` | 品質・UXの改善 |
| 修正 | `fix` | バグ・不具合の修正 |
| 削除・整理 | `remove` | ファイル・コード・要素の削除 |
| | `cleanup` | 不要なコード・ファイルの整理 |
| 内部改善 | `refactor` | 動作を変えずに構造を改善 |
| 設定・依存 | `configure` | 設定・初期化 |
| | `bump` | バージョン・依存関係の更新 |

### `# Why`

変更の**背景・目的**を記述します。以下のいずれかに該当する場合は必須：

- 設計・ロジック・挙動の変更
- 技術的な選択肢が複数あった場合
- 非自明な判断を含む場合

### `# What`

変更内容を箇条書きで記述します。

### `# Notes`

主に以下に使用：

- 設計判断・補足情報
- 制約・前提条件
- 既知の問題
- 今後の課題

### `BREAKING CHANGE:`

破壊的変更がある場合のみ記述します。

#### 単行

```text
BREAKING CHANGE: `token` フィールドが `access_token` にリネームされました。
```

#### 複数行（概要の後に詳細を続けて記述）

```text
BREAKING CHANGE: `token` フィールドが `access_token` にリネームされました。

移行手順：
- レスポンスを参照している箇所を `access_token` に変更してください。

影響範囲：
- auth モジュール全体
```

### `Refs: #<n>`

関連するIssue番号を記述します。

- コロン形式（`Refs: #123`）を使用します
- 複数のIssueはカンマ区切りで記述します（`Refs: #123, #456`）
- コミット時点ではIssueをCloseしません（CloseはPRで行います）

> `Refs:` はConventional Commitsのフッタートークン仕様（`TOKEN: value`形式）に準拠しており、commitlint等の外部ツールと互換性があります。また `BREAKING CHANGE:` の終了トークンとして確実に機能します。

---

## 4. ルール

- ✅ 1コミット = 1つの論理的な変更
- ✅ Gitmoji と type は必ず対応表に従う
- ✅ subject は72文字以内を目安
- ✅ `Refs:` はコロン形式で記述する
- ✅ IssueのCloseはPRで行う
- ❌ `main` に直接pushしない
- ❌ 複数の無関係な変更をまとめない
- ❌ 意味の薄いメッセージを避ける（例：「修正」「更新」）

---

## 5. 参考

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Gitmoji](https://gitmoji.dev/)
