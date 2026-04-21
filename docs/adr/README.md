# Architecture Decision Records

本ディレクトリは、プロジェクトにおける技術的・運用上の意思決定を記録します。

---

## ADRとは

ADR（Architecture Decision Record）は、重要な設計・運用上の決定を「背景・決定・理由・却下した案」の形式で残すドキュメントです。「なぜそうなっているか」を後から追えるようにすることが目的です。

## 一覧

| # | タイトル | 状態 |
| --- | --- | --- |
| [0000](./0000-template.md) | テンプレート | — |
| [0001](./0001-document-structure.md) | 規約ドキュメントの構成 | 採用 |
| [0002](./0002-branch-strategy-and-merge.md) | ブランチ戦略・マージ方法 | 採用 |
| [0003](./0003-issue-label-design.md) | Issueラベルの設計 | 採用 |
| [0004](./0004-github-projects-design.md) | GitHub Projects の設計 | 採用 |
| [0005](./0005-github-folder-structure.md) | `.github/` フォルダの構成方針 | 採用 |
| [0006](./0006-commit-convention-design.md) | コミット規約の設計 | 採用 |
| [0007](./0007-release-note-generation.md) | リリースノート生成方針 | 採用 |
| [0008](./0008-ci-pr-workflow-design.md) | `ci-pr.yml` の検証対象とブランチ名ルールの設計 | 採用 |

## ADRの追加方法

1. `0000-template.md` をコピーして連番ファイル名で作成する
2. 状態は `採用` / `却下` / `保留` / `廃止` のいずれかを記入する
3. 上の一覧に追記する
4. 既存のADRを変更・廃止する場合は、元のADRに「廃止：`NNNN` に置き換えられた」と追記し、新しいADRを作成する（過去のADRは編集しない）
