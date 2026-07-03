# Template Philosophy（テンプレート設計思想）

## Purpose（目的）

本書は、`templates/` 領域の設計思想を定義する。

`templates/` は、共通Conventionを個別リポジトリへ適用するための初期雛形・案内部品を管理する領域である。Templateは規約本文の正本ではなく、共通Conventionを複製せず参照することを基本とする。

---

## Scope（適用範囲）

本書は `templates/` 配下のすべてのTemplateファイルに適用される。

以下は本書の対象外とする。

- 規約本文の定義 → `docs/conventions/`
- テンプレート構造・ファイル仕様の詳細 → Specifications
- 個別リポジトリ固有の運用ルール → 各リポジトリのドキュメント

---

## Core Philosophy（基本理念）

### Template as Entry Point（テンプレートは入口である）

Templateは、リポジトリ作成時に必要な初期構成を提供する。しかし、完成済みの運用規約を丸ごとコピーするものではない。

各リポジトリは、Templateを通じて共通Conventionへの入口を持つ。Templateの役割はConventionへ到達させることであり、Conventionを代替することではない。

---

## Design Principles（設計原則）

### Keep Convention as Source of Truth（規約の単一情報源を維持する）

規約本文の正本は `docs/conventions/` に置く。`templates/` はConvention本文を複製してはならない。

### Provide Entry Points（入口を提供する）

Templateは、個別リポジトリの利用者・開発者が必要な規約へ到達できる入口を提供する。特に `CONTRIBUTING.md` は、開発参加規程の入口として機能する。

### Organize by Artifact（成果物単位で管理する）

Templateは成果物の種類によって管理する。どの成果物をどのように組み合わせるかは、Templateの責務ではなく、リポジトリ構築手順の責務とする。

### Avoid Premature Abstraction（早期の抽象化を避ける）

実際の利用場面が明確でない分類軸は追加しない。必要性が明確になった時点で、ArchitectureまたはADRで追加を検討する。

### Minimize Repository Duplication（リポジトリ間の重複を最小化する）

個別リポジトリには、必要最小限の案内文と初期ファイルのみを配置する。共通ルールの改定時にすべてのリポジトリへ同じ修正を反映する必要がある構造は避ける。

---

## Relationships（関係性）

### Relationship to Conventions（Conventionとの関係）

Conventionは、共通認識・共通語彙・最低限の判断基準を定義する。Templateは、そのConventionを個別リポジトリで利用しやすくするための入口・雛形を提供する。

### Relationship to Individual Repositories（個別リポジトリとの関係）

個別リポジトリは、Templateを通じて初期構成を取得する。ただし、個別リポジトリ固有の運用差分はTemplateに戻して一般化しない。共通化できると判断された場合のみ、ConventionまたはTemplateへ反映する。

---

## Non-Goals（対象外）

`templates/` は以下を目的としない。

- Convention本文の正本を管理すること
- すべてのリポジトリ運用を完全自動生成すること
- リポジトリ用途別の完成済み規約を大量に複製すること
- 個別リポジトリ固有ルールを中央管理すること
- 各リポジトリの設計判断（運用モデル・構成・方針）を代替すること

本書は、`templates/` 領域を設計・運用する際の基本理念を定義する。
