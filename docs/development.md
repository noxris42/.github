# Shared Development Instructions

## Purpose

本書は、`.github`、`ai-cos`、`symnous`の3Repositoryで共通利用する開発指示を定める。

AI-CoSとSymnousをゼロベースで開発し、早期稼働と実用結果に基づく改善を優先する。旧プロジェクトの設計、実装、規約は参考情報として評価し、自動的に引き継がない。

## Development Approach

- **Requirements-first**：対話で要求の全体像とコアとなる最小要求、成功条件、重要な制約を明確化して開始する。完全な仕様や詳細設計の事前確定を求めない。
- **AI-delegated Design**：確定した要求・制約と委任範囲で、Architecture、技術選択、詳細設計、実装、実行、検証、修正を原則AIに委任する。
- **Top-down Design**：要求から必要な構造を導く。人間による詳細設計の事前確定を求めない。
- **Just-in-time Design**：現在必要な範囲だけ設計し、未使用の拡張や抽象化を先行実装しない。
- **Prototype-first**：動く機能を早期に成立させ、実物、検証結果、主要な判断記録を評価し、要求・仕様を更新して反復する。
- **AI-first Integration**：既存AIの機能を優先的に評価し、不足部分をテキスト処理や独自実装で補う。
- **Risk-based Review**：リスクに応じてレビューを実施し、複数AIレビューを一律必須にしない。

## Decision Boundaries

人間は要求、成功条件、重要な制約、重大な判断・Trade-off、成果の採否を担当する。

AIは確定した要求・制約と委任範囲で作業を進める。通常の内部設計や技術的判断について逐一承認を求めない。

要求変更、固定制約からの逸脱、委任範囲を超える重大な選択は人間に確認する。実行不能な阻害要因が生じた場合は、該当作業を停止し、原因と必要な判断を報告する。独立して進められる作業は継続してよい。

AIが実装した内容を、自動的に正式仕様や人間の承認済み事項として扱わない。検証の成否と人間による承認・採否は別に扱う。

## Communication Language

AIがユーザーへ出力する回答、説明、質問、進捗報告、レビュー結果、完了報告は、日本語で記述する。Claude Code、CodexなどのCoding AIにも適用する。入力資料やツール出力が英語であっても、ユーザー向けの説明は日本語にする。

ユーザーが明示的に別の言語を指定した場合は、その指定を優先する。

コード、コマンド、Identifier、ファイルパス、引用したログなどは必要な原表記を維持する。Repository内の成果物の言語は、その成果物に適用される指示や既存の方針に従う。

## Execution and Verification

- 1 Taskは1つの主目的を持つ。
- 1 Taskは複数のWork Subjectを含んでよい。
- TaskとCommitは1対1に対応させず、Commit単位は`commit.md`に従って変更の意味から決める。
- 無関係な変更目的を同一Commitに混在させない。
- 委任範囲内で実行・検証・修正を行い、成功条件に照らして結果を確認する。
- 作業結果は変更内容、主要な判断・仮定、検証結果、未検証事項、残課題を中心に報告する。検証した対象と条件を明示し、未確認の動作を推測しない。
- 文書化は現在必要な理解・引継ぎに限定し、構造が安定してから拡充する。

## Delegation and Handoff

作業を委任する指示書は、目的、対象範囲、要求資料、成功条件、重要な制約、AIが判断してよい範囲、確認・停止条件、期待する成果物と検証・報告内容を中心に記述する。固定様式は要求しない。

開発モデルは暫定段階であり、モデル全体の思想や詳細手順をすべての実装AIの必読資料としない。個別作業に必要な要求・委任条件・アウトプット要件を渡す。

Task間および外部AIとの指示書・成果物の受け渡しはユーザーが行う。引継ぎ指示書や報告書は、依頼または合意がある場合に作成する。

## Repository Responsibilities

- 開発モデルの方針・知見は`.github`へ蓄積する。
- AI-CoS固有の要求・仕様・設計・検証情報は`ai-cos`、Symnous固有の情報は`symnous`へ保持する。
- 継続参照する情報の正本は対象Repository内に置く。旧資料から採用する情報は必要な内容を対象Repositoryへ取り込み、旧資料へのリンクだけに依存させない。

## Design Documentation

重要な設計情報は、Design NotesとしてRepository内に記録・維持する。

