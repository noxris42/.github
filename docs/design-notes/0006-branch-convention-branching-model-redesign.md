# Branch Convention再設計とBranching Model確立

元セッション：

- [ChatGPT「GitHubリポジトリ参照」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a5785bc-5628-83ee-8cd7-1e7763d84346)（2026-07-15〜7/16、後半のBranch運用議論部分）
- [ChatGPT「Symnousリポジトリ構築方針」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a58ea19-fa58-83e9-b32b-94240795e3e6)（2026-07-16〜7/24）
- Claudeとの実装セッション（同期間、上記ChatGPTセッションからの指示を実装・レビュー往復）

Symnousリポジトリのブランチ運用を検討する中でConvention Extension Architectureが生まれ、それが「Branch Patternの粒度誤り」の発見を経てBranching Model概念へ発展し、Base Branch Conventionの再設計、Issue・GitHub Project・Work Branchの責務分離、Main Branch Flowの実装、`.github`への適用、Symnous専用Modelの検討と却下、LTS Release Branch Flowの保留までを扱った、一連の連続した設計テーマを持つセッション群。

Convention Extension Architecture自体の概念設計（Base/Pattern/Repositoryの3層、Rule ID Override方式）は既存design-notes（0001〜0005）に記録がなかったため、本ノートで最初から扱う。

---

## Notes（メモ）

### 発端：Symnousのブランチ運用をどう固有化するか

Symnousリポジトリの構築を進める中で、ブランチ運用が最初の論点になった。共通規約（当時のBranch Convention）は「1 Issue = 1 Branch + Pull Request、mainへの直接Pushは禁止」を前提としていたが、Symnousはチャット履歴やAI生成知識を日常的に追加するモノレポであり、すべての追加にIssue・Branch・PRを要求すると運用負荷が過剰になることが分かった。

最初の案は「main-only」だったが、それでは新機能開発やスクリプト変更などリスクの高い変更まで無防備になる。検討の末、「原則ブランチ＋PR、日常的な低リスク追加のみmain直接Pushを例外的に許可する」で確定し、Symnous固有のRepository Override文書として書く方針になった。

### Repository Overrideの表現方法を巡る検討（Convention Extension Architectureの起点）

Repository Overrideをどう書くかで、次の3案を比較した。

- 自然言語で差分だけを説明する：共通規約のどの規則が置き換わったのか曖昧になり、人もAIも2文書を読み比べて解釈する必要がある
- 共通規約を丸ごとコピーして固有部分を書き換える：共通規約の改訂が自動反映されず、コピー後にどこが固有変更か分かりにくくなり、正本一元化が崩れる
- Rule ID単位で明示的にOverrideする：共通規約にRule IDを振り、Symnous側ではそのRule IDを対象にReplace／Extend／Disableし、対象外のRule IDは共通規約をそのまま継承する

3番目のRule ID単位方式を採用した。この時点ではSymnousで暫定的に実践し、後で`.github`側の共通仕様として正式化する進め方も検討されたが、「これはBranch Conventionだけの局所ルールではなく、規約継承・拡張・上書きの共通モデルである」という指摘により、先に上位設計を確定する方針へ転換した。

この転換の判断基準は、影響範囲の広さだった。Rule ID単位のOverride方式はCommit Convention、Naming Convention、GitHub Project Conventionなど他の規約にも将来使える汎用概念であり、Branch Convention内だけで定義すると各規約が独自の上書き方式を持ち始め、Extendの意味が規約ごとに揺れる、Rule IDの付け方が統一されない、AIが共通方式で解釈できない、といった問題が起こると判断した。

### Convention Extension Architectureの確立

上位設計をArchitectureとSpecificationの2段階に分けて進めることにした。

- Architecture：規約拡張モデルの概念（レイヤー構成、適用順序、優先関係、各レイヤーの責務、正本性）
- Specification：具体的な記法（Replace／Extend／Disable／Addの定義、Rule ID形式、ファイル配置、検証条件）

対象範囲は、当初「規約以外の文書にも一般化するか」が論点になったが、現時点で具体的な適用対象がBranch Conventionだけであることを理由に、Convention Extension Architectureとして規約（Convention）に限定した。一般化は実例が増えてから検討する（Design When Needed）。

レイヤー構成は次の順で決まった。

