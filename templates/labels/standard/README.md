# standard（標準ラベル定義）

本ディレクトリは、個人アカウント全体で使用する標準ラベル定義を管理する。

初期構成では、GitHub Projectsで使用するEpic・Feature・Taskと、対応する標準Issue Templateに必要な最小限のラベルを定義する。

Epic・Feature・Taskは固定された必須3階層ではなく、管理対象の規模・性質に応じて必要なTypeのみを使用する。

## 構成

| ファイル | 用途 |
| --- | --- |
| `labels.yml` | 標準ラベル定義（`EndBug/label-sync@v2` が読み込むYAML配列） |

## 配置先

```text
templates/labels/standard/labels.yml
→ .github/labels.yml
```

`.github/labels.yml` は、個別リポジトリが共通ラベル定義を利用する際にReusable Workflowから参照される公開ファイルであり、本Templateの適用結果である。

## 正本の扱い

標準ラベル定義の正本は本ディレクトリの `labels.yml` とする。`.github/labels.yml` は正本ではなく適用結果であるため、ラベル定義を変更する場合は本ディレクトリを変更し、その内容を `.github/labels.yml` に反映する。
