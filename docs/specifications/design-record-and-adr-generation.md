# Design Record and ADR Generation（Design Record・ADR生成プロセス）

## Purpose（目的）

本書は、設計・議論が一区切りした後、利用可能な一次情報と現行Documentationをもとに、Design RecordおよびADRを生成する標準工程を定義する。

このプロセスは、特定のAIサービスやツールに依存しない。人間または任意のAIが、利用可能な情報に基づいて実行できる工程として定義する。

---

## Scope（適用範囲）

本書は、Design RecordおよびADRを生成するための工程を対象とする。

以下は本書の対象外とする。

- 特定AI向けのプロンプト
- Raw Chat Archiveのエクスポート仕様・ブラウザ拡張機能の操作方法
- 自動化スクリプト・ベクトル検索・知識化
- 知識管理基盤との連携
- Gitのコミット手順
- Design RecordおよびADRのテンプレート設計そのもの → `docs/design-records/0000-template.md`、`docs/adr/0000-template.md`
- Design Recordの思想・運用 → `docs/philosophy/design-record.md`、`docs/design-records/README.md`
- ADRの思想・運用 → `docs/philosophy/adr.md`、`docs/adr/README.md`

---

## Generation Phases（生成フェーズの全体像）

以下は標準的な生成フロー（Standard Generation Flow）の一例である。すべての場合にこの順序通り進むとは限らない。

```text
Source Collection
        ↓
Design Exploration Extraction
        ↓
Design Record Creation
        ↓
Design Record Review
        ↓
Decision Identification
        ↓
Decision Review
        ↓
ADR Creation
        ↓
Consistency Review
        ↓
Traceability Update
```

本プロセスは、Design Record作成からADR作成までの標準的な流れを示す。ただし、各成果物は必ず生成されるとは限らず、次のパターンをすべて許容する。

- ADRへ発展しないDesign Record（Phase 1〜4で終了する）
- Design Recordを経由しないADR（Phase 5以降から直接開始する）
- 複数のDesign Recordから作成される1つのADR
- 1つのDesign Recordから作成される複数のADR

---

## Phase 1 — Source Collection（一次情報の収集）

利用可能な一次情報と関連Documentationを収集する。

**収集対象の例:**

- Raw Chat Archive
- 会議記録・作業メモ
- 現行Documentation
- 既存Design Record
- 既存ADR
- Git履歴・レビュー記録

特定のブラウザ拡張機能・AIサービス・エクスポート方法には依存しない。Raw Chat Archiveは必須ではない。利用可能な情報から必要十分な記録を作成することを前提とする。

---

## Phase 2 — Design Exploration Extraction（設計検討の抽出）

収集した一次情報から、設計検討のまとまりを抽出する。

**抽出対象の例:**

- 設計背景
- Question
- 比較案
- 議論の変化
- 保留案
- 未採用案
- 暫定的な結論
- 検討から得られた知見

Design Recordの粒度は、`docs/design-records/README.md` の緩やかな方針に従う。厳密な機械的基準は適用しない。

---

## Phase 3 — Design Record Creation（Design Recordの作成）

抽出した設計検討を、Design Recordテンプレート（`docs/design-records/0000-template.md`）に従って記録する。

この段階では、正式なArchitecture Decisionを定義しない。Conclusionが存在する場合も、あくまで検討の暫定的な到達点として記録し、正式な判断としては扱わない。

---

## Phase 4 — Design Record Review（Design Recordのレビュー）

作成したDesign Recordについて、次を確認する。

- 一次情報を不当に省略・歪曲していないか
- Questionと検討過程が追跡できるか
- ADRやDocumentationの責務が混入していないか
- 関連する検討が欠落していないか
- 分割・統合の粒度が不自然ではないか

必要な修正を行った後、Design Record本文を確定する。確定後の本文は、`docs/design-records/README.md`のImmutabilityに従い、原則として書き換えない。

---

## Phase 5 — Decision Identification（Decision候補の識別）

Design Recordおよび利用可能な関連情報（Documentation・既存ADR・その他の一次情報を含む）から、ADRとして保存すべきArchitecture Decisionを識別する。

**ADR候補の基準:**

- 複数の案から選択した判断である
- 将来「なぜそうなっているか」を知る必要がある
- 他の設計へ影響を与える
- 将来変更・再検討される可能性がある
- 判断根拠や影響を独立して保存する価値がある

すべてのConclusionをADR化しない。基準を満たさない場合は、Design Recordに記録されたままで完結してよい。

---

## Phase 6 — Decision Review（Decision候補のレビュー）

ADR候補ごとに、次を確認する。

- Decisionとして独立しているか
- 既存ADRへ統合すべきではないか
- 上位のDecisionに吸収されていないか
- 単なる現行仕様・運用ルールではないか
- ADRとして保存する重要性があるか
- Decisionとして十分成熟しているか（結論が曖昧なままDesign Recordで終えるべきではないか）

レビュー結果は、対応するDesign RecordのReview Historyへ追記する。

---

## Phase 7 — ADR Creation（ADRの作成）

ADR化すると判断したDecisionを、ADRテンプレート（`docs/adr/0000-template.md`）に従って記録する。

**集中する項目:**

- Decision
- Decision Rationale
- Decision Evolution
- 最小限のAlternatives
- Consequences
- Related Documents

Design Recordにある詳細な検討過程を再掲しない。Decision Evolutionには、Design Recordの探索全体ではなく、採用されたDecisionが辿った変遷のみを要約する。

---

## Phase 8 — Consistency Review（整合性レビュー）

作成したADRについて、次を確認する。

- Design Recordと矛盾していないか
- 現行Documentationと矛盾していないか
- ADR単体でDecisionを理解できるか
- 詳細な検討過程を過剰に含んでいないか
- Decision Evolutionが探索全体ではなく、採用したDecisionの成熟履歴になっているか
- Design Insightsを独立した責務として復活させていないか

---

## Phase 9 — Traceability Update（追跡情報の更新）

Design Record・ADR・Documentationの関連情報を更新する。

具体的なリンク書式や自動化方法は、各README・テンプレートおよび将来のConventionへ委ねる。

---

## Process Principles（プロセス上の原則）

- 設計活動と記録作業を分離する
- 各成果物には、その成果物の責務に属する情報のみを記録する
- Design RecordはExplorationを保存する
- ADRはDecisionを保存する
- DocumentationはCurrent Stateを保存する
- 情報の完全な複製を避け、必要な要約と参照で関連付ける
- 一次情報が完全でなくても、利用可能な情報から必要十分な記録を作成する
- 不明な情報を推測で補完しない
- AIの出力は確定成果物ではなく、レビュー対象のドラフトとして扱う
- 完璧な網羅性より、追跡可能で誠実な記録を優先する

---

## Notes（補足）

本プロセスはDesign RecordおよびADRの生成のみを対象とする。

Design Record・ADRそれぞれの思想・責務・運用・テンプレート仕様は、本書ではなく対応するPhilosophy・README・Templateに従う。
