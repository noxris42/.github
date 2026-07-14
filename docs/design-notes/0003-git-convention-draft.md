# Git Convention初稿

元セッション: [ChatGPT「Git Convention初稿」](https://chatgpt.com/g/g-p-6a43cfba7f608191a26f67a735cb575c/c/6a464050-28a8-83e8-aef5-e41fd339bcfc)（2026-07-02〜7/11）

Git Convention全体の構想から、Template Architectureの大幅な方向転換、Repository Setup/GitHub Project Setup仕様、Issue駆動運用、Issue/PR Templateの設計までを扱った長いセッション。

## Notes（メモ）

### Git ConventionとCommit Conventionの関係

既存の`docs/conventions/commit.md`と「Git Conventionの一部としてのCommit Convention」の関係が論点になった。結論：Commit Conventionは規模が大きいため独立ファイルとして定義し、他の項目（Branch等）も将来規模が拡大すれば同様に独立ファイル化する、という方針。

GitとGitHubの境界も論点になった：既存のCommit ConventionはGit概念でありGitHub概念（Issue番号等）も含んでいるように見える、という指摘があったが、この時点では明確な結論は出ておらず、後続の議論に持ち越された。

### Branch Conventionの複雑さの発見

過去の参考資料にあったブランチモデル（`main / maint/vX / next / release/* / hotfix/`）はバージョン管理式パッケージ製品向けであり、今回のドキュメント管理用途には`main`のみの運用が適切、Webアプリケーションでは`main`＋`hotfix/*`が適切、という具合に、用途によって適切なブランチモデルが異なることが分かった。

この複雑さへの対処として、当初「ブランチモデルごとにファイルを分ける」案が検討されたが、それを進めると「コミット規約もワークフローもモデルごとに分ける必要が出てくる」ことに気づき、テンプレート領域の話ではないかという疑問が生まれた。しかしテンプレートで細分化すると、デプロイ系・パッケージ系などソフトウェアの分類も細分化が必要になり、設計が行き詰まった。

### Conventionsとテンプレート/フローの責務境界（重要な整理）

議論の末、次の整理に到達した：

- Conventions＝共通認識のレベル。例：「ブランチを使うならこの命名基準に従う」「ブランチにIssue番号を含むならこの順番にする」
- 「LTS Release Branch Flowがどういうフローか」「どういうソフト開発の時にこのフローを使うか」は別次元の話（Conventionsの対象外）

この整理により、Conventionsは「採用するかどうか」ではなく「採用する場合はどう命名・記述するか」という共通ルールに限定されることが明確になった。

「上位設計の概念が出てきたら、先に上位に立ち戻って設計する」という進め方の原則が、この場面で実際に適用された（models/・overrides/という概念が出てきた際、いったんテンプレート設計を中断して上位設計＝Template Philosophyに立ち戻った）。

### 設計アプローチの転換：ボトムアップ分析

上位設計（思想）はトップダウンで進めつつ、実運用に近い部分（現在扱っているテンプレート設計）はボトムアップで進める方が近道ではないか、という提案があった。具体的には、実際に構築されうる具体的なリポジトリ例（個人事業管理・非公開・日本語、等）をいくつか想定し、どこが共通でどこが独自かを分析することから始める、というアプローチ転換。この転換を経て、成果物視点でのフォルダ構造・内容の実運用ベースの整理に進んだ。

### Template Architectureの方向転換（最も重要な決定）

1. 当初、`templates/`を`base/ flow/ audience/ visibility/ management/`という軸で分類する案が検討された。しかし`visibility`・`management`の使い道が具体的にイメージできず、行き詰まった
2. ボトムアップ分析（組織アカウント/Necnos開発環境、個人アカウント等の具体例を実際に書き出す）を経て、「テンプレートファイルをコピーせずとも設定で参照するだけでよいのではないか」という発想が生まれた。理由：ファイル実体をコピーする方式では、各リポジトリに複製されたファイルのルール改定時の修正作業が発生する問題があった
3. 最終決定：**`templates/`はコピー可能な「テンプレートセット置き場」ではなく、構築可能な「テンプレート部品置き場」である**という位置づけに転換。リポジトリ構築の過程で、属性・運用方式に応じてテンプレート部品を取得（Obtain）・編集（Edit）・使用（Use）する、という運用時の初期化手順の中で差異を吸収する考え方
4. Template PhilosophyのNon-Goalsに「各リポジトリの設計判断を代替すること」を明示的に追加。理由：将来TemplateにFlowやAudienceの判断を持ち込もうとする動きへの歯止めとして機能させるため
5. Template Lifecycleとして「個別リポジトリの知見を共通化した場合にのみTemplateへ戻す」という原則を構造として可視化。Repository PhilosophyのEvolve Through Operation・Knowledge over Tacit Knowledgeと整合する形

### Repository Profile概念の扱い

「現在の設計思想にのっとると、Repository Profileの概念は今はなくてもよい、将来必要があれば考える」という判断があった。人が読むかツールが読むかも今は用途が明確でないため決められない、として明示的に導入を見送った（Design When Neededの適用例）。

### 中間成果物ドキュメントの扱い（後のADR/design-notes分離の先駆け）

`docs/architecture/template-use-cases.md`（ボトムアップ分析で作成した中間文書）が、Template Architectureの方針転換後に不要になるかが論点になった。

重要な整理：「後から設計が変わったのではなく、あくまで設計途中の方針変更」であり、これをドキュメントとして正式に保管するかは検討事項とした上で、「設計の方針の確定などの話はADRとして残す程度でもいい」という発言があった。この発言は、後の「確定した判断はADRへ、途中の検討過程は別の場所へ」という設計思想の先駆けと位置づけられる。

### Repository Setup仕様の位置づけの確認

「手順書なので読み物・説明書の扱いでよいのでは」という疑問が出たが、「将来的にも上位設計を残したほうが良いなら上位設計を採用したい」という判断で、Philosophy/Architectureレベルの設計対象として扱う方針が確認された。

### リポジトリ属性・Template Component Matrixの最小化

リポジトリ属性は現時点で最小限にする方針。理由：本来は運用していく中でテンプレート化する流れであるため。

議論が複雑化した原因として、個人アカウントと組織アカウント（Necnos）の考えが混在していたことが振り返られた。「Necnosの話をすべきではなかった」とユーザー自身が振り返り、個人アカウントでは外部参加者を考慮しない方針を明確化した。

Issueテンプレートに直接影響する「管理対象（Management Target）」属性は採用するが、現状は「ソフトウェア」のみで十分（過去の参考資料を流用できるため）とし、他の種別は将来必要になってから追加する。

Workflow・ラベルについても同様に「新しいリポジトリ種別・フローが出てきたときに`.github`リポジトリ側で追加設計してから新規リポジトリに取り込む」という、新規概念→設計→実装→運用の流れが確認された（Design When Neededの適用）。

テンプレートファイルの配置構造については、「末端のファイル名はリネームせず実ファイル名のまま使う。違いはフォルダ階層で表現する」という方針が確認された。

将来課題（スコープの定義ファイル化・CI連携等）は「メモ程度に留め、ドキュメントへの記載は避ける」という判断があった。

### GitHub Project Setup: Areaフィールドの明示的却下

GitHub ProjectのフィールドにArea（＝Scope相当）を持たせるかが再検討され、「活用方法を明確に考えずに雰囲気で採用していた」ことが振り返られた。AreaとScopeは責務が異なるため連携させるべきではないという判断のもと、**Areaは採用せず、必要性が生じたら設計・実装するという方針（Design When Needed）を明示的に確認**。さらに、「未設計の概念をドキュメントに書くこと自体が将来メモになり不要な情報になる」として、Areaについて何も書かないという判断がされた。

Status・Priorityのフィールド値は、参考資料（`PROJECT_CONVENTION.md`）に既存の定義があったため、それを流用する形で確定した。

GitHub Project Setup仕様からは、View設定（未設計のため削除）、「すべてのIssueに設定する」という運用原則（Design PrinciplesからConvention側またはGitHub Project Operation側へ委譲）が外され、この文書はSetup（初期構成）の定義のみに責務を絞る形に修正された。

### Issue駆動運用（Issue-Driven Workflow）の確立

「Issue＝Task」として作業をIssueで管理し、Issueを起点に作業する、という大きな運用思想が導入された。ブランチを使う場合は「1 Issue = 1 Task = 1 Branch = 1 PR」の関係とし、複数の作業を同一ブランチ上に並行させない（レビューが困難になるため）。

**Subject Documentという考え方**：思想（philosophy）を追加する際、それに伴ってarchitectureの変更が必要になることがある。これを「1 Issue = 1 Document」と厳密に決めてしまうとタスクを不自然に分割することになるため、「変更の主体となるドキュメント（Subject Document）」という考え方を導入し、付随する変更は同一タスク内で扱えるようにした。

Closing Keyword（`Closes` / `Refs`）の使い分けは、Commit Convention・Issue Template・PR Templateへ委譲する形で定義された。

### Issue Templateにおける「Notes」概念の一般化

Notes（補足）フィールドについて、「定期的に書く内容は分離・独立化してテンプレートの正式フィールドになる」という考え方が整理された。例：ソフトウェア開発で設計資料へのリンクを書きたい場合、Notesではなく独立した「Input」フィールドを追加する。これはIssueテンプレートの差別化＝専用化の一般原則として確認された。

Issueテンプレートの階層表現（Epic→Task、Feature→Taskなど）は、Sub-issueの親子関係機能を使い、運用上どこまでの階層を使うかは自由とする方針。

Issueテンプレートは、抽象化された「standard/」という名称を採用し、「documentation/」のような特定用途名にはしなかった。プレースホルダーも「例）○○の対応を実施する。」のような汎用形式に変更し、特定用途（Markdown Convention等）を示す表現を除去。理由：ドキュメント管理という管理方式自体がGitHubの本流でありあらゆるリポジトリに共通する考え方だと判断されたため。

配置は`templates/issue-templates/standard/`のみとし、`.github/ISSUE_TEMPLATE/`への実配置は目的が異なるため別コミットで行う方針。

### PR Templateの設計

基本的な考え方はIssue Templateと同じ。YAMLではなくMarkdownファイルであるため、Guidance（項目説明）はHTMLコメントで実装（編集画面には表示されるが、レンダリングされたPR本文には残らない）。これはIssue Templateの`type: markdown`に相当する仕組み。

採用するInput項目は理由付きで整理され、READMEで「何がPR本文に属し、何が属さないか」の判断基準を表にまとめた。PRのライフサイクルに「Merge」ステップを追加：PRは「途中成果物」、Mergeが「完了の定義」であることをフローで明示した。

### コミットメッセージの語彙選択

「文書＝規約は策定、テンプレート＝成果物は追加」という使い分け、「採用」より実装の意味合いに合う「適用」を使う、という語彙の好みが確認された。

### セッション終盤の依存関係整理

次に設計すべきものとその依存関係が整理された：Commit Convention（Workflowから参照されるため依存関係上最も自然）→ Branch Convention（1 Issue = 1 Branchの具体化）→ GitHub Project Operation（Workflowから委譲されたStatus運用の定義）。

セッション終了時、既存の`docs/conventions/commit.md`と、このセッションで参照されていた「Commit Convention」という語の違いを説明するよう求められたが、回答内容はこの抽出範囲には含まれていない。

## Open Questions（未解決事項）

- GitとGitHubの概念の境界（Issue番号のようなGitHub固有概念をGit Conventionでどう扱うか）は、セッション序盤で疑問として出たが明確な結論は確認できていない
- `docs/conventions/commit.md`と、Workflow設計内で言及される「Commit Convention」という語の関係・違いは、セッション終了時点で質問されたが、回答が本抽出範囲に含まれていない
- テンプレートファイル階層による違いの表現が「Repository Setup（手順書）の領分」か「より上位のTemplate設計書の領分」かという問いが出たが、明確な切り分けの結論はこの範囲では確認できていない

## ADR候補（暫定）

後続セッションでの維持・統合状況を確認してから記録要否を判断する。

### ADR化価値が高い

- `templates/`を「コピー可能なテンプレートセット」ではなく「構築可能なテンプレート部品置き場」と定義した判断（代替案との比較が明確で独立して覆せるためADR向き）
- Conventionsとテンプレート/フローの責務境界（「採用するかどうか判断する対象」と「採用する場合の命名・記述ルール」を分離する判断）
- Issue駆動運用・1 Issue = 1 Task = 1 Branch = 1 PRの原則（Subject Documentという例外的考え方とセット。ただし「Issue駆動で作業する」「1 Issue = 1 Task」「Branch使用時は1 Issue = 1 Branch」「1 Branch = 1 PR」がそれぞれ別々に緩和できる可能性があるため、Decision Mining時に分割要否を確認する）
- GitHub ProjectでArea/Scopeフィールドを採用しない判断（責務の違いを理由に明示的に却下した経緯があるためADR向き）

### 現行ADR/design-notes運用ADRのContext・Rationaleへ統合する可能性が高い

- Repository Profile概念を現時点で導入しない判断（Design When Neededの適用例として、他の判断のRationaleでも繰り返し参照される可能性が高い）
- 中間成果物ドキュメント（方針転換前のドラフト）の扱いについての当時の考え方。当時は「途中の検討過程は正式資産として残さず、確定した判断だけをADR相当で残す」という判断だったが、現在の設計は「途中の検討過程はdesign-notesへ残し、確定した重要判断はADRへ」という一段進化した形になっている。この**当時と現在の差分**こそが、現行ADR/design-notes運用ADRのContextとして価値が高い（「なぜ現在の分離設計に至ったか」の実例として使える）
- base/flow/audience/visibility/management軸によるTemplate Architecture案が行き詰まり、ボトムアップ分析へ切り替えた経緯（独立ADRにするより、Template Architectureの方向転換ADRのRationaleとして使う方が自然）

### ADR不要の可能性が高い

- Issue Templateの命名を用途限定（documentation等）ではなく抽象名（standard）にした判断（Template ArchitectureやNaming Conventionの適用結果として説明できる可能性が高く、独立ADRにするほどではないかもしれない）