1. 「共通規約・共通規約のパターン化・リポジトリ固有規約」の3段階が確認された
2. 呼称を統一的に「○○ Convention」にする方針が示され、Base Convention／Pattern Convention／Repository Convention／Effective Conventionという最終呼称に落ち着いた
3. Pattern Conventionは、パターン分岐が必要なConventionにだけ任意で設ける（すべてのConventionに強制しない）
4. Pattern Conventionは、対象リポジトリごとに正確に1つだけ選択する（複数同時適用は認めない。追加調整が必要ならRepository Conventionで行う）
5. Repository Conventionも任意とし、固有差異がなければ省略できる

Rule IDにはScope要素を導入し、`<Convention>-<Scope>-<Category>-<Number>`という4要素形式にした。共通Ruleは`BS`、Pattern固有Ruleはそのpattern固有コード、Repository固有の新規Ruleは`RP`とする。この設計により、Rule IDを見ただけでそのRuleがどのレイヤーで最初に定義されたかを判別できるようにした。

この時点で、Convention Extension ArchitectureはADR化する価値があると認識されていた（複数の代替案（全文コピー・差分記述・Rule ID単位拡張）を比較検討したこと、将来変更すると多くの規約・リポジトリに影響することが理由）。

### Branch Patternの試作と粒度の誤り

Convention Extension Architectureの最初の適用対象としてBranch Conventionを選び、Pattern Conventionとして3つの「Branch Pattern」を設計しようとした。

初期の3案は次のとおりだった。

- main-primary（仮称main-only）：mainを標準の作業場所とし、直接Commit／Pushを通常経路として許可。Branch／PRの使用は禁止せず任意
- dual-track：定型的な運用更新はmain直接、設計・開発上の変更はBranch＋PRという2経路併用。Symnous向け
- protected-main：mainへの直接Commit／Pushを禁止し、Issue→Branch→PR→Mergeのみを変更経路とする。Nexnos（本格的なソフトウェア開発）向け

ここでパターン名の検討中に「Flow」という語を避ける方針が一度示された。理由は、Git Flow・GitHub Flow・独自のLTS Release Branch Flowと名称が混ざるためだった。この過程で「Git Flow、GitHub Flow、LTS Release Branch FlowはBranch Patternと同じ粒度の概念か、それとも詳細化した概念か」という疑問が生まれ、添付されたNexnos向けのBranch Convention資料（LTS Release Branch Flowの定義）を確認した。

調査の結果、GitHub Flow・Git Flowの公式定義とLTS Release Branch Flow資料を比較すると、これらは現在検討中の3 Patternより一段具体的な概念であり、`main`保護の有無だけでなく`maint/vX`・`next`・`release`・`hotfix`・パッチ反映・メジャーバージョン移行・Branch削除までを含む、Branch運用全体のライフサイクルを定義するものだと分かった。

ここでユーザーから重要な指摘があった。「リポジトリ構築時にブランチパターンを1つ選択する、という話は少し抽象的だったかもしれない。実際にリポジトリとして決めるべきは、mainの扱い・Branch必須か・PR必須か・Issue＝GitHub Projectとの関係・永続Branch／hotfix経路など、ブランチを運用するための大きな枠組み全体であり、今考えているようなBranch Patternという小さな話ではない」。

### Branching Model概念への転換

この指摘を受けて設計を立ち戻った。Branch Conventionの文脈でPattern Conventionが選ばせるべき実体は、保護レベルの違いのような部分的な差分ではなく、`main`の役割、直接変更可否、作業Branchの要否、PR要否、Issueとの対応、分岐元・統合先、永続／一時Branchの分類、hotfix・release・保守経路、Branch Protectionまでを一体として定義する「Branching Model」である、という整理に至った。

用語を次のように整理した。

- Pattern Convention：Convention Extension Architecture上の共通概念（レイヤー名）
- Branching Model：Branch ConventionにおけるPattern Conventionの実体（他のConventionでは別の実体名になりうる。例：Commit Conventionなら"Commit Style"）

この整理により、GitHub Flow・Git Flow・LTS Release Branch Flowはすべて同じ「Branching Model」という選択肢として横並びに扱えるようになった。また、それまで避けていた「Flow」という語も、「モデル名でFlowを使わない前提は以前のBranch Pattern時代の話で、現在はBranchの運用・ライフサイクルを定めるBranching Modelに考えが移行したので、むしろFlowという語の方がBranching Modelとしては適合する」という再評価により、採用してよいことになった（後述のMain Branch Flowの命名）。

