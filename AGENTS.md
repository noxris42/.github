# AGENTS.md (.github / 共通の指示)

noxris42 の各リポジトリで共通に使う、AI エージェント向けの指示です。共通のルール・規定・規約は `.github` だけが持ちます。ほかのリポジトリに同じ内容を書き写さないでください（例外は、雛形から写す「.github への接続手順」だけです）。

- `.github` リポジトリで作業するときは、このファイルが入口になります。
- ほかのリポジトリは、それぞれの AGENTS.md の接続手順からこのファイルを読みます。
- このファイルと `.ai/` 以下に書くパスは、すべて `.github/` からの相対パスです。

## 前提ルール（どの作業でも必ず守る）

### シェルと文字コード

- 文書は UTF-8（BOM なし）・改行 LF です。
- Windows では PowerShell 7（`pwsh`）を使ってください。Windows PowerShell 5.1（`powershell.exe`）は使わないでください。
- 読み書きでは UTF-8 を明示してください: `Get-Content -Encoding utf8 -Raw <path>` / `Set-Content -Encoding utf8NoBOM <path>`
- 外部 CLI にテキストを渡す、または出力を受け取る前に、次を実行してください:
  `[Console]::InputEncoding = [Console]::OutputEncoding = $OutputEncoding = [System.Text.UTF8Encoding]::new($false)`

### Git の操作

- 人の指示なしに、Git の状態を変える操作をしないでください（`status` や `diff` などの読み取りはしてかまいません）。
- Git の状態を変える操作をするときは、先に `.ai/git.md` を読んでください。

### 読めないとき

指示文書が見つからない、または読めない場合は、推測で進めずに作業を止めて報告してください。

## 状況ごとに読むファイル

| 状況 | 読むファイル |
| --- | --- |
| 開発作業をするとき | `.ai/development.md` と、リポジトリが採用している開発モデルのファイル |
| Git の状態を変える操作をするとき | `.ai/git.md` |
| コミットするとき | `.ai/commit.md` |
| 新しいリポジトリに AGENTS.md を作るとき | `.ai/templates/consumer-AGENTS.md` |
