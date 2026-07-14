# GitHubリポジトリの設計思想とアーキテクチャ

元セッション: [ChatGPT「GitHubリポジトリの設計思想とアーキテクチャ」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a43dcc3-b488-83ee-af19-4fd01f3de220)（2026-07-01〜7/2）/ [Claude 同名セッション](https://claude.ai/chat/6df3b911-c418-4bde-8d03-1ea585cfec79)（〜2026-07-09）

Repository/Documentation PhilosophyからCommit Conventionまで、コア文書群を順に設計したセッション。

## Notes（メモ）

### docs/構成の初期提案と置き換え

セッション冒頭、ChatGPT側から最初に提示された`docs/`配下の構成案は、`policies/`（守るべき規範）・`guides/`（実際の運用手順）・`standards/`（標準仕様）・`decisions/`（ADR相当）・`reference/`（用語集等）という5分類だった。

これに対し、ユーザー側から`philosophy/ architecture/ conventions/ specifications/ adr/`という別の5分類が直接提案され（前セッション0001で示された分類がそのまま踏襲される形）、ChatGPT側もこれを高く評価した。理由：「philosophy→architecture→conventions→specifications→adr」という並びが「思想から実装へ自然につながる」流れになっており、各領域が「Why（なぜ）」「構造」「規約」「実装要件」「意思決定履歴」という明確な意味的進行を持つため。`policies/guides/standards/decisions/reference`という最初の案には、この種の一貫した意味的順序がなかった。

### フォルダ構成の確定

- `.github`という名前のリポジトリであっても、GitHubが認識するファイル（CONTRIBUTING、ISSUE_TEMPLATE、workflows等）は通常のリポジトリと同様に`.github/`サブフォルダ配下に置く必要がある。ユーザー自身の実運用経験（「実際に試したことがあります」）による確認。ChatGPTは当初「リポジトリ直下に置くべき」という逆の提案をしていたが、この実運用確認により訂正された
- `.github/actions/`（Composite Action置き場）も構成に追加
- `docs/`配下は`philosophy / architecture / conventions / specifications / adr`の5分類で確定。この分類は前セッション（0001）で提示された5分類がそのまま踏襲された
- ADRは「テンプレートを作ってからまとめて作成する」方針とし、この段階では後回し。まず設計に集中する

### 個別リポジトリと共通`.github`リポジトリの優先順位

同種のファイル（例：CONTRIBUTING.md）が個別リポジトリと共通`.github`リポジトリの両方に存在しうる場合の優先順位が、以下の6段階で整理された（0001のRule Override Policyの初期案をさらに具体化したもの）。

1. 個別リポジトリ側の`.github/CONTRIBUTING.md`
2. 個別リポジトリ側の`CONTRIBUTING.md`
3. 個別リポジトリ側の`docs/CONTRIBUTING.md`
4. 共通`.github`リポジトリ側の`.github/CONTRIBUTING.md`
5. 共通`.github`リポジトリ側の`CONTRIBUTING.md`
6. （共通`.github`リポジトリ側の`docs/CONTRIBUTING.md`、と推定される。参考にした過去チャットの引用範囲では6番目の項目が途中で切れており、正確な文言は未確認）

個別リポジトリ側に同種のファイルが存在する場合は、そちらが共通`.github`リポジトリのデフォルトファイルより常に優先される、という原則がここで確定した。

### 初期コア文書の絞り込み

Repository Profileの優先度を下げ、まず「ドキュメントの責務・設計思想・方針」を明確にすることを優先する判断があった。理由：責務が決まれば、それに沿ってリポジトリ方針・アーキテクチャ・Markdown規約というコア部分の設計に自然に進めるため。

初期コアドキュメントは philosophy・architecture・conventions（Markdown規約のみ）に限定。理由：これらを固めることで、以降のドキュメント設計を統一的な思想の上で進められる。

### ファイル命名規則

- ディレクトリ階層で責務が表現されているため、ファイル名自体に責務を含めるのは冗長と判断
- kebab-case（ハイフン区切り）を採用。理由は開発者の言語感覚：「アンダーバーは区切り、ハイフンは意味のつなぎ」という個人的な使い分け感覚に基づく

### Repository Philosophyの内容決定

- Purpose/Visionを分割：Purposeは存在意義そのもの、Visionは「なぜGitHubか」「なぜRepository単位か」に絞る
- 「Knowledge over Tacit Knowledge」はDocumentation Philosophyではなく**Repository Philosophy側に配置**。理由（ChatGPTの判断）：これはMarkdown形式の話ではなく、Git・ADRという「変更履歴・意思決定を版で残す」というリポジトリ全体の思想の話であるため
- 「構造で責務を語る」はCore Philosophyから削除。ディレクトリ階層による責務表現という設計手法の話はArchitecture側の責務であり、Philosophy（Why）の対象ではないと整理された。この判断は後にDocumentation Architectureの「構造は責務を表現する」という原則として結実している
- 「Commonality with Explicit Exception（共通化と例外の明示）」を独立した柱として新規追加
- SSOTの表現を「責務を持つ唯一の場所で管理する」という抽象度に書き換え、固有名詞を排除

### Documentation Philosophyの内容決定

- 「責務の分離」という見出しに変更し、repository.mdから削除した「構造で責務を語る」とは別物として独立させた
- 「ディレクトリ階層で表現する」という設計手法の部分はArchitecture側へ切り離す方針を確認

### Repository Architectureの内容決定

- 「トップレベル要素の増減判断基準」を追加。目的：`scripts/`や`tools/`等の新要素が将来必要になった際、まず既存要素への統合を検討する、という判断軸を持たせるため。「責務による構造化」の原則の延長として位置づけられた

### Documentation Architectureの内容決定

- 「責務は交差させない」をDesign Principlesの筆頭に配置。理由：「構造は責務を表現する（静的・設計時の原則）」と「責務は交差させない（動的・運用時の原則）」が対になるようにするため。設計時に責務を定義し、運用時にその境界を守るという二段構えで一貫性を保つ

### Markdown Convention設計の順序判断

設計文書のスタイル統一を進める前に、まずMarkdown規約自体を確定させ、既存ドキュメントの表記を統一する、という順序が決められた（表記統一の基盤を先に固めてから応用する、という進め方）。

以前ChatGPTと作成した参考資料（`MARKDOWN_CODING_CONVENTION.md`）をベースに再編する方針。

### Rule記述フォーマットの変遷

1. 当初、参考資料はRule/Requirement/Sourceが表、Reasonがリスト、Exampleがコードブロックという構成だった
2. 一度全項目を表形式に統一したが、「AIの解析性は上がるが、人間には長文が見づらく例の表現も制限される」という指摘があった
3. **ハイブリッド構成を採用**：構造データ部分（Rule/Requirement/Source＝Header）は表、内容部分（Reason/Examples/Notes＝Body）は自由記述、という二層構造に決定。「人にとってもAIにとっても読みやすい最適解」という判断
4. Ruleの項目は「ルール自体の核でありAIにとってのメタデータに近いもの」として、表の先頭に短い説明として置く方針
5. Bodyの見出し表現で`#### Reason`のような見出しを使うと、MD-DS-006（Unique Headings、markdownlint MD024）に抵触する（同一レベル・同一タイトルの見出しが複数出現するため）ことが判明。**見出しではなくkey:value形式**（`**Reason:**`のような強調装飾付きラベル）で表現する方式に変更した

markdownlintに起因するルール（エラー番号が明確にあるもの）は積極的に採用する方針。既存ルールへのSource追記（MD-DS-002←MD001、MD-DS-003←MD025、MD-DS-005←MD022、MD-CR-002←MD040）、新規ルール追加（MD-DS-006 Unique Headings/MD024、MD-DS-007 No Emphasis as Heading/MD036、MD-PS-002/MD009）が行われた。運用フロー：「markdownlintエラーが発生→修正するか検討→修正する場合は独自ルールとして規約に追加」という流れも確認された。

### Writing ConventionとMarkdown Conventionの境界

Document Labels（`**Reason:**`等の表記スタイル）は「マークダウンでの表現＝スタイルの話」であり、Markdown Conventionの責務。Writing Conventionは「言語に限らず集約的な内容」ではなく、文章表現・文体・用語利用を扱う、という線引きが明確化された。

### 英日併記方針の精緻化

個人アカウントのリポジトリは基本的に日本語がベース。ただしH1/H2は「英語タイトル（日本語説明）」の英日併記フォーマットで統一する。本文中の英語には「英語（日本語）」の補助訳を付けることがあるが、全部に付ける必要はなく、統一基準は設けない（主観判断の余地を残す）という方針。

### Glossaryの分離

用語集（Glossary）は独立した関心事として分離する方針が決定された。

### README（Conventions README）設計

Convention Responsibilitiesセクションに「責務→実装:ファイル名」という構造を導入。目的：将来ファイル名が変わっても、責務の定義自体は本書側で安定して維持できるようにするため。「個別ConventionはREADMEを再定義しない」という原則も追加され、SSOTがConventions層の運用にも明示的に適用されるようになった。

### Rule Componentのformat再修正

Header（Rule→Requirement→Source）とBody（Reason→Examples→Notes→Exceptions）を明確に分離し、順序を固定。旧READMEにあった「References」項目は、新しいBody定義に含まれていないため削除された。

### Commit Convention設計

- タイトル形式：`{gitmoji} {type}({scope}): {subject}`を採用（過去の実運用規約を参考資料として使用）
- 言語：対象読者視点で選択する方針。今回の個人アカウント用`.github`リポジトリでは日本語
- 命令形ルールは英語表記時の名残と整理され、日本語では別の表現にする
- Scopeについては、公開ソフトウェアではなく個人用ドキュメント管理という性質上、厳格な表記を求めない方針
- コミットメッセージの言語は**リポジトリの目的・対象読者によって変わる**という運用上の整理があった：個人利用は日本語、一般公開の製品でも基本は日本語、グローバル向け製品（例：WordPressプラグイン）は英語、組織アカウントのOSSプロジェクトは開発ドキュメントは日本語でも公開時に英語化されるが、コミットメッセージは後から翻訳できないため最初から英語にする、という考え方。最終的にはRepository Overrideで明示する抽象的なルールに落とし込まれた
- Typeの使用範囲：ドキュメント管理用途では、Conventional Commitsの全Typeを使うわけではなく、そのリポジトリで実際に使うTypeだけを採用する

### Footer固有ルールとBREAKING CHANGEの扱い

Footer固有ルールとして次が提案された：Issue参照は`Refs`を使う／Issueのクローズは（コミットではなく）PRで行う／`BREAKING CHANGE:`はFooterの最後に配置する（複数行説明時にFooterの終端を明確にするため）。

**全角コロン案の提示と撤回の経緯**：当初、`BREAKING CHANGE:`の説明本文中で項目ラベル（「移行方法：」等）を書く際、半角コロンだとツールにkey:valueと誤認識される懸念から、全角コロン「：」を使うという案が出た。しかしこの案は英語表記に対応できない（英語には全角/半角の区別がない）ことが分かり、re-thinkが行われた。

根本原因を掘り下げた結果、「全角コロンを使う」は対策の一つに過ぎず、本当のルールは「Footerパーサーと競合するkey:value構造を説明本文中に新たに作らない」ことだと整理された。解決策として、書き方を限定するのではなく、禁止事項（制約）だけを定義する方針に転換：具体的な表現（見出し・箇条書き等）は自由に選べるが、新たな`key:value`的構造を作ってはならない、というルールになった。

**この経緯から見えたパターン**：これまでのMarkdown Convention（「HTMLを書け」ではなく「HTMLに依存するな」）、Writing Convention（「である調を使え」ではなく「文体を統一しろ」）、Naming Convention（「repository.mdにしろ」ではなく「責務を表す名前にしろ」）と同じ、**「書き方を指定するのではなく、必要な制約だけを定義し、表現の自由度は書き手に残す」**という設計パターンがConvention全体に共通していることが、この議論を通じて言語化された。ChatGPTはこれを新しいDesign Principle「Constraint over Prescription」として追加することを提案したが、最終的には「既存のConsistency over PreferenceやTool Compatibilityに包含される」と判断され、独立原則としてではなく各Conventionの個別ルール設計方針として採用する形に落ち着いた。

### Gitmoji-Type対応

Gitmoji・Type11項目の対応表（リリースノート掲載可否付き）を追加。GitmojiとTypeの1対1対応を強制するルールを新規追加（対応表外の組み合わせを禁止）。Gitmojiの使用は当初MAY（任意）だったが、「標準で必須とすることでリポジトリをまたいだ視覚的一貫性を保証する」という理由でMUSTに変更された。ただし個別リポジトリ側でのRepository Overrideによる緩和は可能な設計。

## Open Questions（未解決事項）

- GitHub Naming（GitHub上で使う識別名の命名規則）は「後で検討が必要」として保留された
- BREAKING CHANGE本文では新たなkey:value構造（項目ラベル）を作らない方針は確定したが、英語表記時に推奨する具体的な記号・表現（見出し／箇条書き／Bodyへ逃がす、のいずれを標準とするか）は、このセッション終盤時点でまだ未確定だった

## ADR候補（暫定）

後続セッションでの維持・統合状況を確認してから記録要否を判断する。

- `.github`リポジトリ自身も`.github/`サブフォルダ配下にGitHub認識ファイルを置く必要があるという構成上の制約とその根拠（プラットフォーム制約への準拠であり、代替案を選んだ設計判断ではないため、独立ADRよりRepository構造ADRの背景情報として統合される可能性が高い）
- 初期コアドキュメントをphilosophy/architecture/markdown Conventionに絞り込んだ判断（作業順序・初期スコープの判断に近く、将来の説明価値が低ければADR対象外）
- ファイル名にkebab-caseを採用し、責務をファイル名に含めない判断（理由が主に個人的な言語感覚であり、Naming Convention本文の記述で足りるならADR不要の可能性）
- 「構造は責務を表現する」の配置（Philosophy側ではなくArchitecture側）
- Rule記述のHeader（表）/Body（自由記述＋key:value）というハイブリッド形式の採用（全表形式・全自由記述との明確な代替案比較があり、独立して覆せる判断でもあるためADR向き）
- Document LabelsとWriting Conventionの責務境界
- Commit Footerにおいて、特定の表記（全角コロン等）を強制せず、パーサー競合を避ける制約だけを定義した判断（全角コロン案の撤回経緯を含む。抽象原則そのものではなく、この具体的な決定単位で候補とする）
- Gitmojiの必須化（MAY→MUST）（Gitmoji-Type 1対1対応とは別々に覆せる可能性があるため、ADR化する場合は分割候補として扱う）
- Gitmoji-Type 1対1対応の強制（同上、Gitmoji必須化とは独立に検討する）