この転換を受けて、それまで進めていた3 Patternファイル作成作業は一旦中止した。

### 3つのBranching Modelの特定とBase Branch Conventionの再分類方針

Branching Modelとして最初に必要なものは、当初どおり次の3つで確定した。順序は指定せず、抽象度が低く設計しやすいものから段階的に進める方針にした。

1. `.github`向け独自Model（仮称：Main-Primary Model）
2. Symnous向け独自Model（仮称：Selective Branching Model）
3. Nexnos向け：LTS Release Branch Flow

同時に、現行Branch Conventionの各Ruleを「Base共通Rule」「特定Branching Model固有Rule」「Repository固有Rule」の3区分へ再分類する方針を決めた。この時点で、次のRuleは特定Modelに依存していると判断された。

- `<type>/<issue-number>-<short-description>`という命名形式：Issue番号を必須としないModelもある
- Issue → Branch → Commit → PR → Merge → Deleteという固定ライフサイクル：ほぼGitHub Flow型の具体的フローであり、すべてのModelに共通しない
- 1 Issue = 1 Branch：すべてのBranching Modelに共通する原則ではない
- Merge後にBranchを削除：`maint/vX`のような永続Branchには適用できない

またこの段階で、GitHub Projectの扱いについても境界が意識された。「Task Issueとの対応」はBranching Modelが扱うが、「GitHub Projectを使うか」「StatusをいつどうVaryさせるか」「Epic／Feature／Taskの管理」はGitHub Project Conventionの責務であり、「Issue必須」と「GitHub Project必須」は別の軸として扱う必要がある、という認識が生まれた。これが後のTask Issue／GitHub Project責務分離の伏線になった。

### Base Branch Conventionの再設計（Claudeによる実装）

上記の方針に基づき、Claudeへ`docs/conventions/branch.md`の再設計を依頼した。Base Ruleの範囲は「個別のBranching Modelに共通する原則と、Branching Modelが満たすべき最低限の契約」に限定し、mainへの直接Commit可否、作業Branch必須か、PR必須か、IssueとBranchの1対1か、使用するBranch Type、Merge方式、release／hotfix構成などはBaseで決めないと明確化した。

Rule Category構成は、旧来の`NM`（命名）・`TY`（Type）・`LC`（ライフサイクル）・`CR`（作成）・`DL`（削除）から、`BM`（Branching Modelの選択・定義要件）・`NM`（命名共通原則）・`LC`（寿命・終了条件）・`EX`（Repository拡張）へ整理した。`TY`と`CR`は個別Ruleが特定Modelへ移るため廃止し、`DL`は`LC`へ統合した。

Rule ID再採番については、当初は「削除する旧IDは欠番として維持する」方針だったが、この再設計は正式運用開始前の全面的な見直しであるとして、既存Rule IDの維持・欠番維持を要求せず、新しいCategoryごとに`001`から振り直す方針へ変更された（この例外は今回の設計段階に限り、正式運用開始後は通常の再利用禁止・欠番維持ルールへ戻す）。

Base Branch Conventionのレビュー過程で次の修正が入った。

- `main`のような永続Branchには終了条件が存在しない場合があるため、Branching Modelの定義要件Ruleにおいて、終了条件の定義対象を一時Branchに限定するよう修正した
- Branching Modelが特定のBranchや運用経路を使用しない場合、その旨を明示できるとする補足を追加した
- Repository Conventionで許容される変更範囲（選択したBranching Modelの基本構成・変更経路を維持する範囲に限る、中心的構造を変える場合は新しいBranching Modelとする）を明確化した

### Work Branchの定義とTask Issue対応の1対1原則

Branch Conventionの各Modelが「作業を隔離する一時Branch」を持つことが共通して必要だと分かり、Base Branch Conventionへ「Work Branch」という用語を新設した。Work Branchは「独立した作業単位の変更を、デフォルトBranchなどから隔離して行うための一時Branch」であり、この定義自体にはTask Issueとの対応関係を含めない（Work Branchは必ずTask Issueを必要とする、とは書かない）。release・hotfix・保守・移行Branchも自動的にWork Branchへ含めず、各Branching ModelがどのBranchをWork Branchとして分類するかを決める。

