# GitHub運用規定設計（前半）：Layer Dependency違反の修正とADR初回作成

元セッション: [ChatGPT「GitHub運用規定設計」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a4c5e39-b418-83ee-a427-539576852e26)（2026-07-07〜7/13、前半部分）

前セッション（0003）からの引き継ぎメモで開始。Branch Conventionの作成、Layer Dependency違反の発見と全体修正、ADRテンプレートの初回設計、旧12件ADR（Legacy ADR）取り込み案の検討と却下、ADR-0001〜0006の実際の作成までを扱う。

## Notes（メモ）

### セッション開始時点の完了済み設計

引き継ぎメモによれば、この時点でRepository Philosophy・Template Philosophy・Repository Setup Specification・GitHub Project Setup Specification・GitHub Workflow Specificationが完了済み。設計方針は一貫して「Design When Needed」。

### Branch Convention設計

`docs/conventions/branch.md`を新規作成。BR-TY-001はCommit ConventionのCM-TG-002（Type定義）を参照する形にし、Type定義の重複管理を避けSSOTを徹底。BR-CR-001はSHOULDとし、main-only運用の例外を排除しない設計。conventions-readme.mdにもBR識別子とBranch Conventionの責務定義を追記。

### Layer Dependency違反の発見と全体修正（重要な構造修正）

Branch Conventionの記述に「`docs/specifications/github-workflow.md`で定義したブランチ運用を具体化する下位文書である」という一文があり、これが違和感の発端となった。

**問題の構造**：Convention→Specificationの関係で見ると、Conventionが上位・Specificationが下位（Specificationが実装可能な仕様としてConventionを具体化する）という設計思想があるにもかかわらず、Branch Convention側の記述はGitHub Workflow Specificationを「上位」であるかのように参照していた。実装順序としてはgithub-workflow.mdを先に作りbranch.mdを後に作ったという事実はあるが、ドキュメント構造上の依存方向とは無関係、という整理がされた。

原則として「上位設計のことは知っているが、下位設計は知らない」（Convention文書はSpecificationを参照しない）という方針が確認され、全ドキュメントで同様の依存方向の逆転がないか横断的に確認された。

**修正内容**：
- `branch.md`のScope・Relationships・BR-LC-001のSourceからgithub-workflow.mdへの参照・具体的ファイルパスを削除し、概念名のみの記述、または参照自体を削除
- SSOT観点での重複（「Branchは1つのIssueに対応させる」等の記述がbranch.mdとgithub-workflow.mdの両方にあった）を解消し、github-workflow.md側はbranch.mdへの参照に統一
- 修正後、Specification（github-workflow.md）がConvention（branch.md・commit.md）を参照・利用する方向が正しく保たれていることを確認

この整理の結果、「レイヤー依存原則」を上位設計文書へ正式化する作業も行われ、Convention文書内の逆方向参照（commit.md・branch.mdにあった「将来のSpecifications」「templates/pull-request-template」等への言及）も削除された。

**根本原因の特定**：この問題は「参照（reference）」と「依存（dependency）」の混同から生じていたと整理された。Branch ConventionがGitHub Workflow Specificationに言及すること自体は作成順としては自然だが、それによって「Workflowが親、Branch Conventionが子」という所有関係が暗黙に表現されてしまっていた。あるべき構造は、Workflowが「オーケストレーター」としてCommit Convention・Branch Conventionを利用し、Issue→Branch→Commit→PR→Mergeという流れを組み立てる、というものであり、Workflow自身がBranchの仕様を定義するわけではない。

**「Layer Dependency Principle（レイヤー依存原則）」という名称がこの議論の中で明示的に命名された**：「上位レイヤーは下位レイヤーを知らない。下位レイヤーは上位レイヤーを参照・利用する」という内容で、「レイヤーの依存方向は、作成順ではなく、アーキテクチャ上の依存関係で決める」という一文でまとめられた。この原則は、当時作成予定だったGitHub Project Operation・Label Convention・Milestone Convention・Release Conventionなど将来のConvention文書にも同じ誤りを防ぐため、Design Principlesとして明文化する価値があるとされた。

**SSOT重複の具体的な判断基準**：修正の過程で、github-workflow.md内に3箇所、branch.mdのルールを再述している記述（「Branchは1つのIssueに対応させる」「Merge後、BranchはGitHub上で削除する」「BranchはIssueと1対1で対応しているか」というReview Checklist項目）が見つかった。このうち最初の2つ（ルールの「定義」を再述しているもの）はbranch.mdへの参照表現に置き換えられたが、Review Checklist項目（ルールの「確認」に過ぎないもの）はWorkflow実行時の確認項目として自然という理由で現状維持とされた。この判断は「定義の重複は解消するが、運用上の確認項目としての言及は許容する」という基準として今後も参照できる。

### ADRテンプレートの初回設計

