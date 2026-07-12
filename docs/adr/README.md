# ADR（アーキテクチャ決定記録）

本ディレクトリは、確定した設計判断を保存するADR（Architecture Decision Record）を管理する。

ADRは現行仕様を定義する文書ではない。採用した設計判断とその判断理由を記録し、意思決定の経緯を長期資産として保存することを目的とする。詳細な設計検討の過程はDesign Recordが記録する。

---

## ADRの責務（ADRが扱うもの）

ADRが記録するのは以下である。

- 採用した設計判断（Decision）
- 判断理由（Decision Rationale）
- Status
- 判断による影響（Consequences）
- 判断が反映された関連文書（Related Documents）

ADRが記録しないのは以下である。

- 現行仕様そのもの（仕様は各Convention・Specification文書がSSOT）
- 運用手順・操作方法
- 詳細な設計検討・比較検討の全容・議論の流れ・未採用案の詳細（Design Recordの責務）

---

## ファイル命名規則（命名規則）

```text
<4桁連番>-<kebab-case-slug>.md
```

**Examples:**

```text
0000-template.md
0001-adopt-layer-dependency-direction.md
0002-separate-setup-and-operation.md
```

- 連番は4桁のゼロパディングで採番する
- スラッグは判断の主題を英語のkebab-caseで表現する
- ファイル名に `adr-` プレフィックスは付けない（このディレクトリ配下である時点でADRと判断できるため）
- `0000` はテンプレート予約番号とし、実際のADRは `0001` から採番する

---

## Statusの定義（ステータス定義）

| Status | 意味 |
| --- | --- |
| `Proposed` | 提案中。まだ合意が得られていない |
| `Accepted` | 採用済み。現在有効な判断 |
| `Superseded` | 別のADRにより上書きされた |
| `Deprecated` | 廃止済み。理由はADR本文に記載 |

---

## ADRを書くタイミング（作成タイミング）

以下の場合にADRを作成する。

- 複数の設計案を比較検討した判断
- 将来の設計者が「なぜこうなっているのか」を知る必要がある判断
- 現在は採用しないが、将来再検討する可能性がある判断

以下の場合はADRを作成しない。

- 自明な選択（他の選択肢が実質ない場合）
- Convention・Specificationで直接表現できる運用ルール

---

## テンプレートの使い方（テンプレート利用方法）

`0000-template.md` をコピーして新しいADRを作成する。

```text
0000-template.md → 0001-<slug>.md
```

ADR IDとTitleを更新し、Statusを `Proposed` から始める。

各セクションの詳細な書式・責務はテンプレート本体（`docs/adr/0000-template.md`）に委ねる。

---

## Design Recordとの関係（Relationship with Design Record）

ADRとDesign Recordの対応関係は1対1に固定しない。次の関係をすべて許容する。

- 1つのDesign Recordから複数のADRが生成される
- 複数のDesign Recordから1つのADRが生成される
- Design Recordのみで終了し、ADRへ発展しない
- Design Recordを経由せず、ADRのみが存在する

```text
ADR
 └── 設計判断を保持する

Design Record
 └── 設計検討を保持する
```

対応関係の追跡は、各文書が持つ参照情報によって行う。具体的な相互参照の書式は、`docs/design-records/README.md` および各テンプレートの改定時に定義する。

---

## Documentationとの関係（Relationship with Documentation）

ADRは現行仕様・運用ルールのSSOTではない。

現在有効な設計はDocumentationを参照する。

DocumentationはADRへ依存しない。

---

## 関連文書（参照先）

- 設計思想: `docs/philosophy/adr.md`
- テンプレート: `docs/adr/0000-template.md`
- 命名規則: `docs/conventions/naming.md`（NM-ID-004）
- Design Recordの運用: `docs/design-records/README.md`
