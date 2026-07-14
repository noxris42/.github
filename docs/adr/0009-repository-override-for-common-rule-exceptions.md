# 0009. 共通ルールへの例外はRepository Overrideとして明示する

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

このプロジェクトの初期段階で、共通ルールとリポジトリ固有ルールの優先順位が検討された。当初案は「①各リポジトリ固有の明示的なルール ②共通の`.github`ルール ③一般的なGitHub運用慣習」という優先順位のみを定義するものだった。

この案に対し、固有ルールが無秩序に共通ルールを上書きできる余地を残すべきではない、という指摘があった。固有ルールを例外として認める場合でも、それが共通ルールとの差分であり、なぜ共通ルールから外れるのかを示せなければ、単なる逸脱と見分けがつかなくなる。

この考え方は、`docs/philosophy/repository.md`の「Commonality with Explicit Exception（明示的例外を伴う共通化）」という基本理念として定式化され、以後、Commit Convention・GitHub Project Conventionなど個別のConvention文書で、それぞれ「Repository Override」という具体的な仕組みとして実装されている。

---

## Decision（決定）

共通ルールを標準とし、リポジトリ固有の事情による例外は、各Conventionが許可した範囲内でのみ、個別リポジトリ側のドキュメントに明示する（Repository Override）。

上書きを許可する具体的な範囲（どの項目を上書きしてよいか）と、明示の方法は、各Convention文書が定義する。

---

## Rationale（理由）

暗黙の例外を許容すると、共通ルールとの差分がどこにあるか、なぜその差分が生じているかが追跡できなくなり、運用の一貫性が失われる。例外を常に明示させることで、共通ルールと個別リポジトリの実際の運用との差分が明文化され、暗黙知に依存しない状態を保てる。

一方で、上書き可能な範囲を無制限にすると、共通ルールを持つ意味自体が薄れる。各Conventionが上書き可能な範囲をあらかじめ限定することで、リポジトリ間の一貫性を維持すべき部分（構造・ツール互換性に関わる部分）と、リポジトリの性質に応じて調整してよい部分（言語・Type・Scope等）を区別できる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| 固有ルールを共通ルールより単純に優先する（差分・理由の明示を伴わない優先順位のみの定義） | 差分と理由の明示を伴わない上書きは、意図的な例外と単なる逸脱の区別がつかなくなり、運用の一貫性を損なう |

---

## Consequences（影響・注意点）

- 各Conventionは、Repository Overrideとして上書きを許可する具体的な範囲を、それぞれの文書内で明示的に限定する（例：Commit ConventionはLanguage・Type・Gitmoji・Scopeのみを上書き対象とする）
- リポジトリ固有の例外は、そのリポジトリ自身のドキュメントに明記する
- 上書き可能な範囲・明示方法の詳細は、本ADRの対象外とし、各Convention文書が引き続き所有する

---

## Related Documents（関連文書）

- `docs/philosophy/repository.md`
- `docs/conventions/commit.md`
- `docs/conventions/github-project.md`
