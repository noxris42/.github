# GitHub運用規定設計（後半）：ADR運用の再検討とDesign Record概念の誕生

元セッション: [ChatGPT「GitHub運用規定設計」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a4c5e39-b418-83ee-a427-539576852e26)（2026-07-07〜7/13、後半部分）

0004の続き。ADR-0001〜0006を作成した後、ADRの性質そのものへの違和感が生まれ、大規模なADR運用の再検討に発展する。旧Design Record概念の誕生から、Raw Chat Archiveの発想の起源、実際のDesign Record抽出の試行までを扱う。

> [!NOTE]
> ここで誕生した「Design Record」は、今回のADR/DR運用再設計（本プロジェクト最新のセッション）で全面的に置き換えられた旧概念である。design-notesとは名称・設計思想・厳密さが異なる別物として読むこと。

## Notes（メモ）

### ADRの性質への違和感の発生

ADR-0001〜0006を作成した後、「以前作成したADRの姿が、ADRのあるべき姿として頭に残り、進め方に迷う」という違和感が表明された。以前（旧個人アカウント`.github`リポジトリ時代）は議論の議題を主軸にADRを作っており、議事録的な役割も含んでいた。ADRとして残す／残さないの判断も緩く、議題として挙がった事項は基本的に残す、という方針だった。

今回のADR-0001〜0006作成では、この主軸が「議題」から「決定（Decision）」へ変化しており、この変化自体は「成熟」と認識された一方、**情報の欠落**への懸念が生まれた。これが「最初に十数個あったADR候補が漏れなく網羅されているか」という疑問（0004のOpen Questions）の根本原因だったと振り返られている。

この違和感は最終的に「Design Journal式からDecision Record式への変化」と言語化された。また、ADRがSymnous（構想中の知識管理システム）の方向へ引っ張られているようにも感じられた、という指摘があった。

**ADR成熟の3段階仮説**：ChatGPT側から、ADRの理解が3段階で変化したという仮説が示された。第1段階「ADR＝設計テーマをまとめる文書」（例：「Documentation Architectureについて書く」）、第2段階「ADR＝なぜそう設計したかを書く」（ADR-0003あたりから、責務で設計した理由を書く形に変化）、第3段階「ADR＝設計上の問いに対する最終回答」（Question→Decision→Documentationという流れで、Documentationが結果・ADRが判断・Questionが発端という位置づけ）。

**旧ADR12件の実際のレビュー結果**：旧ADR（例：「PostgreSQLを採用」「GitHub Flowを採用」）と現在のADR-0001〜0006（例：ADR-0003「Documentationを責務で設計する」、ADR-0004「Layer Dependency」）を比較したところ、「以前のADRは間違っていたのではなく、ADR成熟度の第1世代」という結論に至った。旧ADRは「Architecture Decision Record」というより「Technical Decision Record」に近く、Decisionが技術選択（What）だった。現在のADRはDecisionが設計思想（Why）にまで抽象化されている。この違いの理由は、旧ADR作成当時はDocumentation PhilosophyもArchitectureも存在しなかったため「ADRが全部説明していた（ADR＝Documentation）」のに対し、現在はDocumentation→ADRという順序（DocumentationがWhatを書き、ADRはDocumentationへ書けないWhyだけを書く）に変化したためと整理された。

この気づきについては、「まだADRを6件書いた経験から得られた知見に過ぎない」として、すぐにADR PhilosophyやADR自体には反映せず、今後さらに設計判断を重ねて理解が揺るがなければ原則化する、という慎重な扱い（ADR-0002のDesign When Neededの自己適用）が取られた。

### 二段階生成フローの発案（重要な転換点）

上記の違和感への解決策として、「前回（議題主軸・Design Journal的）と今回（決定主軸・Decision Record的）のハイブリッド方式」が提案された：

1. まず議事録的に、設計上の議題を主軸に広く記録する（Design Journal的な段階）
2. その候補をもとにDecision Miningを通じて、現在の設計判断（Decision）としてADRを残す（Decision Record的な段階）

ChatGPTによるレビューでは、一般的なADRの考え方（Michael Nygard, 2011の原典、MADRやadr-toolsなど）と、このプロジェクトで実際に作成したADR-0001〜0006の実例の両方に照らして評価が行われた。当初の運用（テーマ単位、比較的広く記録）と現在の運用（決定単位）の違いが整理された。