過去に参考資料としてZIPに含めていたADRテンプレート（旧個人アカウント`.github`リポジトリのもの）を参考に、今回の設計に沿ったADRテンプレートを新規作成。

論点として、①ファイル名に`ADR-`プレフィックスが必要か（既存の命名規則から不要と判断）、②連番を4桁採番にするか（Claude推奨として採用）が確認された。

「ADRを書くタイミング」は作る/作らないの判断基準として明示され、「他文書との関係」はLayer Dependency Directionに従い、ADRが参照する側・参照される側ではない（他文書がADRへ依存しない）関係を図で明示。「関連文書」はADRが依存する上位Conventionのみを明示し、下位層（templates/adr/等）へは参照しない設計とされた。

ADR READMEの参照表現は「参照しない」から「現行仕様・運用ルールの根拠として依存しない」に変更。理由：一覧ページや設計レビューからの参照リンクは許容しつつ、仕様文書がADRへ依存してルールを成立させることを禁止する、という意図をより正確に表現するため。

### Legacy ADR（旧12件ADR）取り込み案の検討と明示的な却下（重要）

旧個人アカウント`.github`リポジトリに残されていた12件のADR（今回のリポジトリ設計には直接関係しないが、前提となる検討結果）について、「間接的に今回の設計判断として継承して取り込みたい」という提案が最初にあった。

検討の結果、いったん「Legacyフォルダを採用する」案（`docs/adr/legacy/github-personal/`）が決まりかけ、実際に分類・整理作業まで進んだ。

しかし作業途中で立ち止まり、再検討が行われた：「レガシー→今回」という時系列を管理の標準体系にしてしまうと、あらゆる新設計がレガシーとの関係性を管理しなければならなくなる（例：今回の`.github`リポジトリを将来組織用に拡張した際、今回のリポジトリ自体がレガシーになる懸念）。

**最終的な結論**：今回の`.github`リポジトリではレガシーADRという考え方を一切採用しない方針に転換。理由：時系列的には旧リポジトリ→新リポジトリだが、旧リポジトリを改造したわけではなく、考えを全部リセットしてゼロベースで設計した。旧リポジトリの知識があったから思いつけた場面はあったとしても、それは通常の思考が過去の経験から影響を受けるのと同じことであり、ADRとしての正式な派生関係は持たせない。

この却下を受けて、ADRテンプレート自体も「レガシーADRからの派生を前提にしない、ゼロベースのADR」という方針で再設計された。

**ADR Mining構想の提案と事実上の放棄**：Legacy案の検討過程で、一度「ADR Mining」という中間工程（`docs/adr/mining/`）が提案された。これはLegacy ADR・現行Documentation・設計チャットという3つの知識源から新しいADRを作るための「採掘」を行う中間成果物という位置づけで、`docs/adr/legacy/`（過去の判断履歴の原本）・`docs/adr/mining/`（抽出・整理の中間成果物）・ADR本体（最終的な設計判断記録）という3層構造が提案されていた。しかしこの直後の再検討でLegacy ADR自体が却下されたため、Mining構想も事実上あわせて放棄された。

**却下の決定打（局所最適 vs 全体最適の論法）**：`docs/adr/legacy/`を持つこと自体は今回のGitHub運用規定単体で見れば綺麗に見えるが、一歩引いて見ると「GitHub運用規定だけが特別扱いされている」ことに気づかれた。将来他のプロジェクト（Nexnos v1→v2、Symnous v1→v2、Blog、Business等）がそれぞれ`legacy/`を持つことになれば、これは「知識管理」ではなく単なる「履歴管理」の乱立になる。過去との関係性・知識の系譜（Knowledge Lineage）を追う機能は、個々のプロジェクトリポジトリではなくSymnous（あらゆる知識を横断的に保持する構想中の別システム）の責務であるべき、という整理がなされた。

**最終的な責務分担**：`.github`リポジトリが持つのは「Current ADR」（現行の設計判断）だけとし、Legacy・Knowledge Lineage・Decision Evolution・Chat・Design Notes・Review・ADR HistoryはすべてSymnous側の責務とする。旧12件のADRは「捨てるわけではない」が、`.github`リポジトリには置かず、ADR作成時の参考資料として利用するに留める（旧ADR→今回のADR作成→Symnousへ保管、という流れ）。

### ADRテンプレートの再設計における往復（重要）

Legacy却下を受けたテンプレート再設計では、当初**Decision Evolution・Design Insights・Related Documentsを削る（あるいは現行設計判断に閉じる形へ再定義する）方針**が提案された。理由：ADRを「過去知識との系譜管理」から切り離し、`.github`リポジトリ内の現行設計判断だけを記録する「Knowledge-oriented ADRからCurrent Design Decision ADRへ戻す」という考え方。

しかしこの直後、ChatGPTによる実際のテンプレートレビュー（0004前段に記載）で、Decision Evolution・Design Insightsの**欠落**が指摘され、「設計途中で得られた知見や検討過程も資産として保存する」という設計思想（Knowledge Record）の核心にあたるとして、**両セクションとも復活・追加が必須とされた**。

