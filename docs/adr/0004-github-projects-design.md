# 0004. GitHub Projects の設計

日付：2025-04-14
状態：採用

---

## 背景

GitHub Projectsのフィールド構成・Status値・Workflows自動化の設定方針を決める必要があった。特にStatusの遷移設計と、PRレビュー結果（差し戻し・承認）をStatusに反映するWorkflows（⑩⑪）の有効/無効が検討対象となった。

## 決定

**フィールド構成**：`Status` / `Layer` / `Area` / `Priority` の4フィールドを必須とする。`Size` は使用しない。

**Status値**：`Backlog` / `Ready` / `In Progress` / `Review` / `Done` / `Blocked` の6値。

**Workflows**：⑩ Code changes requested・⑪ Code review approved を **有効化** する。

**Status遷移**：
```
Backlog → Ready → In Progress → Review → Ready（差し戻し・⑩）
                                       → Ready（承認・⑪）→ Done
```

`Review → Ready` に統一することで、StatusがどちらのケースもReadyになる。

## 理由

**`Size` フィールドを不採用**：作業粒度はTaskを1〜3時間単位に揃えることで管理する。見積もり精度よりも分解の適切さを重視した。`Size` によるポイント見積もりは個人開発では管理コストが高い。

**`Layer` フィールドを採用**：Epic / Feature / Task の階層をProjectsのフィールドで表現し、Viewでフィルタリングできるようにした。Sub-issue機能による親子関係と役割を分離している。

**⑩⑪を有効化**：個人開発であっても、PRのレビュー結果がStatusに反映されることでチーム開発のフローを体験しながら学習できる。`Review → Ready` に統一することでStatusの意味もシンプルに保たれる。

**`Area` をコミットの `<scope>` と統一**：フィールド値と `<scope>` を一致させることで、IssueとコミットのAreaが自然に対応する。

## 却下した案

**`Size` フィールドの採用**：XS〜XLの相対見積もりを使う案。Task粒度を揃えることで代替できると判断し不採用。

**⑩⑪を無効のままにする案**：学習効果と実害のなさを考慮して有効化に変更した。

**`Todo` をStatus値に含める案**：`Todo` と `Ready` は実質同じ意味になるため `Ready` に統一した。

## 影響・注意点

- `Backlog → Ready` と `Ready → In Progress` の2遷移は自動化できないため手動で変更する
- ⑨ Auto-archive items はOFF。過去Issueを参照・再オープンする運用のため自動アーカイブを無効にしている
- Epic には直接着手せず、必ず Feature または Task に分解してから作業する
- 複数リポジトリを同一Projectで管理する場合、`Auto-add to project` のフィルターに `OR` でリポジトリを追加する
