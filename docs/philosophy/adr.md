# ADR Philosophy（ADR設計思想）

## Purpose（目的）

本書は、このプロジェクトにおけるADR（Architecture Decision Record）の設計思想を定義する。

ADRをどのように使うかを説明する文書ではなく、なぜADRを作成するのか・ADRはどのような考え方で運用するのかを定義する。利用方法は `docs/adr/README.md` に委ねる。

ADRは、確定した設計判断（Architecture Decision）を記録する成果物である。判断に至るまでの設計検討・比較過程はDesign Recordが担い、ADRは意思決定とその根拠に責務を絞る。

---

## Scope（適用範囲）

本書は、このプロジェクトで作成するすべてのADRの設計思想に適用される。

以下は本書の対象外とする。

- ADRの命名規則・Status定義・テンプレート利用方法 → `docs/adr/README.md`
- ADRテンプレートの構成 → `docs/adr/0000-template.md`
- 詳細な設計検討・比較検討の全文・議論の流れ・未採用案の詳細 → Design Record Philosophy・Design Record
- 現行仕様・運用ルールの定義 → 各Philosophy・Architecture・Convention・Specification文書

---

## Core Philosophy（基本理念）

### ADR is a Decision Record（ADRは決定の記録である）

ADRは設計途中のメモや議論ログではない。設計判断が安定した段階で、その判断を整理して保存する文書である。

ADRに記録するのは「何を決めたか」だけでなく、「なぜそう決めたか」「何を得たか」である。設計判断の全体像を、将来の設計者が再現できる形で保存する。

### ADR Preserves Decision Rationale（ADRは判断根拠を保存する）

ADRは「Decision Record」である。最終的に採用した判断と、その判断に至った根拠を保存する。

詳細な設計検討・比較した案の全容・議論の流れ・未採用案の詳細はDesign Recordが保存する。ADRはその中から、意思決定を理解するために必要最小限の背景・根拠・比較のみを記録する。

現行のADRテンプレートには、これまでの思想を反映した「Decision Evolution」「Design Insights」という固有セクションが存在する。これらのセクションが担うべき責務の見直しは本書の改定範囲には含めず、今後のADRテンプレート改定において扱う。

### ADR is Created at Design Milestones（ADRは設計フェーズの区切りで作成する）

設計途中で逐次ADRを書くことは目的としない。設計・議論・ドキュメント反映が一区切りした後、その成果を整理してADRとして記録する。

この考え方により、ADRはリアルタイムの議事録ではなく、確定した設計判断の記録として機能する。

### ADR Does Not Replace Documentation（ADRはDocumentationを置き換えない）

ADRは判断理由を保存する。現行仕様・運用ルールはDocumentationへ反映する。

Documentationは、現行仕様・運用ルールの根拠としてADRへ依存しない。現行仕様のSSOTはPhilosophy・Architecture・Convention・Specification・Templateが保持する。

### ADR Does Not Replace Design Record（ADRはDesign Recordを置き換えない）

ADRは意思決定に必要な要素に絞った記録である。設計検討の詳細な過程・比較検討の全体像・議論の流れ・未採用案の詳細はDesign Recordが保持し、ADR単体でその全容を再現することは目的としない。

ADRとDesign Recordは、どちらか一方が他方を包含する関係ではなく、責務が独立した並立する記録である。

### ADR Numbers Represent Logical Structure（ADR番号は論理構造を表す）

ADR番号は作成日時の順序ではなく、設計判断の依存関係・論理構造を表す。そのため、ADRを書く順番とADR番号は一致しなくてもよい。

設計全体の構造を俯瞰した上で、依存関係の順序を優先して採番する。これにより、ADRの一覧が設計の論理的な積み上げとして読めるようになる。

本書は、このプロジェクトにおけるADRに関する設計判断の基本原則を定義する。
