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
- ADRの設計思想 → ADR Philosophy（`docs/philosophy/adr.md`）
- ADRの運用方法・design-notesの利用方法 → 各ディレクトリのREADME

---

## Document Structure（ドキュメント体系）

`docs/` は以下の責務領域によって構成する。

```text
docs/
├── philosophy/
├── architecture/
├── conventions/
├── specifications/
├── adr/
└── design-notes/
```

これらはフォルダではなく、知識を分類する責務領域として定義する。ディレクトリは責務を表現するための結果であり、目的ではない。

`docs/` 配下の領域は、性質によって3つに分かれる。

| 領域 | 性質 |
| --- | --- |
| philosophy / architecture / conventions / specifications | 現在有効な知識・規範を構成する |
| adr | 正式な判断履歴を保存する。規範ではない |
| design-notes | 自由な作業記録。非規範・非正式 |

philosophy・architecture・conventions・specificationsは現在有効な知識体系を構成する規範的領域である。adrは正式な判断履歴を保存する領域であり、規範そのものではない。design-notesは非規範的な作業領域であり、正式な知識体系の一部としては扱わない。詳細はDesign-Notes Domainを参照する。

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

確定した設計判断について、その背景・理由・却下した案・影響を記録した**正式な履歴記録**を保存する。

扱うもの: 独立して覆せる単位に分割された設計判断・その背景・理由・却下した案・影響

扱わないもの: 現行仕様そのもの（現行仕様はConvention・SpecificationがSSOT）・運用手順・確定前の思考過程そのもの（思考過程はdesign-notesが持つ）

ADRはphilosophy・architecture・conventions・specificationsのすべてに対する判断履歴を記録する、横断的な責務領域として位置付ける。ただし、ADRは**現在有効な規範ではない**。現在有効な規範は各Convention・Specificationが持ち、ADRはそこに至った判断の理由を将来へ説明可能にするための記録に徹する。

### design-notes/

設計に関する議論・疑問・比較・保留事項などを、任意の完成度・形式で保存する。

扱うもの: 設計中の論点・比較・疑問・保留事項・途中または最終的な結論を含む自由形式の記録

扱わないもの: ADRとして整理・抽出された正式な決定記録（正式な記録はadr/が持つ）

design-notesの境界は「確定しているかどうか」ではない。検討の中で結論に至った内容が含まれていてもよく、整理された比較メモや論点整理であってもよい。ADRとの違いは文書形式ではなく、責務と成熟度にある。design-notesは検討のための非公式な作業記録であり、ADRは記録要否基準を満たす確定した設計判断を、正式な判断履歴として保存する。同じ決定について両方に記述が存在してよく、design-notes側は検討過程としての価値を、adr/側は将来参照するための正式な判断履歴としての価値を持つ。

design-notesは非規範的な作業領域であり、Convention・Specificationへの準拠を要求しない。書式・構造・粒度・ライフサイクルを定義せず、識別と保管のための最低限の存在意義のみをここで定義する。詳細はDesign-Notes Domainを参照する。

---

## Design-Notes Domain（design-notes領域の位置づけ）

design-notesは、他の責務領域と異なり、知識体系としての完成度・一貫性を求めない領域である。本書がdesign-notesについて定義するのは以下の3点のみに限定する。

- 何を置く場所か：設計に関する議論・疑問・比較・保留事項の置き場所（結論に至った内容を含んでよい）
- 規範性がないこと：Convention・Specificationへの準拠を要求しない
- 正式な判断根拠にはしないこと：design-notesの内容そのものを規範や正式な設計判断の根拠として依存しない（参照は妨げない。詳細はRelationshipsを参照）

design-notesには、識別のための最小限の命名規則のみを設ける。命名規則の具体的な形式は `docs/design-notes/README.md` が所有し、本書では定義しない。命名規則を除く、文書の書式・構造・粒度・ライフサイクル・Statusは現時点では定義しない。将来、実運用上の必要性が確認された場合にのみ見直す。先回りして定義しようとすると、design-notesが再び正式資産化し、Documentation Philosophyの各原則（Single Owner per Informationなど）を過剰に適用する対象になってしまう。

---

## Relationships（責務領域間の関係）

規範性を持つ責務領域（philosophy・architecture・conventions・specifications）は、独立して存在するのではなく、上位領域を前提として設計する。

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

現行Documentation（philosophy・architecture・conventions・specifications）は、内容を成立させるためにADRへ依存してはならない。現在有効な規則を理解するために対応するADRを読む必要がある設計は避ける。ただし、判断履歴への補助リンクとしてADRを参照することは妨げない（例：「判断理由はADR-0003を参照」）。

design-notesについても同様に、依存と参照を分ける。design-notesは規範や正式な設計判断の根拠として依存されてはならない。ADRは、design-notesの内容をそのまま判断根拠とせず、確定した判断・理由をADR自身の本文で自己完結させる。ただし、ADRのContextなどで検討過程の補足資料としてdesign-notesを参照することは妨げない。

design-notesに含まれる設計判断がADRの記録対象となる場合は、ADRへ抽出する。ADR対象外の内容（軽微な運用改善・自明な仕様整理・汎用的な思想の発見など）は、必要に応じて責務を持つ現行Documentationへ直接反映してよい。design-notesからの情報移動経路はADRに限定されない。

```text
design-notes（非規範・依存されない）
    ├─ ADR記録対象となる判断 → adr/（正式な履歴記録）
    └─ ADR対象外の内容       → 責務を持つ現行Documentationへ直接反映
```

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
| 検討過程・論点・比較・保留事項をどこに残すか（結論を含んでもよい） | design-notes/ |

同じ情報を複数箇所で管理しない。情報は責務を持つ唯一の領域で管理し、必要に応じて他文書から参照する。design-notesは例外的に、内容の重複・矛盾・陳腐化を許容する。これはdesign-notesが正式な知識体系に属さないためであり、Single Owner per Informationの原則はphilosophy・architecture・conventions・specifications・adrにのみ適用される（適用範囲の詳細はDesign Principlesを参照）。

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

ここでの重複とは、**同一の責務を持つ情報**が複数箇所に存在することを指し、同一テーマについて異なる責務の記述が存在することは重複に当たらない。例えば、ADRが「なぜmain-onlyを採用したか」という理由・履歴を持ち、Conventionが「現在main-onlyをどう運用するか」という規範を持つことは、同じテーマを扱っていても責務が異なるため重複ではない。

この原則はphilosophy・architecture・conventions・specifications・adrに適用する。ただし、各領域が所有する責務の範囲内に限る。design-notesは例外とし、この原則の対象外とする。

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