Design Notesは正式なArchitectureやSpecificationではなく、要求・設計・実装を通じて成立した決定事項、判断理由、現在の設計状態を継続的に共有・再利用するための資料である。

### Organization

- Design Notesは各Repositoryの`docs/design-notes/`に配置する。
- Task単位や設計・実装の工程単位ではなく、機能・コンポーネント・横断的な設計領域を単位として管理する。
- 同じ設計対象の記録は、Taskをまたいで継続的に更新する。
- 設計と実装の情報を原則として同じDesign Noteに保持する。
- ファイルの作成・分割・命名は必要に応じて判断し、未使用の構造を先行作成しない。

### Design and Implementation

- 作業を担当するAIは、成立した主要な設計判断、判断理由、補った仮定、後続へ委任する事項を必要な範囲でDesign Notesに記録する。ChatGPT Workによる詳細設計や記録の事前完了を、実装開始の必須条件としない。
- Coding AIは関連するDesign Notesを参照し、確定事項と制約に従って詳細設計・実装を行う。
- Coding AIは、実装中に成立した重要な設計判断と実装結果をDesign Notesに反映する。
- 成果を評価する担当AIは、要求・制約、実装結果、検証結果、Design Notesの整合性を確認する。
- 同じ設計情報を重複して記録せず、既存のDesign Notesを継続的に更新する。

### Decision Status

設計情報は、その意味に応じて次の状態を区別する。

- **Decided**：人間との確認または委任範囲内のAIの判断によって確定した事項。重大な事項では判断者・根拠を分かるようにし、AIの判断を人間の承認と混同しない。
- **Proposed**：検討中の案であり、後続作業の確定条件ではない事項。
- **Delegated**：Coding AIなど、後続の担当AIに判断を委任する事項。
- **Implemented**：実装によって実際に成立した設計状態。

固定的な状態管理Schemaは要求しない。ただし、確定事項と提案・委任事項を混同しない。実装状態に加え、必要な範囲で検証済み・未検証と人間の承認・採否を区別して記録する。Implementedは、検証済み・承認済みを意味しない。

人間が確定した要求や重要な設計判断は、合意なく変更しない。

AIに委任された技術判断は、委任範囲内で変更してよい。実装済みであることだけを理由に、将来の変更を禁止しない。

### Content

必要に応じて、次の情報を記録する。

- 設計対象の目的と関連する要求
- 確定した重要な設計方針と判断理由
- 採用方式と重要なTrade-off、補った仮定
- 主要な検証結果と未検証事項
- 後続へ委任する未確定事項
- 実装後の主要な構成と成立した振る舞い
- 意図的な簡素化、制約、未対応事項

固定テンプレートは要求しない。

コードから容易に確認できる詳細や、保存価値の低い判断を重複して記録しない。

### Source of Truth and Workspace

Design Notesなど継続参照する情報のSource of Truth（正本）は、対象Repository内のファイルとする。GitへのCommit前の変更も含め、ローカルRepositoryの現在の内容を優先する。

ChatGPT WorkでRepositoryに配置するファイルを作成・編集する場合は、Workワークスペースのみで作業する。Repositoryへの配置・コピー・書き戻しはユーザーが行う。WorkはRepositoryへの書き込みや書き込み可否の検証を試みない。

- 新規作成時は、Workワークスペースでファイルを作成し、ファイルへのリンクとRepository内の配置先を提示する。
- 既存ファイルの編集時は、必ずRepository側の最新内容を取得し、それを起点としてWorkワークスペースで編集して改訂版を提示する。
- Workワークスペースに残る過去のファイルを、継続管理する正本や次回編集の起点として使用しない。
- ユーザーはRepositoryへの反映前に、編集開始後の変更がないか確認し、既存の変更を無断で上書きしない。
- ユーザーから反映完了の連絡を受けた後は、WorkはRepository側の内容を確認し、以後の作業ではその内容を参照する。

Workによるファイル作成・編集の完了は、ワークスペースでのファイル作成・編集と改訂版の提示までとする。Task全体の完了とは区別する。ユーザーによるRepositoryへの配置待ちは、Workの書き込み失敗として報告しない。

Workワークスペースを経由することは、ファイル操作の役割分担であり、追加の設計・承認工程を意味しない。

Repositoryへのファイルコピー・編集とGit操作の許可は区別する。

