# 0016. Commit MessageでGitmojiの使用を必須とする

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

Commit MessageにおけるGitmojiの使用可否を検討する過程で、当初は任意（MAY）として扱う案が想定されていた。

改めて検討した結果、GitmojiをTypeの視覚的な補助として標準で必須にすることで、リポジトリをまたいだコミット履歴の視覚的一貫性を確保できることが分かった。

---

## Decision（決定）

Commit MessageではGitmojiの使用を標準として必須とする。TypeにGitmojiを付与し、Typeの前に配置する。

---

## Rationale（理由）

Gitmojiが任意になっていると、リポジトリによってGitmojiを使うものと使わないものが混在し、複数リポジトリを横断してGit履歴を眺めたときの一貫性が失われる。標準で必須とすることで、どのリポジトリのGit履歴も同じ視覚的な識別性を持つ状態を維持できる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| Gitmojiの使用を任意（MAY）とする | リポジトリによってGitmojiの有無が混在し、複数リポジトリを横断したGit履歴の視覚的一貫性が失われる |

---

## Consequences（影響・注意点）

- Commit MessageのHeaderは、Type単独ではなくGitmoji付きのTypeで構成する
- Gitmojiを任意または無効にしたい場合は、Repository Overrideとして明示する。上書き可能な範囲・明示方法自体は本ADRの対象外とする
- GitmojiとTypeの対応関係（どのGitmojiがどのTypeに対応するか）は、本ADRの対象外とし、別途定義する

---

## Related Documents（関連文書）

- ADR 0009（共通ルールへの例外はRepository Overrideとして明示する）
- `docs/conventions/commit.md`