最終的に「ADRの最終成果物として現在の方針は適している。そのうえで前段階の一時情報を残すか、残さないか、どう残すかという話」という整理に至り、2段階の生成フローの採用が決定された。

**ChatGPT自身による結論の自己修正（重要な転換点）**：Claudeへ客観的な評価を仰ぐための質問状を作成する過程で、ChatGPT自身がそれまでの自分の意見（「ADRを厳密化すべき」）を修正する場面があった。「今回の方針は『ADRを成熟させた』のではなく、『ADRに責務を押し込み過ぎた可能性がある』」という自己修正である。

この過程で、知識を4層に分類する整理が示された：①一次情報（チャット・メモ・議論）、②設計成果（Documentation）、③設計判断（ADR）、そして**④設計検討**——ここが従来抜け落ちていた層だと特定された。例えば「Repository Override」という論点は、ADR候補として検討されながらADR-0006へ吸収されて消えた（ADRにもDocumentationにも残らない）。ずっと感じていた不安の正体は「ADRをDecision Recordにしたこと」ではなく、「設計検討そのものを残す場所がなかったこと」だと結論づけられた。

**OSSにおける2つの潮流への言及**：ADRには「Decision Record派（採用したDecisionだけを書く）」と「Design Journal派（設計検討そのものを残す）」の2つの考え方が存在するという一般化が示され、これにより「以前のADRは議事録的だった」という違和感が、ADRとしての欠陥ではなく「Design Review Record」としての価値だったのではないか、という再評価がなされた。

**最終的な4層構造の確立**：チャット→Design Journal（設計検討）→Decision Mining→Decision Record（ADR）という流れが確定した。これは「ADRを二種類作る」のではなく「成果物を二種類（Design JournalとADR）に分ける」という考え方であり、ADRという言葉の意味がぶれることを避けるため。

この構造は、一般的な知識管理のパターン（Raw→Processed→Curated）とも類比された：Git（Working Tree→Staging→Commit）、GitHub（Issue→PR→Merge）、Symnous（チャット→Knowledge Candidate→Knowledge）と同様、「必ず中間状態が存在する」という一般原則の一例として位置づけられた。

### 中間生成物を残す動機はSymnous思想（重要な背景情報）

中間生成物（Candidate、後のDesign Record）を残すべきかどうかの議論の中で、「明確な理由は持ち合わせていないが残したい」という発言があり、その理由として「情報は残すという方針が好みに合っている。これはSymnous的思想（あらゆる知識・経験をデータ化して蓄積し、第二の脳を作りAI連携する）から来ている」ことが明かされた。

「Symnousを先に考えていなければ、Candidateは中間成果物程度にしか思わず消すことも考えただろう」という自己分析があった。この構造的な動機（Symnous思想がDesign Record重厚化の駆動要因だったこと）は、design-notesが今回のプロジェクトで再設計されるに至った背景として重要である。

### Design Record概念の設計

- 保存場所：`docs/adr/`のサブフォルダか、`docs/`直下かが責務重視で検討された
- 3階層の構造（①以前のADR方式のADR候補＝Design Record、②レビュー結果、③現在方式のADR）について、①②が同一ファイルかどうかが論点になった
- 旧ADR方式の原則（「確定後は触らない、同じ議論が再発したら新たなADRとする」）がDesign Recordにも適用されるかが検討され、最終的に「同一ファイルで、レビューは追記OK」という方針で決定（Symnous側は別途検討）
- Design Recordにも連番が必要とされた。プレフィックスは不要（フォルダ階層が役割を果たすため、他の設計ドキュメントフォルダと同じ考え方）
- ファイル名は議題＝トピック単位（旧ADR方式に近い命名）
- 抽出順＝採番順は時系列
- Design Recordの単位（トピックの粒度）について、「大きなテーマの中で議論が細分化した場合にどう扱うか」という粒度の難しさが指摘された。これは後の「Design Recordの抽出粒度に関するレビュー」で、「機械的・明確な基準として定義可能だが推奨しない、方針の方向性だけ示し確定は実例蓄積後に委ねる」という結論になった
- 実際の運用として、Design RecordとADRは「一定の区切りの段階で過去チャットから事後的に抽出する」ものであり、作業そのものが目的ではないことが確認された（この運用スタイルは、現在まさに本セッションで行われているdesign-notes抽出作業と同型である）

### Raw Chat Archive（チャット保存運用）の起源

