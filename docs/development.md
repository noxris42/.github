# Shared Development Instructions

## Purpose

本書は、`.github`、`ai-cos`、`symnous`の3Repositoryで共通利用する開発指示を定める。

MVPの早期稼働と実用結果に基づく改善を優先する。旧プロジェクトの設計、実装、規約は参考情報であり、自動的な制約としない。

## Development Approach

- **Requirements-first**：実現する価値、要求、成功条件、重要な制約から開発を開始する。
- **AI-delegated Design**：Architecture、技術選択、詳細設計、実装は原則AIに委任する。
- **Top-down Design**：要求から必要な構造を導く。人間による詳細設計の事前確定を求めない。
- **Just-in-time Design**：現在必要な範囲だけ設計し、未使用の拡張や抽象化を先行実装しない。
- **Prototype-first**：動く機能を早期に成立させ、実用検証を通じて改善する。
- **AI-first Integration**：既存AIの機能を優先的に評価し、不足部分をテキスト処理や独自実装で補う。
- **Risk-based Review**：リスクに応じてレビューを実施し、複数AIレビューを一律必須にしない。

## Decision Boundaries

人間は要求、成功条件、重要なArchitecture上の判断、重大なTrade-off、成果の採否を担当する。

重要なArchitecture上の選択肢は、必要に応じて概要を人間と確認する。詳細まで確定する必要はなく、実装時の判断へ委任してよい。

AIは確定した要求と制約の範囲で設計・実装を進める。通常の技術的判断について逐一承認を求めない。

製品の意味、要求、重大なTrade-offに関わる未確定事項が生じた場合は、人間に確認する。

## Execution and Verification

- 1 Taskは1つの主目的を持つ。
- 1 Taskは複数のWork Subjectを含んでよい。
- 1 Work Subject＝1 Commitを基本とする。
- 無関係な変更目的を同一Commitに混在させない。
- 変更の完了後は、適切な技術的検証を行う。
- 作業結果は変更内容、検証結果、残課題を中心に報告する。
- 文書化は現在必要な理解・引継ぎに限定し、構造が安定してから拡充する。

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

- ChatGPT Workは、設計段階で確定した重要事項、判断理由、実装へ委任する事項をDesign Notesに記録する。
- Coding AIは関連するDesign Notesを参照し、確定事項と制約に従って詳細設計・実装を行う。
- Coding AIは、実装中に成立した重要な設計判断と実装結果をDesign Notesに反映する。
- ChatGPT Workはレビュー時に、確定事項、実装結果、Design Notesの整合性を確認する。
- 同じ設計情報を重複して記録せず、既存のDesign Notesを継続的に更新する。

### Decision Status

設計情報は、その意味に応じて次の状態を区別する。

- **Decided**：人間との確認または委任された設計判断によって確定した事項。
- **Proposed**：検討中の案であり、後続作業の確定条件ではない事項。
- **Delegated**：Coding AIなど、後続の担当AIに判断を委任する事項。
- **Implemented**：実装によって実際に成立した設計状態。

固定的な状態管理Schemaは要求しない。ただし、確定事項と提案・委任事項を混同しない。

人間が確定した要求や重要な設計判断は、合意なく変更しない。

AIに委任された技術判断は、委任範囲内で変更してよい。実装済みであることだけを理由に、将来の変更を禁止しない。

### Content

必要に応じて、次の情報を記録する。

- 設計対象の目的と関連する要求
- 確定した重要な設計方針と判断理由
- 採用方式と重要なTrade-off
- 後続へ委任する未確定事項
- 実装後の主要な構成と成立した振る舞い
- 意図的な簡素化、制約、未対応事項

固定テンプレートは要求しない。

コードから容易に確認できる詳細や、保存価値の低い判断を重複して記録しない。

### Source of Truth and Workspace

Design NotesのSource of Truth（正本）は、対象Repository内のファイルとする。GitへのCommit前の変更も含め、ローカルRepositoryの現在の内容を優先する。

ChatGPT WorkでRepositoryに配置するファイルを作成・編集する場合は、Workワークスペースのみで作業する。Repositoryへの配置・コピー・書き戻しはユーザーが行う。WorkはRepositoryへの書き込みや書き込み可否の検証を試みない。

- 新規作成時は、Workワークスペースでファイルを作成し、ファイルへのリンクとRepository内の配置先を提示する。
- 既存ファイルの編集時は、必ずRepository側の最新内容を取得し、それを起点としてWorkワークスペースで編集して改訂版を提示する。
- Workワークスペースに残る過去のファイルを、継続管理する正本や次回編集の起点として使用しない。
- ユーザーはRepositoryへの反映前に、編集開始後の変更がないか確認し、既存の変更を無断で上書きしない。
- ユーザーから反映完了の連絡を受けた後は、WorkはRepository側の内容を確認し、以後の作業ではその内容を参照する。

Workの作業完了は、ワークスペースでのファイル作成・編集と改訂版の提示までとする。ユーザーによるRepositoryへの配置待ちは、Workの書き込み失敗として報告しない。

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

- Implementation Instructionは今回の目的、成功条件、重要な制約、関連するDesign Notesの参照先を中心に記述する。
- Design Notesに保持された情報をImplementation Instructionへ不要に複製しない。
- 後続Taskでは関連するDesign Notesだけを参照する。
- `AGENTS.md`からDesign Notes全件の読み込みを要求しない。
- 実装後は、Design Notesが実際の設計・実装状態と整合することを確認する。
- 設計上の意味が変わらない軽微な変更では、Design Notesの更新を省略してよい。
- Design NotesとCode / Testsが一致しない場合は、要求と確定事項を確認して不整合を解決する。
- 将来の正式設計文書化では、Design NotesをInputとして再評価し、無条件に正式設計へ昇格させない。

## Git Safety

人間から明示的な指示がない限り、Git状態を変更しない。

対象には、`add`、`commit`、`push`、`pull`、`reset`、`restore`、`checkout`、`clean`、`stash`、`merge`、`rebase`、Branch・Tagの作成・削除・切替などを含む。

Read-onlyのGit調査は許可する。

既存のstaged、unstaged、untrackedの状態を尊重する。

ファイルの作成・編集が許可されても、Git操作が許可されたものとは解釈しない。

## Commit Convention

Commitの分割判断、Commit Messageの作成・確認、Commit実行時は`commit.md`を参照する。

通常の開発作業では、Commit規約の事前読み込みを要求しない。
