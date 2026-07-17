# Convention Extension Architecture（規約拡張アーキテクチャ）

## Purpose（目的）

本書は、共通規約を正本として維持しながら、Pattern ConventionおよびRepository ConventionによってRule ID単位で段階的に拡張し、各リポジトリで有効となるEffective Conventionを成立させるための責務・関係性・適用構造を定義する。

Conventionは一枚岩の文書として個別リポジトリごとに複製されるものではなく、Base Conventionを起点として段階的に具体化・調整されるレイヤー構造を持つ。本書は、この拡張構造を成立させる責務・関係性・適用順序を定義するものであり、具体的な構文仕様や記述形式を定義するものではない。

---

## Scope（適用範囲）

本書は、Convention拡張を構成するレイヤーの責務・関係性・適用構造を対象とする。

対象は以下を含む。

- Base Convention・Pattern Convention・Repository Convention・Effective Conventionの4層
- Convention間の関係
- 拡張の適用順序
- Convention間の優先関係
- Rule IDを参照境界とする考え方
- 各Conventionの管理責務
- Effective Conventionの正本性および派生性

以下は本書の対象外とし、後続のSpecificationへ委ねる。

- Replace・Extend・Disable・Addなど各操作の具体的な記法および厳密な意味
- 操作を記述する見出し形式および構造化メタデータの項目
- Rule IDの具体的なフォーマットおよびBS・RP・Pattern識別子などの具体値
- ファイル名およびディレクトリ配置の詳細規則
- 重複や不正参照の機械的なエラー条件
- Effective Conventionの生成アルゴリズムおよび自動検証方法
- 既存Rule IDの移行手順

---

## Convention Layers（規約レイヤー）

Convention拡張は、以下の4層によって構成する。

### Base Convention

共通規約の正本である。

複数のリポジトリへ共通して適用する基本ルールと設計原則を定義する。下位Conventionが拡張する起点となる。

### Pattern Convention

Base Conventionを標準的な用途または運用パターンへ具体化する。

再利用可能な標準拡張として扱う。Architecture全体としては任意のレイヤーであり、Pattern Conventionを持つかどうか、選択を必須とするか、選択可能数をどうするかは、各Base Convention側で定義できるものとする。

### Repository Convention

個別リポジトリ固有の事情に応じて最終調整する。

標準的なPattern Conventionでは表現できない差分を扱う。必要な場合だけ存在する。再利用可能な差分を安易にRepository Conventionへ閉じ込めない。

### Effective Convention

適用対象で実際に有効となる最終的な規約状態である。

Pattern ConventionまたはRepository Conventionの有無にかかわらず常に成立する。物理ファイルとして存在することは必須ではない。

---

## Responsibilities（各レイヤーの責務）

各レイヤーの責務を以下のように整理する。

- Base Convention：共通ルールと設計原則を定義する
- Pattern Convention：Base Conventionを標準的な用途へ具体化する
- Repository Convention：標準パターンでは表現できない個別事情に応じて最終調整する
- Effective Convention：実際に適用される最終的な規約状態を表す

各レイヤーの責務は重複しない。

Repository Conventionは、単に各リポジトリで自由にルールを作るための領域ではない。標準化によって再利用可能な差分はPattern Conventionへ属し、Repository Conventionはそれでも表現できない個別事情のみを扱う。

---

## Extension Flow（拡張の経路）

拡張は、以下の単一の基本フローに従って適用する。

```text
Base Convention
    ↓
Pattern Convention（任意）
    ↓
Repository Convention（任意）
    ↓
Effective Convention
```

Pattern ConventionとRepository Conventionは、それぞれ独立して省略できる。

両方を省略した場合は、Base Conventionの通常適用となる。少なくとも一方を適用した場合は、拡張フローとなる。

Repository Conventionを適用する場合、Pattern Conventionが存在しなければBase Conventionの適用後に、Pattern Conventionが存在すればその適用後に適用する。

Pattern ConventionとRepository Conventionの有無にかかわらず、Effective Conventionは常に成立する。

---

## Precedence（優先関係）

Convention間の優先関係は、以下の順序を持つ。

```text
Repository Convention
    >
Pattern Convention
    >
Base Convention
```

ただし、これは3文書を比較して最も優先度の高い記述を単純に採用する仕組みではない。

優先関係は、以下の逐次適用モデルとして成立する。

```text
Base Convention
    ↓
Pattern Convention
    ↓
Repository Convention
    ↓
Effective Convention
```

