# ADR Philosophy（ADR設計思想）

## Purpose（目的）

本書は、このプロジェクトにおけるADR（Architecture Decision Record）の設計思想を定義する。

ADRをどのように使うかを説明する文書ではなく、なぜADRを作成するのか・ADRはどのような考え方で運用するのかを定義する。利用方法は `docs/adr/README.md` に委ねる。

---

## Scope（適用範囲）

本書は、このプロジェクトで作成するすべてのADRの設計思想に適用される。

以下は本書の対象外とする。

- ADRの命名規則・Status定義・テンプレート利用方法 → `docs/adr/README.md`
- ADRテンプレートの構成 → `docs/adr/0000-template.md`
- 現行仕様・運用ルールの定義 → 各Philosophy・Architecture・Convention・Specification文書

---

## Core Philosophy（基本理念）

### ADR is a Decision Record（ADRは決定の記録である）

ADRは設計途中のメモや議論ログではない。設計判断が安定した段階で、その判断を整理して保存する文書である。

ADRに記録するのは「何を決めたか」だけでなく、「なぜそう決めたか」「何を検討したか」「何を得たか」である。設計判断の全体像を、将来の設計者が再現できる形で保存する。

### ADR is Created at Design Milestones（ADRは設計フェーズの区切りで作成する）

設計途中で逐次ADRを書くことは目的としない。設計・議論・ドキュメント反映が一区切りした後、その成果を整理してADRとして記録する。

```text
Design（設計・議論）
    ↓
Documentation（文書への反映）
    ↓
Review（レビュー・確定）
    ↓
ADR（判断の整理・記録）
```

この順序により、ADRはリアルタイムの議事録ではなく、確定した設計判断の記録として機能する。

### ADR Does Not Replace Documentation（ADRはDocumentationを置き換えない）

ADRは判断理由を保存する。現行仕様・運用ルールはDocumentationへ反映する。

ADRはDocumentationを参照する立場であり、DocumentationはADRへ現行仕様・運用ルールの根拠として依存しない。現行仕様のSSOTはPhilosophy・Architecture・Convention・Specification・Templateが保持する。

### ADR Preserves Design Knowledge（ADRは設計知識を保存する）

このプロジェクトではADRを「Decision Record」であると同時に「Knowledge Record」として扱う。最終判断だけでなく、そこへ至る思考過程と設計知見も資産として保存する。

そのため、本プロジェクトのADRテンプレートには以下の固有セクションを設ける。

**Decision Evolution**：設計途中の考え方の変遷を記録する。なぜ最初の案が変化し、最終判断に至ったかの経路を保存する。

**Design Insights**：判断を通じて得られた設計知見を、Decisionとは独立して記録する。このセクション単体を読んでも意味が通るように書くことで、知見の抽出・再利用を可能にする。

### ADR Numbers Represent Logical Structure（ADR番号は論理構造を表す）

ADR番号は作成日時の順序ではなく、設計判断の依存関係・論理構造を表す。そのため、ADRを書く順番とADR番号は一致しなくてもよい。

設計全体の構造を俯瞰した上で、依存関係の順序を優先して採番する。これにより、ADRの一覧が設計の論理的な積み上げとして読めるようになる。

本書は、このプロジェクトにおけるADR設計・運用のすべての判断の出発点である。
