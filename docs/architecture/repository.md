# Repository Architecture（リポジトリアーキテクチャ）

## Purpose（目的）

本書は、Repository Philosophy で定義した思想を、リポジトリ構造・責務・関係性として具体化する。

Repository Philosophy が「なぜそのようなリポジトリを設計・運用するのか」という Why を定義するのに対し、本書はその思想を実現するための How を定義する。構造そのものではなく、その構造を成立させる責務と関係性を定義することを目的とする。

---

## Scope（適用範囲）

本書は、リポジトリ全体を構成するトップレベル要素の責務と関係性を対象とする。

対象は以下を含む。

- リポジトリ全体の構造
- トップレベルディレクトリの責務
- トップレベル要素同士の関係
- リポジトリ全体の情報アーキテクチャ

以下は本書の対象外とする。

- Repository運用思想 → Repository Philosophy
- ドキュメント設計思想 → Documentation Philosophy
- docs配下の詳細構造 → Documentation Architecture
- Markdown記法・命名規則 → Conventions
- テンプレート仕様・Repository Profile・GitHub運用ルール → Specifications

---

## Repository Structure（全体構造）

リポジトリは以下のトップレベル要素によって構成する。

```text
README.md
.github/
docs/
templates/
```

各要素は独立した責務を持ち、責務の重複を避ける。要素の配置場所ではなく、責務によって分離することを原則とする。

---

## Responsibilities（各要素の責務）

### Repository Entry Point（README.md）

リポジトリ全体の入口となる。

このリポジトリの目的・概要・主要ドキュメントへの導線を提供する。詳細な思想・設計・仕様は各ドキュメントへ委ねる。

他の3要素が「領域」として機能するのに対し、README.mdはリポジトリ全体への単一の入口として独立した役割を持つ。

### .github/

GitHubが直接参照・実行する設定領域。

対象は以下を含む。

- Community Health Files
- Issue Template
- Pull Request Template
- Workflow
- Actions
- GitHub設定

GitHubの動作に関わるものを集約して管理する。

### docs/

思想・設計・規約・仕様・ADRを管理する知識領域。

リポジトリ全体の判断基準となる情報を管理する。GitHubが実行する設定や、他リポジトリへ展開するテンプレートは管理しない。

### templates/

他リポジトリへ展開するテンプレートを管理する。

Repository Profileごとの初期構成や雛形を提供する。共通設定そのものではなく、他リポジトリへ適用する成果物として扱う。

---

## Relationships（要素間の関係）

各要素は独立して存在するのではなく、役割に応じた依存関係を持つ。

### docs → templates

`templates` は、`docs` に定義された思想・設計・規約・仕様を反映した成果物である。

テンプレートは独自に設計するものではなく、`docs` を根拠として生成される。

### docs → .github

`.github` 配下のGitHub設定は、`docs` で定義された思想・規約・仕様を根拠として設計する。

Issue Template・Workflow・Actionsなどは、リポジトリ全体の思想や規約を実装したものである。

### templates → Individual Repositories

`templates` は個別リポジトリへ適用するための配布物である。

共通リポジトリで直接利用するものではなく、他リポジトリへの展開を目的とする。

### .github → GitHub Platform

`.github` はGitHubが直接参照・解釈・実行する領域である。

リポジトリ内の他要素とは責務の性質が異なり、GitHubプラットフォームとの接点を担う。

---

## Information Architecture（情報の流れ）

リポジトリ内の情報は、以下の順序で具体化される。

```text
Philosophy
    ↓
Architecture
    ↓
Conventions
    ↓
Specifications
    ↓
Templates / GitHub Settings
```

上位文書は下位成果物の判断基準となる。下位成果物は上位文書と矛盾してはならない。

---

## Design Principles（設計原則）

### Structure by Responsibility（責務による構造化）

リポジトリ全体は責務によって構造化する。配置場所ではなく責務を優先することで、要素の意味が構造から読み取れる状態を維持する。

トップレベル要素は機能ではなく責務によって追加・変更する。新しいトップレベル要素を追加する場合は、既存要素へ責務を統合できないことを確認した上で設計する。

### Clear Separation of Domains（領域の明確な分離）

GitHubが利用するもの(`.github/`)、人間・機械的処理主体が参照するもの(`docs/`)、他リポジトリへ展開するもの(`templates/`)を明確に分離する。

領域をまたいだ責務の混在は、保守性と可読性を損なう。

### Long-Term Maintainability First（長期保守性の優先）

リポジトリ構造は、運用効率よりも長期保守性・一貫性・再利用性を優先して設計する。

短期的な便宜による構造変更は、上位文書との矛盾を生む起点となりやすい。構造の変更は、必ず上位の Philosophy・Architecture に立ち戻った上で判断する。
