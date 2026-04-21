# 開発参加規定

本ドキュメントは、リポジトリへの参加・貢献に関する基本ルールと、各種規約へのナビゲーションを提供します。

---

## ドキュメント構成

| ドキュメント | 内容 | 対象 |
| --- | --- | --- |
| [WORKFLOW_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/WORKFLOW_CONVENTION.md) | ブランチ・Issue・PR・リリースの運用フロー | 全員 |
| [COMMIT_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/COMMIT_CONVENTION.md) | コミットメッセージのフォーマット・絵文字・動詞ルール | 全員 |
| [PROJECT_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/PROJECT_CONVENTION.md) | GitHub Projectsの階層構造・フィールド・View・自動化 | 全員 |
| [REPOSITORY_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/REPOSITORY_CONVENTION.md) | リポジトリ設定・Rulesets・ラベル・Actions・フォルダ構成 | 管理者向け |

---

## 開発の基本フロー

```text
1. Issueを作成する（epic.yml / feature.yml / task.yml / bug-report.yml / enhancement.yml）
2. Project上でLayer / Priority / Areaを設定する
3. ブランチを作成する（type/{issue番号}-{kebab-case-description}）
4. 実装・コミットする
5. PRを作成する
6. レビューを受けてマージする（Squash merge）
7. ブランチ削除・Issueクローズ（自動）
```

詳細は [WORKFLOW_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/WORKFLOW_CONVENTION.md) を参照してください。

---

## コミットメッセージの基本形

```text
<gitmoji> <type>(<scope>): <subject>

# What
- <変更内容>

Refs: #<issue番号>
```

詳細は [COMMIT_CONVENTION.md](https://github.com/noxris42/.github/blob/main/docs/COMMIT_CONVENTION.md) を参照してください。

---

## はじめに確認すること

新しくリポジトリに参加する場合は、以下の順番でドキュメントを確認してください。

1. **WORKFLOW_CONVENTION.md** — ブランチの切り方・Issueの立て方・PRの出し方を確認する
2. **COMMIT_CONVENTION.md** — コミットメッセージの書き方を確認する
3. **PROJECT_CONVENTION.md** — GitHub Projectsの使い方を確認する
4. **REPOSITORY_CONVENTION.md** — リポジトリ設定・フォルダ構成を確認する（主にリポジトリ管理者向け）
