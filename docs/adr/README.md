# ADR（アーキテクチャ決定記録）

本ディレクトリは、設計判断の履歴を保存するADR（Architecture Decision Record）を管理する。

ADRは現行仕様を定義する文書ではない。設計判断・判断理由・検討過程・判断による影響を記録し、設計知識を長期資産として保存することを目的とする。

---

## ADRの責務（ADRが扱うもの）

ADRが記録するのは以下である。

- なぜその設計判断を採用したか
- どのような案を検討し、なぜ却下したか
- 設計途中でどのように考え方が変化したか
- 判断から得られた設計知見

ADRが記録しないのは以下である。

- 現行仕様そのもの（仕様は各Convention・Specification文書がSSOT）
- 運用手順・操作方法

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

- 連番は作成順に4桁のゼロパディングで採番する
- スラッグは判断の主題を英語のkebab-caseで表現する
- ファイル名に `adr-` プレフィックスは付けない（このディレクトリ配下である時点でADRと判断できるため）

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
- 設計途中で考え方が大きく変化した判断
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

---

## 他文書との関係（依存方向）

ADRは他文書を参照する。他文書はADRを現行仕様・運用ルールの根拠として依存しない。

```text
ADR
 └── References → Convention / Specification / Philosophy / Architecture
```

現行仕様はADRではなく各Convention・Specification文書に反映する。ADRはその判断に至った経緯を記録する。

---

## 関連文書（参照先）

- テンプレート: `docs/adr/0000-template.md`
- 命名規則: `docs/conventions/naming.md`（NM-ID-004）