Task IssueとWork Branchを対応させる場合の原則として、`BR-BS-BM-004`を新設した。当初のRule文は片方向（1つのTask Issueに1つのWork Branch）のみだったが、レビューで「複数のTask Issueが同じWork Branchへ対応することも禁止すべき」という指摘があり、双方向の1対1（1つのWork Branchを複数のTask Issueに対応させない）へ修正した。

このRuleは、Task IssueまたはWork Branchの作成自体を必須にしない。IssueなしWork Branchの可否、Task IssueをWork Branchなしで完了できるか、Pull Requestの要否は、いずれもBranching Modelが定義する。

### Task Issue・GitHub Project・Work Branchの責務分離

Base Branch Conventionのレビューが進む中で、「Task Issueを作成する」ことと「GitHub Projectで管理する」ことが暗黙に同一視されている状態が問題として浮上した。

確定した整理は次のとおり。

- Task Issueは、GitHub Projectを使用しない場合でも、Task Issueテンプレートを使って作業内容・背景・完了条件を管理するために作成できる（Task Issue作成 ≠ GitHub Project登録）
- GitHub Projectで管理する作業には、Task Issue → GitHub Projectへ登録 → Work Branch → Pull Request → mainなどへMerge → Issue Close → Project StatusをDoneという厳格なフローを適用する
- GitHub Projectで管理しないTask Issue、Issueなし作業、IssueなしWork Branchの可否・変更経路は、選択したBranching Modelが定義する

この整理に伴い、`docs/conventions/github-project.md`（GitHub Project Convention）へ`GP-BS-MW-001`（Managed Work Rule）を新設し、Purposeと Design Principles（Responsibility Separation）を、Status運用だけでなくProject管理作業の基本フローも扱う文書へ拡張した。

レビューで、`GP-BS-MW-001`のRule本文が当初「対応するWork BranchおよびPull Requestを使用する」という表現に留まり、Pull Requestの1対1性が弱く読める状態だったため、「Branch Conventionに従って対応するWork Branchを作成し、そのWork Branchの変更を1つのPull Requestとして統合する」という表現へ強化した。またPull Request再作成时の扱い（旧PRと新PRの対応関係・理由を記録する。継続的に異なる運用を採用する場合はRepository Conventionで明示する）を追記した。

Epic・Feature・Taskの意味・階層の正本は、引き続き`docs/specifications/github-project-setup.md`（GitHub Project Setup）に置き、Branch Conventionはこれを再定義せず、Work Branchと対応できるIssue種別としてTask Issueを参照するだけにとどめた。

### `.github`向けBranching Model：Main Branch Flowの設計

.github向けModelの設計対象を、`.github`リポジトリの実際の運用（Issue登録なしの直接編集を含む、単純なドキュメント・Workflow管理）から出発して定義した。

要点：

- `main`を唯一の永続Branchとし、正本かつ通常の作業場所とする
- `main`への直接Commit／Pushを許可する（Branch Protectionとして直接Push禁止を標準要求しない）
- Work Branchは任意で使用できる一時Branchとする
- GitHub Project管理作業だけは、Task Issue・Work Branch・Pull Requestを必須とする厳格フローとする
- Project管理外のWork Branchを統合する場合、Pull RequestはSHOULD（基本経路だが必須ではない）とする
- `develop`・release・hotfix・保守Branchなど`main`以外の永続Branchは標準構造に含めない

名称は、「ブランチ名は単純な名称が好み。名前だけでフローを理解させることは不可能なので概要的な名称で十分」というユーザーの意向により、Main Branch Flowで確定した。前述のとおり、この時点では「Flow」という語を避ける理由がすでに解消されていたため、この名称選択と矛盾しなかった。

Main Branch Flowの各Rule内容（構造・変更経路・Issue関係・命名・ライフサイクル）は、Pattern Conventionの実装（`docs/conventions/patterns/branch/main-branch-flow.md`）として確定し、その後のレビューで、`main`を唯一の永続Branchとする境界表現の統一や、追加永続Branch・未定義変更経路が必要な場合はRepository Conventionではなく新しいBranching Modelとして扱う、という表現の整合が図られた。

### Symnous向けBranching Modelの検討と最終的な不要判断

当初、Symnous向けには専用のBranching Model（仮称：Selective Branching Model、後にdual-track等の名称も検討）を作る想定で議論が進んでいた。

検討の過程で、AIが生成した候補を人が確認してからCommitする場合と、Commit後にPRで確認してMergeする場合とで「人による正式採用のタイミング」が異なるという整理から、Symnousには「定型的な知識運用はmain直接、設計・開発変更はBranch＋PR」という2経路併用モデルが必要という方向で設計が進んだ。