Design Record抽出の前提として、「ChatGPTのプロジェクト内で過去のチャット全歴を横断参照できるか」が確認され、**できないことが判明**。これにより「チャット全歴を後から一括で解析してDesign Record化する」という当初の前提が崩れた。

対応として、各チャットの終わりに「ここまでの内容を保存して」という指示でチャット全文をエクスポートする運用へ切り替えることになった。これが以後のセッション（0001〜0003）末尾で繰り返し見られる「チャットを保存して」という指示の起源である。

メタデータ入りのプロンプト（YAML Front Matter：title・project・conversation_id・assistant・participants・created_at・exported_at等）を設計し、ChatGPTのProject Instructionsに設定する形で運用化された。JSON形式の可能性も検討されたが、この時点でどちらを採用したかは明確でない。

長大なチャットは1回の応答で出力できる文字数制限を超えるため、Part分割でのエクスポートが必要になることも確認された。ただし「運用の細部の議論はここで止め、まずできる範囲でDesign Recordを抽出する」ことが優先された。

ブラウザ拡張機能（ChatGPT to Markdown）を使えばマークダウン形式でのチャットエクスポートが可能なことも発見された。

### ADRに関する思想・手順のドキュメント化への方針転換

「チャット全歴が取得できることが明確になったので、先にADRに対する思想や手順を言語化したい。そのうえでこのADR化プロセスをChatGPT・Claude・他AIによらず行えるようシステム化したい」という方針転換があった。

この過程で「知識を成熟させるプロセスに見えるが、これはSymnousの領分ではないか」という疑問が出たが、「`.github`リポジトリとして見るとADRが終着点。Symnousで知識に昇格させるのはさらに上位の話」として区別され、「Symnousはここでは忘れて`.github`リポジトリのための設計として進める」ことが確認された。

### Documentation Architectureの改定（Design Record責務の登録）

Design Record導入に伴い、`docs/architecture/documentation.md`の改定レビューが行われた。

**「Architecture（責務追加）→Philosophy（思想定義）」という順序原則の起源（重要）**：Claude側は当初「Design Record Philosophyを先に作る」という前提でレビューを進めていたが、これに対し「Design Recordという成果物（`docs/design-records/`）が先に存在する必要がある」という指摘があった。

この指摘の核心は、「Philosophyは責務を創る文書ではなく、存在する責務を説明する文書」という原則である。例：Documentation Philosophyを書いたからDocumentationという責務が生まれたのではなく、Documentationという責務が既にあったからPhilosophyを書いている。つまり「責務→Philosophy」という順序であり、逆ではない。同じ理屈で、まずDesign Recordという責務がDocumentation Systemへ追加され、その後にDesign Record Philosophyを書く、という順序が正しいとされた。

これにより設計手順が「Step1: Documentation Architectureで責務を追加するだけ（ライフサイクル・運用は書かない）→Step2: Design Record Philosophyでなぜ必要かを書く→Step3: ADR Philosophyの責務境界修正→Step4: Process」という順序に修正された。

この「Architecture先行・Philosophy後続」という順序原則は、今回のADR/DR運用再設計セッションでも一貫して採用されている実装順序（Responsibility-first：Architecture→Philosophy→README→Template）の直接の起源である。

重要な自己修正：当初「Design Record Philosophyの新設自体はDocumentation Architectureの修正を要求しない」と判断していたが、これは誤りだったと後に指摘・訂正された。「ファイルが1つ増えるかどうか」という物理的な変化の大小でArchitectureへの影響を判定していたが、正しくは「責務が新規に生まれるかどうか」で判定すべきだった、という反省が記録されている。

Design RecordとADRの前後関係についても前提の修正があった：当初「Design RecordがADRより前に作成され、ADRの後にDocumentationが反映される」という時系列で解釈していたが、修正後の前提では「Design RecordとADRは、Documentationが既に確定した後に、事後的に設計過程を抽出・整理するための成果物」とされた。

### Design Record Philosophyの新設

Design Recordの本質は「設計判断（Decision）と、それに至るまでの検討過程（Exploration）は、責務が異なる別の資産である」という点にあると整理された。ADRが確定した判断のみを持続的に保存するのに対し、Design Recordは判断に至る過程・比較・未採用案・議論の流れという、それまでどの文書にも正式な置き場がなかった情報を保存する。

