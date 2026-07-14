# 0018. Document LabelsはMarkdown Conventionが扱う

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

Rule記述のBody（`**Reason:**`のような強調装飾付きラベル、Document Labels）をどのConventionが管理するかを検討する過程で、これが「マークダウンでの表現方法」なのか「文章表現の一部」なのかが曖昧になっていた。

Document Labelsも文章表現も、どちらも「文書の書き方」に見えるため混同しやすい。しかし両者は異なる責務を持つ。

---

## Decision（決定）

Document Labels（`**Reason:**`等のMarkdown上の局所的な表現形式）はMarkdown Conventionが扱う。文章表現・文体・用語利用はWriting Conventionが扱う。

Markdown Conventionは、そのMarkdown上でどのような文章を書くかには立ち入らない。Writing Conventionは、その文章をMarkdown上でどう表現するかには立ち入らない。

---

## Rationale（理由）

「Markdownでどう表現するか」と「文章としてどう書くか」は別の責務である。前者はMarkdownの記法・構造に関する判断（見出しにするか、強調記法にするか等）であり、後者は文体・用語・言語表記に関する判断である。

この2つを同じConventionに混在させると、Markdown記法の変更が文章表現のルールにも影響するかのように見え、責務の境界が曖昧になる。Document Labelsのような「Markdown上の表現形式」をMarkdown Conventionに帰属させることで、Writing Conventionは純粋に文章表現のみを扱う文書として保てる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| Document LabelsをWriting Conventionで扱う | Document Labelsは文章の内容ではなくMarkdown上の表現形式（強調記法の用法）であり、文章表現を扱うWriting Conventionの責務とは異なる |

---

## Consequences（影響・注意点）

- 新しい表現形式（見出し代替のラベル等）を検討する際は、それがMarkdown上の表現形式か、文章表現かを区別してから配置先を決める
- Document Labelsの具体的な記法・使用条件は、本ADRの対象外とし、`docs/conventions/markdown.md`が定義する

---

## Related Documents（関連文書）

- `docs/conventions/markdown.md`
- `docs/conventions/writing.md`