しかし、`.github`向けModel（Main Branch Flowの前身）が固まった段階で、「mainへの直接Commit／Pushも標準経路にすると、Main Branch Flowとの違いが薄くなるのではないか」という疑問が生じた。実際に比較すると、Symnous向け案は「Main Branch Flowを少し厳格にしたもの」に近く、モデルとして分ける意味のある境界（Work Branchを通常経路に固定する、あるいはmain直接操作を明確に限定用途にする）を持たせない限り、実質的にMain Branch Flowと同じだと分かった。

続いてユーザーから「Symnousやモノレポでデータとツール開発を同居するような構成のとき、Main Branch Flowと明確に違いがあるのか不明瞭になってきた」という振り返りがあり、これを機に方針を立ち戻った。

再整理の結果、次の結論に至った。

- Symnousが抱える複雑さは、Branching Modelの選択の問題ではなく、変更の性質（Raw Dataの日常追加、機械的なメタデータ更新、Knowledge／Valuesの実質変更、ツール開発、スキーマ・データ構造変更、GitHub Project管理作業）ごとにどの変更経路を使うかという、Repository Convention・Symnous固有運用の問題である
- モノレポであること自体は別Branching Modelを作る理由にならない。重要なのは変更の性質であり、リポジトリの構成ではない
- Main Branch Flowは「すべての変更をmainへ直接入れるモデル」ではなく「main直接変更とWork Branchによる変更を、作業の管理方法に応じて選択できるモデル」であるため、Symnousの変更種別ごとの経路選択は、Main Branch FlowのRepository固有運用として十分表現できる

最終的に、「Symnous向けのブランチモデルを専用で考える必要はなく、やりたいことはMain Branch Flow内で実現できることが分かった」というユーザーの判断により、Symnous専用Branching Modelは作成しないことで確定した。Symnousは、Main Branch Flowを採用したうえで、変更種別ごとの経路方針をRepository Convention・Symnous固有運用として整理する（今回のセッションでは、その具体的な文書化までは行っていない）。

### LTS Release Branch Flow（Nexnos向け）の保留

Symnous向けModelの検討決着後、残るBranching ModelはLTS Release Branch Flow（Nexnos向け）だけになった。設計を始めるにあたり、既存のNexnos向けBranch Convention資料を土台に、現行ルールをそのままPattern化できるか、再設計が必要かを確認する段階まで進行順序を整理した（`main`の役割、`maint/vX`など保守Branchの役割、次期バージョン開発Branchの有無、release Branchの役割と寿命、hotfixの分岐元・統合先、複数LTS系列の並行保守、Tag・Releaseとの関係、EOL後のBranch扱いが論点として挙げられていた）。

しかし、実際に設計に入る直前で「LTS Release Branch Flowについては実際のOSSプロジェクトの開始前に考えましょう」という方針転換があった。理由は、リリース頻度、セマンティックバージョニングの運用、複数バージョンの並行保守期間、LTS対象バージョン、hotfixの扱い、backport方針、release candidateの有無、CI/CDと配布方法、EOL後のBranch管理といった具体要件が、実際のOSSプロジェクトが存在しない現時点では確定できず、先に設計するとNexnos由来の想定を一般化しすぎたり、実運用に合わない永続Branchを固定したりする可能性があるためである。これはBranching Model作成そのものにもDesign When Neededの原則を適用した判断である。

この方針転換の結果、Branching Model関連の状態は次のとおりで確定した。

- Base Branch Convention：完成
- Main Branch Flow：完成
- `.github`へのMain Branch Flow適用：完了
- Symnous専用Model：不要と判断
- LTS Release Branch Flow：実際のOSSプロジェクト開始前まで保留

### `.github`へのRepository Manifest適用

Symnous専用Model不要の判断後、Main Branch Flowを`.github`リポジトリへ正式適用する作業（Repository Manifest作成）へ進んだ。この作業はClaudeが担当し、次の判断が生じた。

