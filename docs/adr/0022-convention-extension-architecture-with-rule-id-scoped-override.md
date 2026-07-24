# 0022. 規約はBase／Pattern／Repositoryの3層とし、Rule ID単位で拡張する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-24 |

---

## Context（背景）

Symnousリポジトリ固有のBranch運用（低リスクな定型更新のみ`main`への直接Pushを許可する）を、共通Branch Conventionに対するリポジトリ固有の例外として明示する必要が生じた。

この例外をどう記述するかを検討する過程で、次の3方式を比較した。

- 自然言語で差分だけを説明する
- 共通規約全文をコピーして固有部分を書き換える
- 共通規約のRule IDを対象として、置き換える規則だけを完全な形で明示する

自然言語の差分説明は、共通規約のどの規則が置き換わり、どの規則がそのまま有効なのかを人もAIも読み比べて解釈する必要があり曖昧だった。全文コピーは、共通規約の改訂が自動反映されず、コピー後にどこが固有変更か分かりにくくなり、規約の正本が実質的に分岐する問題があった。

Rule ID単位での明示的な置き換えが最も明確だったが、これはSymnousだけの局所的な話ではなく、Commit Convention・Naming Conventionなど他の規約にも共通して使える拡張モデルだった。各規約が独自の拡張方式を持ち始めると、操作の意味が規約ごとに揺れ、Rule IDの付け方が統一されず、AIも人も共通の方式で解釈できなくなる懸念があった。

---

## Decision（決定）

規約（Convention）は、次の3層構造で拡張する。

```text
Base Convention
    ↓
Pattern Convention（任意）
    ↓
Repository Convention（任意）
    ↓
Effective Convention
```

- Base Convention：共通ルールの正本
- Pattern Convention：Base Conventionを標準的な用途・運用パターンへ具体化した、再利用可能な標準拡張。対象リポジトリはPattern Conventionを持つConventionについて、正確に1つを選択する。Pattern Conventionを持つかどうか、選択を必須とするかは各Base Convention側で定義する
- Repository Convention：標準的なPattern Conventionでは表現できない、個別リポジトリ固有の差分のみを扱う。存在は任意
- Effective Convention：上記を適用した結果として成立する論理的な規約状態。物理ファイルとして存在する必要はない

各Ruleには、`<Convention>-<Scope>-<Category>-<Number>`という4要素のRule IDを付与する。Scopeは、そのRuleを最初に定義したレイヤーまたはPatternを示す識別子とする（例：Base Conventionは`BS`、Repository Conventionでの新規Addは`RP`、Pattern固有のRuleはそのPattern固有コード）。下位Conventionは、既存Rule IDを対象に指定してReplace・Extend・Disableするか、新しいRule IDでAddする。対象Rule IDを指定しない限り、上位Conventionの内容がそのまま継承される。

---

## Rationale（理由）

Rule ID単位の拡張は、共通規約とリポジトリ固有規約の対応関係を明示的に保ちながら、共通規約全文の複製を避けられる。改訂時も、Rule IDが変更されない限り、Override側は影響の有無をRule ID単位で確認できる。

Pattern Conventionという中間層を設けることで、「用途ごとに繰り返し現れる差分」を個別リポジトリのRepository Conventionへ都度書く必要がなくなり、再利用可能な標準拡張として一箇所にまとめられる。Pattern Conventionを持つかどうかをBase Convention側の判断に委ねることで、パターン分岐が不要な規約にまで強制しない。

この仕組みをBranch Convention固有ではなく規約全体の共通基盤として設計したのは、同種の拡張ニーズが将来他の規約にも生じ得るためであり、規約ごとに異なる拡張方式が乱立する事態を避けるためである。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| 自然言語による差分説明のみ | 共通規約のどの規則が置き換わり、どれがそのまま有効かが曖昧になり、人・AIともに2文書を読み比べて解釈する必要がある |
| 共通規約全文をリポジトリ側へコピーして固有部分を書き換える | 共通規約の改訂が自動反映されず、コピー後にどこが固有変更か分かりにくくなり、リポジトリ側の文書が事実上別規約へ分岐し、正本一元化が崩れる |
| Rule ID単位の拡張方式をBranch Convention内だけの局所ルールとして定義する | 同様の拡張ニーズを持つ他の規約が、それぞれ独自の拡張方式を持ち始め、操作の意味・Rule IDの付け方が規約ごとに揺れ、AIが共通方式で解釈できなくなる |
| Convention拡張の対象範囲を規約以外の文書（Specification・Template等）にも最初から一般化する | 現時点で具体的な適用対象がBranch Conventionのみであり、実例が乏しい段階での一般化は時期尚早と判断した（Design When Needed） |

---

## Consequences（影響・注意点）

- 各Base Conventionは、自身がPattern Conventionを持つかどうか、選択を必須とするかを個別に定義する
- Pattern Conventionの実体名（Branching Modelなど）は、各Convention側でその領域に応じた名称を与えてよい。「Pattern Convention」という呼称自体は共通アーキテクチャ上の名称として維持する
- Rule IDの具体的な記法（Replace／Extend／Disable／Addの定義、見出し形式、ファイル配置規則、検証条件）はConvention Extension Specificationが定義し、本ADRの対象外とする
- 下位Conventionは上位Convention全文を複製せず、操作対象のRuleだけを完全な有効内容として記載する
- この仕組みの規約以外への一般化は、実際の適用需要が生じた時点で改めて検討する

---

## Related Documents（関連文書）

- `docs/architecture/convention-extension.md`
- `docs/specifications/convention-extension.md`
- `docs/conventions/README.md`
- ADR 0009（共通ルールへの例外はRepository Overrideとして明示する）
- ADR 0011（Conventionは採用後の共通ルールのみを定義し、採用の可否は扱わない）
- design-notes 0006（Branch Convention再設計とBranching Model確立）