「Design Record is an Exploration Record」がADR Philosophyの「ADR is a Decision Record」と対になる冒頭原則として配置された。採用された6原則は、Design Record is an Exploration Record／Design Record Does Not Define Decisions／Design Record Preserves Discarded Paths／Design Record Does Not Replace Documentation／Design Record Does Not Replace ADR／Design Record Does Not Always Converge、である。そのうち「Design Record Does Not Always Converge（結論に収束しなくてよい）」「Design Record Does Not Define Decisions（判断を定義しない）」がテンプレート設計の最優先方針となった。「Does Not Always Converge」は特に重視され、これによってDesign Recordが「ADRの下書き」ではなく独立した成果物として位置づけられた。

「知識資産」という表現は、Symnous／知識管理基盤という別概念を暗黙に呼び込むとして「設計資産」に修正された。

### ADR Philosophyの純化

ADRを「Decision Record」として純化する方針のもと、「ADR Preserves Design Knowledge」が「ADR Preserves Decision Rationale」へ再定義された。ライフサイクル図（Design→Documentation→Review→ADR）は削除され、「区切りで作成する」という原則の文章のみが残された。「ADRはDocumentationを参照する立場」という記述も削除され、「DocumentationはADRへ依存しない」という一方向の記述に簡素化された。

### コミット時の判断：新設か改定か

Design Record Philosophy・ADR Philosophy改定・Documentation Architecture改定という3つの変更が、独立した変更群か、Design Record Philosophy策定に伴う付随変更かが問われた。過去のコミット履歴に照らし、新しい設計は「策定」、既存設計の変更は「改定」という基準で、それぞれ個別にコミットメッセージが検討された。

### Design Record README・テンプレートの設計

`docs/adr/README.md`の構成・文体を踏襲し、Design Record固有の責務に合わせて再構成された。ADR README側からは、Design Recordへ責務が移管された内容（詳細な設計検討・比較検討の全容・議論の流れ・未採用案の詳細等）が取り除かれ、ADRは「確定した判断の運用」だけに絞られた。

テンプレートのYAML Front Matter採用について、「Symnousに引っ張られている気がする」という懸念が示された。理由：`.github`リポジトリで作成したDR・ADRをそのままSymnousに読み込ませる予定は今はなく、Symnousはチャット履歴の生データから独自に解析する設計のため。この懸念を踏まえつつも、いったんはMetadataをYAML Front Matterへ移行する形が採用された。Review Historyの列名は「Related ADR」から「Reference」へ汎用化された（ADR以外の参照にも対応するため）。

**YAML Front Matterはその後撤回され、Markdown表形式へ差し戻された（重要な訂正）**：後続のClaude側レビューセッションで、「Metadataは現在のMarkdown表形式を採用するのが、この`.github`リポジトリの責務・既存文書との一貫性・Design When Neededの原則に最も適している」という判断が下され、YAML Front Matter化は撤回された。理由：ADRテンプレートとの一貫性（ADRはMarkdown表形式のまま）、GitHub上での表示の素直さ（GitHubの標準レンダラーはYAML Front Matterを特別扱いせず、Jekyll/GitHub Pages以外では生の`---`ブロックとしてそのまま表示されるため、ADRと並べたときに見た目が異なってしまう）。これは「ObsidianやAIとの連携のしやすさ」と「GitHub単体での見た目の一貫性」のどちらを優先するかという選択であり、最終的に後者が優先された。

同じレビューで、Explorationセクションに「Question / Discussion / Findings」という参考構成例を追記する案も一度採用されたが、これも直後に撤回された。理由：「自由度を維持する」というテンプレートの根幹方針からすると、参考例を書き足すこと自体が暗黙のうちに「型」を示唆してしまうため。この撤回は、Design Recordが「型を強制しない」という原則をテンプレート設計の細部でも一貫して守ろうとした具体例である。

### Decision EvolutionとExplorationの違い（重要な概念整理）

ADRテンプレートの「Decision Evolution（判断の変遷）」がDesign Recordの「Exploration（設計検討）」と同じ内容を指すのではないか、という疑問が提起された。

この疑問に対する整理：**両者は主語が異なる**。

- Design RecordのExplorationは「検討活動そのものの記録」（何を検討したか、という活動の記録）
- ADRのDecision Evolutionは「採用された判断が辿った変遷の要約」（「○○を考えたが、○○によって、○○に決めた」という、最終判断に至った経路の要約）

当初Claudeは「Design Recordが検討過程全般を持つなら、ADR側に思考の変遷を残す理由はない」としてDecision Evolutionの削除を提案していたが、この区別を踏まえて判断を改め、Decision Evolutionはテンプレートに**残す**方針に転換された。