- `.github`自身は、共通資産（Issue Template、PR Template、Label定義）の提供元であると同時に、それらの適用先でもあるという特殊性を持つ。Templateについては`.github/ISSUE_TEMPLATE/`等と`templates/issue-templates/standard/`等の内容を実際に比較し、内容が一致することを確認したうえでSource／Destinationを記載した
- Labelについては、`templates/labels/standard/README.md`に「`.github/labels.yml`は本Templateの適用結果である」と明記されていたことを根拠に、通常は個別リポジトリ向けの回避規定（`templates/labels/standard/labels.yml`をSourceに記載しない）の対象外として扱い、Source／Destinationを記載した
- Workflowについては、`.github/workflows/sync-labels.yml`がReusable Workflow本体であり、Caller Template（`templates/workflows/label-sync/sync-labels.yml`）の適用結果ではないことを確認し、「該当なし」とした
- `.github`固有のBranch Repository Conventionは作成しなかった。理由は、現在の運用がMain Branch Flow本体で表現でき継続的な差分がないこと、および`.github`自身にとってRepository Conventionの配置パス（`docs/conventions/branch.md`）がBase Conventionの正本と競合し、現行のRepository Convention配置規則では配置方法が定義されていないことの両方による

Manifest作成後、Source表記を`noxris42/.github@...`という完全修飾形式で書くか、`.github`自身のManifestなので相対パスでもよいのではないかという疑問が出た。検討の結果、Source表記の役割は「現在地からの参照」ではなく「資産の正本を識別する宣言」であるため、`.github`だけを特別扱いせず、Repository Manifest Specificationの記法どおり完全修飾形式を維持する方針で確定した。仮に相対パスを許容するとしても、その場しのぎでその場だけ変更するのではなく、Specification自体を正式に改定すべきという整理も示されたが、現行のSpecificationは相対パスの特例を定めていないため、今回の判断（完全修飾形式の維持）に確定している。

また、この過程で`templates/repository-manifest/repository-manifest.md`と`docs/specifications/repository-manifest.md`内のLabel Sync Workflow Caller TemplateのSourceパスが、実際のファイル配置（`templates/workflows/label-sync/sync-labels.yml`）とずれていること（`templates/workflows/sync-labels.yml`という誤ったパスになっていたこと）が発見され、該当箇所を修正した。修正時に、あわせてExample文中に残っていた「Label Sync Workflowが未実装」「予定パス」という、修正後の実態と矛盾する記述も発見し、修正した。

---

## 現在の未解決事項

- Symnousの変更種別ごとの経路方針（Repository Convention・固有運用としての具体的な文書化）は、今回のセッションでは行っていない
- LTS Release Branch Flowは、実際のOSSプロジェクトが立ち上がるまで未設計のまま保留されている
- `.github`自身のBranch Repository Conventionは、現行のRepository Convention配置規則ではBase Conventionの正本パスと競合するため、配置方法が未定義である。今回是正しておらず、今後Convention Extension Specificationの配置規則を見直す際の課題として残る
- `templates/repository-manifest/repository-manifest.md`のLabels例が`Source: —`のままである点（Symnousのような個別Label定義を持つ場合の記載例が汎用Templateに存在しない点）は、今回の作業では変更していない

## 関連文書

- `docs/architecture/convention-extension.md`
- `docs/specifications/convention-extension.md`
- `docs/conventions/README.md`
- `docs/conventions/branch.md`
- `docs/conventions/patterns/branch/main-branch-flow.md`
- `docs/conventions/github-project.md`
- `docs/specifications/github-project-setup.md`
- `docs/specifications/repository-manifest.md`
- `templates/repository-manifest/repository-manifest.md`
- `docs/repository-manifest.md`
- ADR 0009（共通ルールへの例外はRepository Overrideとして明示する）
- ADR 0011（Conventionは採用後の共通ルールのみを定義し、採用の可否は扱わない）
- ADR 0012（Issueを作業の起点とする）
- ADR 0013（1つのIssueは1つのWorkを表す）
- ADR 0014（Branch運用を採用する場合、Issue・Branch・PRを一対一で対応させる）
- ADR 0020（`.github`リポジトリ自身も共通標準の適用対象とする）
- ADR 0022（規約はBase／Pattern／Repositoryの3層とし、Rule ID単位で拡張する）
- ADR 0023（Branch ConventionをBase Branch ConventionとBranching Modelへ分離する）
- ADR 0024（Task Issue作成とGitHub Project登録を分離し、厳格な1対1経路はProject管理作業に限定する）
- ADR 0025（Main Branch Flowを最初のBranching Modelとして採用する）
- ADR 0026（追加のBranching Modelは実要件が確定するまで作成しない）