### File Placement Display

ChatGPT WorkでRepositoryに配置するファイルを作成・編集して提示する場合は、ファイルへのリンクとともに、Repository内の配置先を明示する。

- 配置先は、Repository名から始まる相対パスで表示する。
- ローカルWorkspaceの絶対パス部分は表示に含めない。
- パス区切りには`\`を使用する。
- 例：`symnous\docs\design-notes\overview.md`、`.github\docs\development.md`。
- Work内の作成場所とRepository内の配置先を混同しない。

### Reuse and Consistency

- Implementation Instructionでは、要求資料と関連するDesign Notesのうち今回の作業に必要な参照先を指定する。
- Design Notesに保持された情報をImplementation Instructionへ不要に複製しない。
- 後続Taskでは関連するDesign Notesだけを参照する。
- `AGENTS.md`からDesign Notes全件の読み込みを要求しない。
- 実装後は、Design Notesが実際の設計・実装状態と整合することを確認する。
- 設計上の意味が変わらない軽微な変更では、Design Notesの更新を省略してよい。
- Design NotesとCode / Testsが一致しない場合は、要求と確定事項を確認して不整合を解決する。
- 将来の正式設計文書化では、Design NotesをInputとして再評価し、無条件に正式設計へ昇格させない。

## Commit and Push Workflow

Commit単位の決定、Commit Messageの提案、ユーザーによるCommitの進行管理は、変更を担当するTaskの責務とする。通常はWork Taskが担い、既存の仕組みの範囲で指示内容を改善するInstruction Management Taskでは同Taskが担う。Management TaskはCommit結果を確認し、ユーザーによるPushを取りまとめる。

### Task Responsible for Changes

- Taskの依頼内容だけでなく、実際の差分と検証結果に基づいてCommit単位を決める。
- `commit.md`に従い、各Commitの変更主体、変更目的、対象変更、Commit Message、実施順序を整理してユーザーへ提示する。同一ファイル内で分割が必要な場合は、その対象範囲も明示する。
- Commitはユーザーが実行する。AIはCommitの判断・提案を担い、Commit操作は実行しない。
- ユーザーの実行後に、Commit履歴と残る差分を確認し、意図した変更がCommitされたか確認する。
- Management Taskへ結果を報告する場合は、対象Repository、Commit ID、Commit Message、未Commitの変更と残課題を含める。独立した指示内容の改善では、Work Taskとしての完了報告を一律には要求しない。
- Commit対象の変更がある場合は、Commit完了の確認までをTaskの責務に含める。未実施の場合はCommit待ちとして報告し、完了扱いにしない。Commit対象がない場合は、その旨を報告する。

### Management Task

- 変更を担当するTaskの報告を受け、成果とCommit結果の対応、未Commitの変更、残課題を確認する。
- 確認済みのCommit単位やCommit Messageを通常の完了処理で改めて作成しない。不整合があれば、変更を担当したTaskで修正・追加Commitを扱う。
- Push対象となるRepository、Branch、未PushのCommitを確認し、ユーザーへPush対象を提示する。
- Pushはユーザーが実行する。AIはPush操作を実行しない。
- ユーザーの実行後に、利用可能なローカル・リモートの情報または実行結果からPush結果を確認する。確認できない場合は、確認できた範囲と未確認事項を明示する。

変更を担当するTaskのCommit完了とManagement TaskのPush完了は、別の状態として扱う。Commit単位やCommit Messageの作成を委任しても、Git状態を変更する操作の許可とは解釈しない。

## Git Safety

人間から明示的な指示がない限り、Git状態を変更しない。

対象には、`add`、`commit`、`push`、`pull`、`reset`、`restore`、`checkout`、`clean`、`stash`、`merge`、`rebase`、Branch・Tagの作成・削除・切替などを含む。

Read-onlyのGit調査は許可する。

既存のstaged、unstaged、untrackedの状態を尊重する。

ファイルの作成・編集が許可されても、Git操作が許可されたものとは解釈しない。

設計・実装の委任を、Git操作や外部公開の包括的な許可として扱わない。外部公開はユーザーの明示的な指示範囲で行う。

## Commit Convention

Commitの分割判断、Commit Messageの作成・確認、Commit実行時は`commit.md`を参照する。

通常の開発作業では、Commit規約の事前読み込みを要求しない。