### ADR Generation Process文書の作成と命名を巡る往復

Design Record・ADRの生成プロセスを文書化する`docs/specifications/design-record-and-adr-generation.md`が作成された。配置理由：`specifications/`は実装可能な仕様を扱う領域であり、Workflowも扱う対象に含まれるため。

その後、「DRはADR生成プロセスの一環である」という捉え方から、ファイル名・概念名を「Architecture Decision Generation」へ変更する提案が出たが、**Claudeはこの提案に反対**した。理由：この提案は「Design Recordはその内部工程で利用される成果物の一つに過ぎない」という前提に立っているが、これはDesign Record Philosophyで確定させた「Design Record Does Not Always Converge」（Design Recordは必ずしもADRへ収束しない）という原則と正面から矛盾するため。この指摘を受けて、名称は現状維持となった。

### Symnous固有名詞の継続的な除去

適用範囲に「Symnousとの連携」という記述が残っていたことが指摘され、過去に置き換えた表現（「知識管理基盤」）に統一する形で修正された。

### 実際のDesign Record抽出の試行

Claudeによる実証として、過去チャット（本セッション以前の0001〜0003に相当する内容）から実際にDesign Recordを抽出する作業が試みられた。

最初に「プロジェクト開始の情報整理」（最も古く、単一のレビューサイクルとして自然にまとまっている会話、8メッセージ）からDR0001として着手。次に「GitHubリポジトリの設計思想とアーキテクチャ」（244メッセージ）は「DR0001より二桁大きく、複数のReview Unitを含む可能性が高い」として、全文抽出前にまず構造を把握する方針が取られた。

この過程で、「1文書=1DR」という単位で悩んでいたこと自体が、Design Record Philosophyの「Design Record is an Exploration Record」の原則から外れかけていたサインだったという振り返りがあった。文書制作の進行（指示書→ドラフト→レビュー→修正というサイクル）自体はDesign Recordが残すべき「検討過程」ではなく単なる作業履歴であり、DRが残すべきは制作の中で実際に行われた比較・判断・却下であって、これは文書単位ではなく設計テーマ単位で自然に切り出せる、という方針転換が行われた。

実際にDR0003「Repository Design Principles」として、Repository Philosophy策定過程（[26]〜[36]付近のメッセージ）が精読され、「文書ができたこと」ではなく「その過程で確定した設計思想そのもの」を抽出する形で作成が進められた。

## Open Questions（未解決事項）

- Design Recordの抽出粒度の機械的基準は「定義可能だが推奨しない」とされ、実例蓄積後に確定するとされたまま、この抽出範囲では確定基準は示されていない
- Design Record抽出の実証作業（DR0001・DR0003）がどこまで完了したか、この抽出範囲では最終結果を確認できていない

## ADR候補（暫定）

- 「ADRは確定した判断のみを記録する」という純化の方針、およびADR PhilosophyでKnowledge RecordからDecision Recordへ再定義した判断
- Decision Evolution（判断の変遷の要約）とExploration（検討活動そのもの）の主語の違いに基づき、両者を別々の資産として併存させた判断（ただし、現在のADR/DR運用再設計ではDecision Evolution自体が撤廃されているため、この判断は「現在は採用されていない過去の判断」として記録する必要がある）
- Convention文書がSpecification文書を参照しない、という依存方向の原則（0004と重複するため、ADR化する場合は0004を判断成立の主たる出典、0005を後続の関連文脈として扱い、ADR自体は1つに統合する）
- Design Recordという中間資産を独立資産として導入した判断
  - Context: 議題主軸から決定主軸へADR運用が成熟する過程で生まれた、情報欠落への懸念
  - Context: Symnous由来の「情報をできるだけ失わず蓄積したい」という価値観が、Design Recordの責務を重厚化させた（「事実・動機」であり、それ自体はDecisionではないためContextとして扱う）

旧ADR方式（議題主軸・広く記録）と新ADR方式（決定主軸）を統合した「二段階生成フロー」（Candidate/Design Journal的段階→Decision Miningで最終ADRへ）は、現在では撤廃された旧判断であるため、独立ADR候補としては扱わない。現行ADR/design-notes運用の再設計ADRを書く際の**Alternative（かつてこの方式を採用していたが、後に置き換えられた前提）**として位置づける。
