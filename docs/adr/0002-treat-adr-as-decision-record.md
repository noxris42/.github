# 0002. ADRをDecision Recordとして扱う

## Metadata（メタデータ）

| 項目 | 内容 |
| --- | --- |
| Status | Accepted |
| Date | 2026-07-14 |

---

## Context（背景）

このプロジェクトの初期に作成されたADRは、確定した設計判断の理由（Why）だけでなく、実質的な仕様や技術選択の内容（What）までを併せて記録する形になっていた。これは、当時Documentation体系（Philosophy・Architecture・Convention・Specification）がまだ整備されておらず、現行仕様を記録する場所がADR以外になかったためである。

その後Documentation体系が整い、現行仕様（What）をConvention・Specificationが持てるようになった結果、ADRが仕様まで抱え込む必要はなくなった。これは初期のADRが誤っていたということではなく、Documentation体系の成熟に伴う責務の再配置である。

この移行を踏まえ、ADRという資産自体が何を記録し、何を記録しないかを改めて定義する必要があった。設計検討記録と正式な判断履歴の資産間の責務分離は、別のADRで扱う。

---

## Decision（決定）

ADRは、確定した重要な設計判断と、その判断を将来説明するために必要な情報を記録するDecision Recordとして扱う。

設計検討そのもの、判断から独立した知見、作業履歴はADRの責務としない。

「重要な設計判断」の具体的な判定基準（記録要否）は本ADRの対象外とし、`docs/adr/README.md`が定義する。

---

## Rationale（理由）

検討過程そのものと確定した判断は責務が異なる。検討過程は「何を検討したか」という活動の記録であり、確定判断は「何を採用し、なぜそれで十分と判断したか」という結果の記録である。両者を同一資産に保持すると、ADRの粒度と役割が曖昧になる。

Documentation側が成熟した現在、現行仕様（What）はConvention・Specificationが持ち、ADRはそこに至った判断の理由（Why）を将来へ説明可能にすることに集中できる。ADRを「判断を将来説明するために必要な情報」に絞ることで、この責務がより明確になる。

---

## Alternatives Considered（却下した案）

| 選択肢 | 採用しなかった理由 |
| --- | --- |
| Decision Evolution（判断に至るまでの思考の変遷）をテンプレートに残す | 検討過程そのものと確定判断の要約は主語が異なるにもかかわらず、同一資産に混在させることになり、ADRの責務が曖昧になる |
| Design Insights（判断から独立した知見）を残す | 判断から独立した知見は、ADRの粒度（独立して覆せる決定単位）と整合しにくく、ADRの範囲を超えて肥大化しやすい |
| Knowledge Record的なADR（議事録的に広く記録する旧来の運用）を維持する | ADRが議事録に近づき、「現在有効な規範ではない、正式な履歴記録」という位置づけが曖昧になる |

---

## Consequences（影響・注意点）

- ADRテンプレートはDecision Evolution・Design Insightsに相当するセクションを持たない
- 将来テンプレートの具体的な項目構成が変わっても、本ADRの決定自体は陳腐化しない。本ADRが定義しているのはテンプレートの項目ではなく、ADRという資産の責務そのものだからである
- 設計検討そのものの保存は、ADRとは別の資産（design-notes）の責務とする

---

## Related Documents（関連文書）

- `docs/philosophy/adr.md`
- `docs/adr/README.md`
- `docs/adr/0000-template.md`
