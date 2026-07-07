# Documentation Architecture（ドキュメントアーキテクチャ）

## Purpose（目的）

本書は、Documentation Philosophy で定義した思想を、ドキュメント体系・責務・関係性として具体化する。

Documentation Philosophy が「良いドキュメントとは何か」という Why を定義するのに対し、本書はその思想を知識体系の構造へ落とし込む How を定義する。フォルダ構成を説明する文書ではなく、知識体系を成立させる責務・構造・関係性・情報配置を定義することを目的とする。

---

## Scope（適用範囲）

本書は、`docs/` を構成する知識体系の責務・構造・関係性を対象とする。

Repository Architecture が `README.md`・`.github/`・`docs/`・`templates/` というリポジトリ全体のトップレベル要素を定義するのに対し、本書は `docs/` 配下の知識体系のみを扱う。

以下は本書の対象外とする。

- ドキュメント設計思想 → Documentation Philosophy
- リポジトリ全体の構造 → Repository Architecture
- Markdown記法・文書構成・命名規則 → Conventions
- テンプレート・メタデータ・自動生成仕様 → Specifications

---

## Document Structure（ドキュメント体系）

`docs/` は以下の責務領域によって構成する。

```text
docs/
├── philosophy/
├── architecture/
├── conventions/
├── specifications/
└── adr/
```

これらはフォルダではなく、知識を分類する責務領域として定義する。ディレクトリは責務を表現するための結果であり、目的ではない。

---

## Responsibilities（各責務領域の役割）

### philosophy/

価値観・設計思想・判断原則を定義する。

扱うもの: Philosophy・Principles・Vision・Design Intent

扱わないもの: 構造・規約・実装方法

### architecture/

知識体系を構成する構造・責務・関係性を定義する。

扱うもの: ドキュメント構造・Responsibility・Relationship・Information Architecture・Responsibility Matrix

扱わないもの: 思想・Markdown記法・テンプレート仕様

### conventions/

日常運用で守る規約・運用ルールを定義する。

扱うもの: Markdown・Writing・Naming・Branch・Commit・Pull Request・Label

扱わないもの: 思想・システム仕様

### specifications/

実装可能な仕様を定義する。

扱うもの: Repository Profile・Template・Workflow・Metadata・Front Matter・GitHub仕様

扱わないもの: 設計思想・判断理由

### adr/

設計判断の履歴を保存する。

扱うもの: Decision・Context・Consequences

扱わないもの: 現行仕様・運用ルール

ADRはphilosophy・architecture・conventions・specificationsのすべてに対する判断履歴を記録する、横断的な責務領域として位置付ける。

---

## Relationships（責務領域間の関係）

各責務領域は独立して存在するのではなく、上位領域を前提として設計する。

```text
Philosophy
    ↓
Architecture
    ↓
Conventions
    ↓
Specifications
```

上位領域は下位領域の判断基準となる。下位領域は上位領域と矛盾してはならない。

ADRは上記の階層を横断し、任意の責務領域における設計判断の経緯を保存する。現行仕様はArchitecture・Conventions・Specificationsへ反映し、ADRは判断の背景・根拠・影響を記録する場所として使い分ける。

ADRは他の責務領域を参照して判断履歴を記述する。逆方向——他の責務領域がADRを参照して仕様や規約を定義すること——は行わない。ADRへの依存は判断履歴の記録に限定される。

---

## Information Placement（情報の配置ルール）

情報は内容ではなく、答える問いによって配置先を決定する。

| 問い | 配置先 |
| --- | --- |
| なぜそうするのか | philosophy/ |
| どのような構造か | architecture/ |
| どのように運用するか | conventions/ |
| 実装としてどう定義するか | specifications/ |
| なぜその判断を採用したか（判断時点の背景・根拠の履歴） | adr/ |

同じ情報を複数箇所で管理しない。情報は責務を持つ唯一の領域で管理し、必要に応じて他文書から参照する。

---

## Information Architecture（情報アーキテクチャ）

`docs/` における情報は、責務を持つ領域へ配置される。各責務領域は情報の所有者であり、情報はその責務領域によって管理される。

ドキュメント体系はフォルダ構成ではなく知識体系として設計する。構造は、知識の責務を表現するための手段である。

---

## Design Principles（設計原則）

### No Crossing Responsibilities（責務は交差させない）

philosophy・architecture・conventions・specifications・adrの各責務領域は、互いの責務を侵食しない。

ある情報がどの責務領域に属するかは、「それが答える問い」によって一意に決まる。責務の境界が曖昧になった場合は、配置先を変更するのではなく、まず問いを明確化することで解決する。

### Structure Expresses Responsibility（構造は責務を表現する）

フォルダ構成ではなく、情報の責務を先に設計する。責務を定義した結果として構造を決定する。どこに置かれているかがそのドキュメントの責務を示す状態を維持する。

### Classify by Question（問いによって分類する）

情報の種類ではなく、答える問いによって配置先を決定する。同じ種類の情報であっても、それが答える問いが異なれば配置先は異なる。

### Single Owner per Information（情報の所有者を一つにする）

各情報は責務を持つ唯一の領域で管理する。重複管理は行わず、必要な場合は参照によって関連付ける。情報の重複は、更新漏れと矛盾の起点となる。

### Lower Domains Depend on Upper Domains（下位領域は上位領域を前提とする）

Philosophy を基準として、Architecture・Conventions・Specifications の順で具体化する。下位領域を設計する前に、上位領域の定義が確定していることを確認する。

### Layer Dependency Direction（レイヤー依存方向）

各文書は、同一レイヤーまたは上位レイヤーのみを参照する。上位レイヤーは下位レイヤーに依存しない。

```text
Philosophy / Architecture
        ↓
Conventions
        ↓
Specifications
        ↓
Templates
```

下位レイヤーは必要に応じて上位レイヤーを参照・利用する。作成順と依存方向は別物であり、先に作成した文書であっても上位レイヤーに属するならば下位レイヤーを参照しない。

### Mature Domains by Responsibility（責務領域は責務に従って成熟させる）

責務が明確でない限り、新しい責務領域を追加しない。既存領域へ統合できないことを確認した上で、新たな責務領域を設計する。

本書は、このリポジトリにおけるすべてのドキュメント構造設計判断の出発点である。
