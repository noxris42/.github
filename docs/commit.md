# Commit Convention

## Purpose

本書は、Commitの意味単位とCommit Messageの記述方法を定める。

Commitは単なるファイル変更の記録ではなく、何を目的として変更したかを保持する単位である。

## Commit Semantic Unit

1つのCommitは、1つのChange Subject（変更主体）に対する1つのSemantic Purpose（変更目的）を表す。

- Commitの単位はファイル数や作業時間ではなく、変更の意味によって決める。
- 複数ファイルの変更でも、1つの変更主体と目的に従属する場合は同一Commitに含めてよい。
- 独立した変更主体または変更目的が複数ある場合は、Commitを分割する。
- 複数の変更をまとめるためだけに、実在しない上位の変更主体を作らない。

変更主体には、機能、概念、モデル、設定、文書、インフラなどが該当し得る。

変更されたファイルそのものを、無条件に変更主体とみなさない。

## Message Structure

Commit Messageは必須のHeaderと任意のBodyから構成する。

```text
<gitmoji> <type>: <subject>

<body>
```

- Header形式は固定とする。
- GitmojiとTypeの間は半角空白1つとする。
- Typeの後にはコロンと半角空白1つを置く。
- Scopeは使用しない。
- Bodyを記述する場合は、Headerとの間に空行を1つ置く。

## Type and Gitmoji

Typeは変更のSemantic Purposeから選択する。

ファイル拡張子、変更ディレクトリ、使用ツールなどの物理的属性だけで判断しない。

TypeとGitmojiは次の対応を使用する。

| Gitmoji | Type | Meaning |
| --- | --- | --- |
| ✨ | `feat` | 機能・Capabilityの成立または変更 |
| 🐛 | `fix` | 意図された動作・設定への回復 |
| ⚡ | `perf` | 動作を維持した性能・効率の改善 |
| 📦 | `build` | 依存関係・Build・Packaging・生成物の変更 |
| ⏪ | `revert` | 過去の変更効果の取り消し |
| 📝 | `docs` | 文書内容・定義の成立または変更 |
| ♻️ | `refactor` | 動作を維持した内部構造の変更 |
| 💄 | `style` | 意味・動作を変えない表示や体裁の変更 |
| ✅ | `test` | Test・Test Infrastructureの変更 |
| 👷 | `ci` | CI/CD Automationの変更 |
| 🔧 | `chore` | Repository Maintenanceを目的とする変更 |

Typeは上記11種類に限定し、対応するGitmojiを使用する。

`chore`はRepository保守そのものが目的である場合に使用する。分類困難な変更のFallbackとして使用しない。

## Subject

SubjectはChange Subject Representation（変更主体の表現）とOperation Representation（操作の表現）から構成する。

Subjectは、そのCommitの変更目的に沿って、変更主体に実際に成立した意味・成果を表す。個々のファイル変更や参照追加などの具体的な操作は、それ自体が変更目的である場合に表す。目的として掲げただけで、そのCommitでは成立していない成果を記述しない。変更理由の詳細は含めない。

日本語のSubjectは、対象を表す名詞句と、その対象に生じた状態変化を表す操作を組み合わせ、次の形を基本として簡潔に記述する。

- `○○を<操作>`：変更主体を対象とする。
- `○○の△△を<操作>`：変更主体の特定の部分・側面を対象とする。

`○○`と`△△`はファイル名に限定せず、変更目的の中心となる意味的対象を表す。

### Change Subject Selection

変更主体は、Commitの変更目的の中心となる意味的対象として確定する。

変更ファイルの名前や配置だけから変更主体を決定しない。

### Change Subject Representation

変更主体を確定した後、その主体を適切に表す名称を選択する。

- 既存の名称や識別子を参考にし、対象の同一性を維持する。
- 正式な英語名称が存在しても、Subjectでその表記を厳密に使用することは必須としない。
- 意味が正しく伝わる場合は、日本語表現や自然な略称を使用してよい。
- 既存のIdentifier、ファイルパス、API名、Product Nameなど、識別上の正確性が必要な表記は維持する。
- Commit Messageのためだけに正式名称、識別体系、設計文書を新たに成立させない。
- 表現しやすさを理由に、確定済みの変更主体そのものを変更しない。

表記の統一よりも、変更主体の正確な識別と理解しやすさを優先する。

### Operation Representation

Operationは変更主体に生じた状態変化を表す。

適切な語がある場合は後述のPreferred Operation Vocabularyを優先する。

ただし語彙は限定集合ではなく、意味を正確に表すために別の表現を使用してよい。

## Message Language

Commit Messageの自然言語は日本語を既定とする。

明示的に別の言語が指定された場合は、その指定を優先する。

TypeなどのSemantic Identifierは言語によって変更しない。

Product Name、技術的Identifier、ファイルパスなどは、言語の変更だけを理由として翻訳・改称しない。

## Body Responsibility

Commit Messageの情報責務は次のように分ける。

- **Header = What**：何を変更したか
- **Body = Why / Context**：そのCommit固有の理由・背景
- **Diff = How**：具体的に何を変更したか

Bodyは任意であり、HeaderとDiffから分からない保存価値のある情報が存在する場合に使用する。

ファイル一覧、変更箇所の列挙、Diffの言い換え、作業完了報告などをBodyに重複記述しない。

## Preferred Operation Vocabulary

以下は推奨語彙であり、使用可能なOperationを限定するものではない。

| Semantic Key | Japanese |
| --- | --- |
| `establish` | 策定 |
| `revise` | 改定 |
| `add` | 追加 |
| `fix` | 修正 |
| `unify` | 統一 |
| `align` | 整合 |
| `build` | 構築 |
| `apply` | 適用 |
| `update` | 更新 |
| `improve` | 改善 |
| `restructure` | 再構成 |
| `format` | 整形 |
| `remove` | 削除 |
| `revert` | 取り消し |
| `rename` | 改称 |
| `migrate` | 移行 |

適切な語が複数ある場合は、変更目的と実際の状態変化に最も近いものを選ぶ。

## Examples

```text
✨ feat: 知識登録機能を追加
🐛 fix: 検索結果の重複を修正
♻️ refactor: 知識保存処理を再構成
📝 docs: 共通開発方針を策定
```

正式な英語名称が存在する場合でも、意味と対象の同一性を維持できるなら自然な日本語表現を使用してよい。
