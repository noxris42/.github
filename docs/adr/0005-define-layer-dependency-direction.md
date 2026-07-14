# 0005. 文書レイヤーの依存方向を定義する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

Branch Convention（Convention層）の記述に、「GitHub Workflow Specification（Specification層）で定義したブランチ運用を具体化する下位文書である」という一文があった。これは実装順序（Specificationを先に作り、Conventionを後に作った）としては事実だが、ドキュメント構造上は「Specificationが上位、Conventionが下位」という誤った依存関係を暗黙に表現していた。

原因を掘り下げると、「参照（reference）」と「依存（dependency）」を混同していたことが分かった。ある文書が別の文書に言及すること自体は自然だが、それによって「言及される側が所有者・親である」という構造が暗黙に生まれてしまっていた。

この誤りは局所的な文言修正では解消できず、文書レイヤー間の依存方向そのものを設計原則として明文化する必要があった。

---

## Decision（決定）

文書レイヤーの依存方向を、以下のとおり定義する。

```text
Philosophy / Architecture
        ↓
Conventions
        ↓
Specifications
        ↓
Templates
```

各文書は、同一レイヤーまたは上位レイヤーのみを参照する。上位レイヤーは下位レイヤーへ依存しない。下位レイヤーは必要に応じて上位レイヤーを参照・利用する。

依存方向は、文書の作成順ではなく、アーキテクチャ上の責務関係によって決める。

---

## Rationale（理由）

依存方向を作成順に委ねると、実装の都合（どちらを先に作ったか）が、そのまま設計上の所有関係であるかのように見えてしまう。これは、後から作成された文書が先に作成された文書を「所有」するかのような誤った構造を生みやすい。

依存方向を責務関係で決めることで、各レイヤーは自分より上位のレイヤーだけを前提にすればよく、下位レイヤーの存在を知らなくても内容が成立する。これにより、各文書がそれ単体で読んで理解できる状態を保てる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| 作成順で依存関係を決める（それまでの暗黙の慣習） | 実装順序と設計思想上の依存方向は無関係である。作成順に従うと、後から作成された文書が先に作成された文書を所有するかのような誤った構造ができ、Convention層がSpecification層を知っているという逆転が生じた |

---

## Consequences（影響・注意点）

- Convention文書はSpecification文書を参照しない。Specification文書はConvention文書を参照・利用してよい
- この原則の適用により、既存の依存関係の逆転（Branch ConventionがGitHub Workflow Specificationを参照していた記述等）を修正した
- ルールの定義そのものが複数文書に重複している場合（SSOT違反）は、権威を持つ文書への参照に統一して解消する。ただし、運用上の確認項目としての言及（例：Workflow文書のReview Checklistにおける確認項目としての言及）は、定義の再述ではないため許容する
- 文書間の関連は、依存としてではなく、本文中の自然文による参照として示してよい

---

## Related Documents（関連文書）

- `docs/architecture/documentation.md`
- `docs/conventions/branch.md`
- `docs/specifications/github-workflow.md`
