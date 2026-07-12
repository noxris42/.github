# Design Records（設計検討記録）

本ディレクトリは、設計検討の過程を保存するDesign Recordを管理する。

Design Recordの設計思想は `docs/philosophy/design-record.md` に定義されている。本書はその思想を前提として、Design Recordの作成・管理方法を定義する運用文書である。

---

## Design Recordの責務（Design Recordが扱うもの）

Design Recordが記録するのは以下である。

- 設計背景
- 設計検討
- 比較した案
- 議論の流れ
- 判断候補
- 未採用案

Design Recordが記録しないのは以下である。

- 現行仕様そのもの（仕様は各Philosophy・Architecture・Convention・SpecificationがSSOT）
- 正式なArchitecture Decision（判断はADRが記録する）
- 運用ルール

---

## ファイル分割の方針

Design Recordのファイル分割には、厳密な機械的基準を設けない。現時点では次の方針を採用する。

- 1ファイルは、一つの設計作業として自然に振り返ることができるまとまりとする
- 関連するQuestionは、同一ファイル内の見出しで整理する
- 一部のQuestionが独立して再検討される可能性が高い場合は、別ファイルへ分割できる
- Question数・文字数・対応するADR数による固定的な分割基準は設けない

粒度は実例や設計内容に応じて判断する。具体的な基準は、実例の蓄積後に必要に応じてGuidelineとして成熟させる。

---

## 採番規則（Numbering）

Design Recordには4桁の連番を付与する。

```text
0001
0002
0003
```

採番は、元となった設計検討が開始された論理的な時系列を基準とする。過去の設計検討を後から抽出した場合は、その検討が実際に行われた時点を基準に、既存の連番の間へ挿入してよい。

ADRとは独立した番号体系とし、`DR-` などのプレフィックスは付けない。Design Recordであることは `docs/design-records/` というディレクトリ階層によって表現する。

---

## ファイル命名規則（File Naming）

ファイル名は以下の形式を基本とする。

```text
<4桁連番>-<design-topic>.md
```

**Examples:**

```text
0001-commit-convention.md
0002-adr-lifecycle.md
```

`<design-topic>` は、そのDesign Recordが扱う設計検討のまとまりを英語のkebab-caseで表現する。

ファイル名は、そのDesign Recordが到達した最終的なDecisionではなく、扱った設計上の議題・対象を表す。

---

## 記録としての性質（Record Lifecycle）

Design Recordは、設計中に逐次更新する作業管理文書ではない。設計・議論が一区切りした後、その内容を事後的に整理・保存する記録として扱う。

Raw Chat Archiveからの抽出方法・AIによる抽出・Decision Miningなど、Design Recordを生成する具体的な手順は本書の対象外とする。これらは後続のProcess文書で定義する。

---

## 不変性の方針（Immutability）

Design Recordの本文は、記録した時点の設計検討を保存するものとして扱う。作成・確認後は、以下を除き本文を変更しない。

- 誤字脱字
- Markdown体裁
- 明らかな事実誤認
- 参照切れなど、保守上必要な修正

後から生じた評価・判断・関連ADRなどの情報は、本文を書き換えずReview Historyへ追記する。

同じ議題について後日新たな設計検討が行われた場合は、既存のDesign Recordを書き換えず、新しいDesign Recordとして記録する。

---

## レビュー履歴（Review History）

Design Recordには、作成後の評価結果を追記できるReview Historyを持たせる。

Review Historyでは、必要に応じて次のような結果を記録する。

- ADR化された
- Documentationにのみ反映された
- 他のDesign RecordまたはADRへ統合された
- 保留された
- 採用されなかった
- 後日再検討された

Review Historyの具体的な書式は、Design Recordテンプレート策定時に定義する。本書では、Review Historyが担う責務のみを定義する。

---

## ADRとの関係（Relationship with ADR）

Design RecordとADRの対応関係は1対1に固定しない。次の関係をすべて許容する。

- 1つのDesign Recordから複数のADRが生成される
- 複数のDesign Recordから1つのADRが生成される
- ADRへ発展しないDesign Recordが存在する

```text
Design Record
 └── 設計検討を保持する

ADR
 └── 設計判断を保持する
```

対応関係の追跡は、各文書が持つ参照情報によって行う。具体的な相互参照の書式は、`docs/adr/README.md` および各テンプレートの改定時に定義する。

---

## Documentationとの関係（Relationship with Documentation）

Design Recordは、現行仕様・運用ルールのSSOTではない。現在有効な設計を確認する場合は、Philosophy・Architecture・Convention・SpecificationなどのDocumentationを参照する。

Design Recordは、何を検討したかを保存する記録として扱う。

---

## 関連文書（参照先）

- 設計思想: `docs/philosophy/design-record.md`
- Documentation全体の責務定義: `docs/architecture/documentation.md`
- ADRの責務: `docs/philosophy/adr.md`、`docs/adr/README.md`

---

本書はDesign Recordの運用方法を定義する。Design Recordの思想は `docs/philosophy/design-record.md` を参照する。現在有効な設計は、各Philosophy・Architecture・Convention・Specificationを参照する。
