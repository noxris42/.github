# プロジェクト開始の情報整理

元セッション: [ChatGPT「プロジェクト開始の情報整理」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a43d183-4f2c-83ee-990c-560adec74ec8)（2026-06-30〜7/11）/ [Claude 同名セッション](https://claude.ai/chat/fd11e26e-5dd8-4701-b2e5-2aea5d4029ca)（2026-06-30）

同一の指示書を両モデルへ提示し、並行してレビューを受けたセッション。

## Notes（メモ）

### プロジェクトの目的・対象範囲

- 個人アカウント用`.github`リポジトリの設計・実装が目的。複数リポジトリで共通利用できる運用標準（ドキュメント・規約・テンプレート・GitHub設定・開発フロー）を一元管理する
- 特定アプリケーション開発は対象外。組織アカウント用`.github`は明確に対象外とし、個人アカウント用とは別プロジェクト・別設計として扱う（責務・前提・読者が異なるため）
- 対象に含めるもの：README・共通CONTRIBUTING・ドキュメント体系・Markdown規約・コミット規約・ブランチ戦略・Issue/PRテンプレート・GitHub Labels・GitHub Projects運用・GitHub Actions・Reusable Workflows・Composite Actions・Repository Templates・用途別テンプレート・開発フロー・レビュー方針

### 設計思想として提示された事項

Long-Term Assets／Responsibility Separation／Single Source of Truth／Consistency over Preference／Concept First, Implementation Second／Simplicity over Complexity／Evolve Through Operation。この7つが最初期から一貫して提示されている。

### ドキュメント5分類として提示された事項

Philosophy(Why)／Architecture(What)／Specification(How)／Convention(Rule)／ADR(Decision)という5分類が、プロジェクト開始時点ですでに提示されている。

### 英日併記方針

- H1・H2は英語＋日本語併記を必須、H3以下は理解に必要な場合のみ
- 表のヘッダーは日本語ベースを優先
- ファイル名・Rule ID・Profile名・GitHub機能名などの識別子は英語のまま

### Rule Override Policy（共通ルールとリポジトリ固有ルールの優先関係）

初期案の優先順位：①各リポジトリ固有の明示的なルール ②`.github`の共通ルール ③一般的なGitHub運用慣習。

ChatGPTからの指摘：固有ルールが無秩序に共通ルールを上書きできる余地を残すべきではない。「固有ルールは例外であり、共通ルールとの差分と理由を明示する」「共通ルールを参照せず独自ルールだけを置くことは避ける」という歯止めが必要、との指摘があった。この時点ではテンプレート変数・自動マージなどの技術的な上書き機構は導入しない方針（ドキュメント運用のみで対応）。

### Repository Profile

初期候補：documentation / development / product / library。

ChatGPTから重要な指摘：この4つは分類軸が異なる（documentationは成果物、developmentは活動一般、productは事業性、libraryは提供形態）。1リポジトリが複数Profileにまたがるケース（Webアプリ＝development/product、OSSライブラリ＝development/library等）で迷う。

ChatGPTの代替案：

- 案A（成果物で分類）：documentation / application / library / service / infrastructure
- 案B（運用特性で分類）：lightweight / standard-development / release-managed / public-oss / private-internal

ChatGPTは案A寄りを推奨（テンプレートに必要なREADME・ライセンス・リリース・CI・公開方針が「成果物の種類」によって変わるため）。この時点では未確定、初期設計で正式定義する前提。

### GitHub上の設定とリポジトリ内ファイルの区別（Configuration Boundaries）

ChatGPTの提案を受けて指示書に追記された3分類：

| 区分 | 内容 | 管理の考え方 |
| --- | --- | --- |
| Default Files | CONTRIBUTING、Issue Template、PR Template | `.github`リポジトリで既定値として提供 |
| Shared Assets | 規約、Reusable Workflow、Composite Action、テンプレート | 参照・コピー・呼び出しで再利用 |
| Managed Configuration | Labels、Projects、Rulesets、Repository settings | 手順書・定義ファイル・CLI・API等で再現性を確保 |

理由：Labels・Projects・Rulesets等はMarkdown/YAMLを置くだけでは完結しない、GitHub上の設定同期が必要という性質の違いがあるため。

「一元管理」と「全リポジトリへの自動反映」は別概念、という指摘もあった（Central Definition／Distribution／Reference／Synchronization／Overrideの用語分離）。

### Standard and Override Policy

共通標準は個人アカウント配下リポジトリへの既定値。個別リポジトリは明示的に例外を定義できるが、例外は「共通標準の無効化」ではなく「固有事情の明確化」のためにのみ設ける、差分と理由を記録する、という方針が追記された。

### Self-Application Policy

`.github`リポジトリ自身も標準の適用対象とする。ただし共通標準を提供する立場としての固有要件があれば例外を明示的に記録する。自己検証用Workflowと、他リポジトリから呼ばれるReusable Workflow/Composite Actionは目的が異なるため区別して管理する、という方針。

### ADR Policy

初期マイルストーンから重要な設計判断はADR候補として扱うが、すべての小さな判断はADR化しない。ADR化すべき例として挙げられたもの：ディレクトリ構成の決定／ドキュメント分類の決定／Repository Profileの採用・変更／共通ルールと固有ルールの優先関係／Reusable WorkflowとComposite Actionの使い分け／複雑な仕組みを採用しない判断（不採用判断も記録する）。

### Entry/Exit Criteria Policy

Issueテンプレート・PRテンプレート・レビュー基準に展開する前提概念として導入。初期マイルストーンでは詳細実装せず、概念認識に留める。

ChatGPTからの指摘：将来的にはすべての作業に同じ厳格さのEntry/Exit Criteriaを課すのではなく、変更種別（Lightweight Change／Standard Change／Policy Change／Automation Change／Security-sensitive Change）ごとに必要な確認項目を変えるべき、という提案があった。

### Raw Chat Archiveについての言及

このセッションの最後に「チャットを保存して」という指示があり、ChatGPT側で「要約せず発言順そのままのRaw Chat Archive」としてMarkdown化する運用が行われた。Front Matter・発言者形式・全文保存・要約禁止、という仕様がこの時点で運用されている。これはSymnousプロジェクト側の資産であり、本リポジトリ（`.github`）の設計対象ではない。

この指示書自体は正式ドキュメントとして管理せず、「設計を開始するための前提整理」と位置づけられた。ただし「成果物ではない」ことと「原文を完全に破棄してよい」ことは別、という整理がされ、原本は会話ログとして残す方針だった。

## Open Questions（未解決事項）

このセッション終了時点で「設計に進む準備が整った」と結論づけられているが、以下は指示書レベルでは未確定のまま設計フェーズへ持ち越された。

- Repository Profileの正式な分類軸・境界（案Aと案Bのどちらに寄せるか、複数Profileにまたがるリポジトリの扱い）
- 共通ルールと固有ルールの優先順位の技術的な実装方法（この時点では「ドキュメント運用のみ」）
- `.github`リポジトリ自身のWorkflow構成（Internal Workflow と Shared Reusable Workflowの命名・配置の区別）
- AI運用ルールの境界（AIが設計提案のみか実装まで行うか、承認が必要な領域の線引き）－この段階では「後続の開発フロー・レビュー方針で定義する」とされ先送り

## ADR候補（暫定）

このノート単体から見えるADR候補は、まだ暫定として扱う。後続セッションを通読し、その判断が維持されたか・別概念へ統合されたか・現行Documentationへ実際に反映されたかを確認してから記録要否を判断する。

現時点で候補になり得るもの：

- Rule Override Policy（共通ルールと固有ルールの優先関係、例外は差分と理由を明示する原則）
- Configuration Boundaries（Default Files / Shared Assets / Managed Configurationの3分類とその理由）
- 個人アカウント用と組織アカウント用`.github`を別プロジェクト・別設計にする判断
- `.github`リポジトリ自身も共通標準の適用対象にする（Self-Application Policy）
- Documentationを責務別に分類する（5分類の採用）
- 「一元管理」と「自動反映」を別概念として扱う整理
- Entry/Exit Criteriaを変更種別に応じて変える方針

ADR Policy（このセッションで示された「初期マイルストーンからADR候補として扱う」「不採用判断も記録する」という方針）自体は、独立したADR候補としては扱わない。これは現在進行中のADR/design-notes運用再設計の背景・比較対象としての価値が高く、後のDecision Miningでは現行ADR運用を決定したADRのContext・Rationaleへ統合される可能性が高い。