つまりDecision Evolution・Design Insightsは「一度削除が提案された後、レビューで押し戻されて復活する」という往復を経ている。この揺れは、「ADRを現行判断だけに絞りたい（Symnousとの責務分離を徹底したい）」という力と、「ADRに知見・検討過程も残したい（情報を失いたくない）」という力の綱引きを表しており、後のセッション（0005で扱う、ADR運用の議題主軸→決定主軸への成熟）でも同じ緊張関係が繰り返し現れる。

### ADR-0001〜0006の実際の作成

新テンプレートを使い、実際にADRの作成が開始された。

ADR Philosophy文書（`docs/philosophy/adr.md`）が新規作成され、「番号は論理構造順で採番する」という設計思想がこの時点でドキュメント化された（理由：検討事項をその都度追加するのではなく、区切りがついた段階でADRにまとめるというフローを表すため）。この過程で、Naming Convention側（NM-ID-004）が「作成順」「順序のみで管理する」まで規定していた責務が見直され、Naming Conventionは「4桁連番という命名方法のみ」を定義し、番号の意味（論理構造順）はADR Philosophyの責務とする、という責務の再配置が行われた。

ChatGPTによるADRテンプレートのレビューで、次の指摘があった：
- Decision Evolutionセクションの欠落：「設計途中で得られた知見や検討過程も資産として保存する」という設計思想（Knowledge Record）が表現できていない、として追加が必須とされた
- Design Insightsセクションも同様の理由で必要とされた

**ADR作成ワークフローの確立**：初版はChatGPT（過去チャット全歴にアクセスできる立場から）が作成し、体裁修正はClaude、ドキュメント内容修正は指示書をもとにClaudeが行う、という分業が明示的に確認された。

ADR-0001（ADR運用プロセスの採用）を皮切りに、Contextを「完成した設計の説明」ではなく「判断が必要になった状況」に焦点を当てる修正、Decision Evolutionに指示書の変遷（逐次ADR案→Legacy ADR管理も検討→Symnousとの責務分離を再整理→ADR運用そのものを先に設計→Documentation完成後にADR化する方針へ確定、という紆余曲折）をそのまま反映する形で作成された。

文中でSymnous（構想段階の別プロジェクト）という固有名詞が使われていたことが問題視され、構想段階の固有名詞は避けるべきという判断のもと、「知識管理基盤」という抽象的な表現に置き換えられた（プロジェクトを横断する再利用可能なADRを維持するため）。

ADR-0002〜0006も同様に、指示書（箇条書きメモ）をADRとして完成した文章（地の文）に書き起こす形で順次作成された。Rationaleでは指示書の複数の観点をそれぞれ独立した段落として、なぜそれが成立するのかまで含めて説明する形が採られた。

Rule記述内での強調記法（`**Text**`）をリスト項目のラベルとして使う用法について、MD-DS-007（見出し代わりの強調記法禁止）への抵触が懸念されたが、文書の見出し（`#`）を代替するものではなく箇条書き内のラベルとして使われているため許容範囲と判断された。

## Open Questions（未解決事項）

- ADR候補として最初に挙がっていた「十数個」の候補がすべて網羅されているかが問い直された（[286]）が、この時点で明確な棚卸し結果は確認できていない
- ADRの性質（議論履歴のログなのか、設計検討の履歴なのか）について根本的な疑問が[288]で提起され、「ADRは議論履歴＝ログ＝無選別で保存ではない」という結論には至ったが、この後さらに大きな設計の再検討（0005で扱う）に発展した

## ADR候補（暫定）

- Convention文書はSpecification文書を参照しない、という依存方向の原則（Layer Dependency Direction）の確立とその適用によるbranch.md/github-workflow.mdの修正（「作成順」と「依存方向」は無関係、という誤認の発見と修正の経緯が、現在のLayer Dependency Directionの成立理由そのものであるためADR候補として強い）
- ADRファイル名に`ADR-`プレフィックスを付けない、4桁連番を採用するという命名判断
- 旧個人アカウント`.github`リポジトリの12件のADRを「Legacy ADR」として取り込まない、ゼロベースでADRを構築するという判断（`docs/adr/legacy/github-personal/`への取り込み・分類作業まで一度進んだ後に却下された経緯を含む。現在のプロジェクトでも同じ方針が踏襲されており、ADR運用そのものの前提として記録価値が高い。独立ADRとするか、現行ADR運用全体のADRへ統合するかは後続の判断とする）
- ADR番号を「論理構造順」で採番するという判断（現在は撤回され、実際の確定・作成順の単純連番に変更されている。現行テンプレートにはDecision Evolution節がないため、独立ADRにはせず、番号ルールを定めるADRのContextまたはAlternatives Consideredへ、「旧判断：論理構造順」「現在：作成順」という形で統合するのが自然）
