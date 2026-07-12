# Design Record Philosophy（デザインレコード設計思想）

## Purpose（目的）

本書は、このプロジェクトにおけるDesign Recordの設計思想を定義する。

Design Recordをどのように作成するかを説明する文書ではなく、なぜDesign Recordが必要なのか・Design Recordはどのような考え方で運用するのかを定義する。作成方法・粒度・生成プロセスは、後続の文書に委ねる。

設計判断（Architecture Decision）と設計検討（Design Exploration）は責務が異なる。ADRは前者を記録するが、後者を記録する場所はこれまで存在しなかった。Design Recordは、この検討過程を独立した設計資産として保存するために存在する。

---

## Scope（適用範囲）

本書は、このプロジェクトで作成するすべてのDesign Recordの設計思想に適用される。

以下は本書の対象外とする。

- Design Recordの命名規則・ファイル構成・ディレクトリ構造 → 将来のSpecification相当文書
- Design Recordの粒度・分割基準 → Guideline
- ライフサイクル・生成順序・Raw Chat Archiveからの抽出プロセス・Decision Mining・AIによる抽出・Review手順 → Process
- 現行仕様・運用ルールの定義 → 各Philosophy・Architecture・Convention・Specification文書

---

## Core Philosophy（基本理念）

### Design Record is an Exploration Record（Design Recordは検討の記録である）

Design Recordが保存するのは、設計背景・検討過程・比較した案・議論の流れ・判断候補・未採用案である。これらは判断そのものではなく、判断に至る過程の記録である。

ADRが「何を決めたか」を記録するのに対し、Design Recordは「何を検討したか」を記録する。両者は同じ設計事象を異なる責務で記録する成果物である。

### Design Record Does Not Define Decisions（Design Recordは判断を定義しない）

Design Recordの中にある種の結論や有力な方向性が記されていたとしても、それは正式な設計判断ではない。何が採用されたかを定義する権限はADRのみが持つ。

Design Recordを読むだけで、現在有効な判断が何かを断定してはならない。

### Design Record Preserves Discarded Paths（Design Recordは採用されなかった案を保存する）

ADRのAlternatives Consideredは、意思決定に必要な要素へ要約される。Design Recordはその過程の詳細——なぜその案が検討され、なぜ採用に至らなかったかという文脈——を保存する。

採用されなかった情報は無価値ではない。将来同じ議題を再検討する際、なぜその案が一度退けられたかを知ることは、同じ検討を繰り返さないための資産になる。

### Design Record Does Not Replace Documentation（Design RecordはDocumentationを置き換えない）

現行仕様・運用ルールのSSOTは、Philosophy・Architecture・Convention・Specificationが保持する。Design Recordがどれだけ詳細であっても、現行仕様の根拠として参照されることはない。

DocumentationはDesign Recordへ依存しない。

### Design Record Does Not Replace ADR（Design RecordはADRを置き換えない）

何が最終的に採用されたかの正式な記録はADRが担う。Design Record単体を読んでも、それが現在有効な判断かどうかは判断できない。

Design RecordとADRは、どちらか一方が他方を包含する関係ではなく、責務が独立した並立する記録である。

### Design Record Does Not Always Converge（Design Recordは必ずしも結論に収束しない）

検討の記録は、必ずしも単一の結論やADRへ結びつくとは限らない。保留・断念・未解決のまま終わった検討にも、将来同じ議題を再検討する際の資産としての価値がある。

Design RecordはADRの前提条件ではない。ADRへ発展しなかった検討であっても、独立した記録として存在してよい。

---

本書は、このプロジェクトにおけるDesign Recordに関する設計判断の基本原則を定義する。
