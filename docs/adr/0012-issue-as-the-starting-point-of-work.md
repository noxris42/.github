# 0012. Issueを作業の起点とする

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

GitHub運用のワークフローを設計する過程で、作業をどのように追跡可能にするかが論点になった。過去の参考資料も踏まえ、作業の起点をIssueに統一する運用思想（Issue駆動運用）が導入された。

---

## Decision（決定）

追跡可能な作業は、Issueを起点として管理する。Issueが作業管理の中心点となる。

---

## Rationale（理由）

作業の起点をIssueに統一することで、「何のために行った作業か」という目的（Issue）から、実際の変更（Commit・PR）までの追跡経路が一本化される。作業がIssueを経由せずに行われると、作業目的から実際の変更までを一貫して追跡する標準的な経路が失われる。

---

## Alternatives Considered（却下した案）

該当なし。この決定はGitHub運用ワークフロー設計の出発点として導入されたものであり、明示的に比較検討された対立案は確認されていない。

---

## Consequences（影響・注意点）

- Issueを起点とせず、作業目的から実際の変更までの追跡経路を持たない変更は、このプロジェクトの標準ワークフローの対象外とする
- Issueを1つの作業単位としてどう扱うか（1 Issue = 1 Taskの原則）は、本ADRの対象外とし、別途定義する
- Branchを使う場合のIssue・Branch・PRの対応関係は、本ADRの対象外とし、別途定義する

---

## Related Documents（関連文書）

- `docs/specifications/github-workflow.md`