後段のConventionは、直前までに成立している有効状態に対して作用する。Repository Conventionは、Base Conventionだけではなく、適用済みのPattern Conventionによって追加または変更されたRuleも対象にできる。

暗黙的な上書きは認めず、どのRuleへ作用するかを明示することを原則とする。

---

## Rule Reference Model（Rule参照モデル）

Convention拡張は、以下の原則に基づいてRuleを参照・拡張する。

- Rule IDをConvention間の安定した参照境界とする
- すべてのConvention Ruleは、定義レイヤーを識別可能な統一されたRule IDを持つ
- 下位ConventionはRule IDを指定して、現在有効なRuleへ作用する
- Rule IDの具体的な構成はSpecificationで定義する
- 下位Conventionに記載されていないRuleは、直前の有効状態から継承される
- 操作対象のRuleは、下位Convention内で完全な有効内容を確認できるように記述する
- 上位Convention全文を下位Conventionへ複製しない
- 同一Convention文書内では、同じRule IDへ複数回作用しない
- Rule IDの変更または削除時には、下位Conventionと参照箇所への影響を確認する

ここでいう「完全な有効内容」とは、Rule本文だけでなく、そのRuleを構成するRequirement・Source・Reason・Examples・Notes・Exceptionsなどを含む。

具体的な操作種別や記述形式はSpecificationへ委ねる。

---

## Effective Convention（有効規約）

Effective Conventionは、以下の性質を持つ。

- Base Convention・Pattern Convention・Repository Conventionを適用した論理的な規約状態である
- Pattern ConventionまたはRepository Conventionが存在しない場合でも成立する
- 物理ファイルとして保存する必要はない
- 自動生成する場合、生成ファイルは派生成果物であり正本ではない
- 生成されたEffective Conventionを直接編集してはならない
- 元となるConvention群から常に再導出可能でなければならない
- 適用判断の根拠は、正本であるConvention群にある

Effective Conventionは、独立した第4の編集レイヤーではない。

---

## Management Boundaries（管理責務の境界）

Convention拡張における管理責務は、以下のように定義する。

- Base Conventionは共通`.github`リポジトリで管理する
- Pattern Conventionは共通`.github`リポジトリで管理する
- Repository Conventionは各対象リポジトリで管理する
- Effective Conventionは論理的に導出する
- Effective Conventionを生成する場合は、対象リポジトリ側の派生成果物として扱う
- 下位Conventionは上位Conventionの正本全体を複製せず、必要なRuleだけを保持する

この構造により、共通規約の正本が個別リポジトリへ分散することを防ぐ。

---

## Design Principles（設計原則）

### Single Source of Truth（単一情報源）

Base Conventionを共通ルールの正本とする。Pattern ConventionおよびRepository Conventionは、それぞれの責務に属する拡張内容の正本とし、Base Conventionの代替または複製として扱わない。Effective Conventionの生成物は正本として扱わない。

- Base Convention：共通ルールの正本
- Pattern Convention：標準パターンに属する拡張内容の正本
- Repository Convention：リポジトリ固有の拡張内容の正本
- Effective Convention：派生状態であり正本ではない

各レイヤーは自身の責務に属する情報だけを管理する。

### Layered Extension（階層的拡張）

Conventionを独立した断片ではなく、順序を持つ拡張レイヤーとして適用する。後段は直前までの有効状態を対象とする。レイヤーを飛び越えた暗黙的な解釈を避ける。

### Rule-Level Clarity（Rule単位の明確性）

Rule IDを参照および拡張の単位とする。操作対象Ruleは、下位Convention単体でも有効内容を理解できる形で記述する。文書全体の複製と、差分だけでは意味を理解できない断片的記述の両方を避ける。

### Explicit Precedence（明示的な優先関係）

Convention間の適用順序と優先関係を明示する。暗黙の上書き、ファイル読み込み順への依存、解釈者ごとの差異を避ける。Effective Conventionが一意に導出できる構造を維持する。

---

## Design Constraints（設計上の制約）

- 下位Conventionは上位Conventionの基本目的や設計原則を覆してはならない
- 基本目的が異なる再利用可能な運用は、新しいPattern Conventionとして定義することを検討する
- 規約の対象領域自体が異なる場合は、新しいBase Conventionとして分離することを検討する
- Pattern Conventionは、Repository Conventionへ同種の例外が重複することを防ぐ標準化レイヤーでもある
- Repository Conventionは、Pattern Conventionを置き換えるための無制限な例外領域ではない
