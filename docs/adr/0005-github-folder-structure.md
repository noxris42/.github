# 0005. `.github/` フォルダの構成方針

日付：2025-04-14
状態：採用

---

## 背景

`.github/` フォルダにはGitHubが自動参照する特殊ファイルを配置するが、自動参照対象外のファイル（`labels.yml`）の配置場所と、個人開発における各特殊ファイルの要否を決める必要があった。

## 決定

- **`labels.yml`**：GitHubの自動参照対象外だが `.github/` に例外配置する（`REPOSITORY_CONVENTION.md` に理由を明記）
- **`CODEOWNERS`**：作成するが `Require review from Code Owners` はOFFで運用する
- **`SECURITY.md`**：最小構成で作成する（公開リポジトリのため存在を示す）
- **`CODE_OF_CONDUCT.md`** / **`SUPPORT.md`**：最小構成で作成する（将来の拡張に備えて存在だけ示す）
- **`FUNDING.yml`**：雛形のみ作成する（収益化予定なし・必要時に追記）

## 理由

**`labels.yml` を `.github/` に例外配置**：`docs/` はドキュメント、`config/` は新設しないという方針から、GitHub運用設定として `.github/` への配置が最も意味的に近い。例外措置として `REPOSITORY_CONVENTION.md` に明記している。

**`CODEOWNERS` を作成するがOFF運用**：個人開発では自己承認の強制は手間になる。チーム開発移行時に `Require review from Code Owners` を有効化することを前提として、ファイルだけ準備しておく。

**`CODE_OF_CONDUCT.md` / `SUPPORT.md` を最小構成で作成**：GitHubのコミュニティプロフィールで不足の警告が出ないよう存在を示す。内容はチーム化・公開時に充実させる。

## 却下した案

**`labels.yml` を `docs/` に配置**：設定ファイルをドキュメントフォルダに置くのは意味的に不自然なため却下。

**`labels.yml` 専用に `config/` フォルダを新設**：1ファイルのためにフォルダを新設するのは過剰と判断した。

**`CODEOWNERS` を作成しない**：将来のチーム移行時に設定漏れが発生しやすいため、今のうちに雛形を作成しておく方が望ましい。

## 影響・注意点

- チーム開発に移行する際は `CODEOWNERS` の内容更新・Rulesetsの `Require review from Code Owners` 有効化・`CODE_OF_CONDUCT.md` の整備を合わせて行う
- `config.yml` の `contact_links` 内のURLは実際のリポジトリURLに変更する必要がある
