# Rule Applicability Resolution Support Specification（規則適用解決補助仕様）

## Purpose（目的）

本文書は、`noxris42` において**最終的なRule Applicability（規則適用性）の判断へ渡すNormative Rule（規範的規則）の候補を安全に絞り込み、その解決知識をDerived Information（派生情報）として再利用可能にするRule Applicability Resolution Support（規則適用解決補助）について、そのConcrete Contract（具体契約）を定義する**Specification Asset（仕様資産）である。

本文書が扱う問いは次の6点である。

1. Rule Applicability Resolution Support（規則適用解決補助）は、既存のFoundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityに対して、どの位置を占めるのか。
2. Candidate Rule Set（候補規則集合）は、どのResolution Phase（解決フェーズ）を経て成立するのか。
3. 各Resolution Phase（解決フェーズ）の結果は、何を保持し、どの条件で再利用でき、どの条件で再利用を停止するのか。
4. Rule Catalog Resolution（規則一覧解決）は、何を対象として、どのPhysical Representation（物理表現）の結果を生成するのか。
5. Repository-level Rule Resolution（Repository共通規則解決）とTarget-specific Rule Resolution（対象固有規則解決）は、適用・選択の設定から、どの規則を有効とし、どの結果を保持するのか。
6. Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）は、どの規則を非適用として除き、どのCandidate Rule Set（候補規則集合）を保持するのか。

本文書が定義するのは、この6点に対するConcrete Contract（具体契約）に限られる。本文書は、Rule ApplicabilityのSemantic Model（意味モデル）を定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するSpecifications Area（仕様領域）に属する通常のDocumentation Asset（文書資産）である。Rule Applicabilityの解決という特定Subjectについて、その解決を補助するDerived Information（派生情報）を生成・保持・再利用可能にするConcrete Contract（具体契約）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

Rule Applicability Resolution Support（規則適用解決補助）のConcrete Contract（具体契約）、すなわちResolution Phase（解決フェーズ）の構成、Minimum Connection Contract（最小接続契約）、ならびに各Resolution Phase（解決フェーズ）の入力・結果・Physical Representation（物理表現）・検証条件・利用停止条件についてのDefinition Authority（定義権限）は本文書が持つ。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は本文書の外にある。本文書はこれらを参照するのみで、再定義・上書きしない。

- Foundation Application、Foundation Application Target（基盤適用対象）、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityの意味と、三者の境界
- Convention（規約）、Normative Rule（規範的規則）、Non-normative Content（非規範的内容）、Rule Identity（規則同一性）、およびRule ApplicabilityがApplicability Scope（適用範囲）とRule Statement（規則文）から定まること
- Rule ID（規則ID）の形式、およびNormative Rule（規範的規則）のConvention Asset（規約資産）上の記述形式
- Current Foundation Application Target Set（現在の基盤適用対象集合）の宣言、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）、Resolved Rule Selection（解決済み規則選択）、およびEffective Foundation State（有効基盤状態）の具体的な構成と導出
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）
- Foundation ProviderのLocationとProvider内部のSource Locationの区別

したがって次は本文書の責務ではない。

- Foundation Application、Foundation Application Target（基盤適用対象）、およびTarget-specific Rule Selection（対象固有規則選択）の意味と境界。→ [Repository Governance](../architecture/repository-governance.md)による。
- Convention（規約）およびNormative Rule（規範的規則）の意味、ならびにRule Applicabilityの意味。→ [Convention Architecture](../architecture/convention.md)による。
- 各Normative Rule（規範的規則）のRule Applicability。→ 当該Normative Rule（規範的規則）のApplicability Scope（適用範囲）とRule Statement（規則文）による。
- Rule ID（規則ID）の形式、およびNormative Rule（規範的規則）の記述形式。→ [Convention Authoring Convention](../conventions/convention-authoring.md)による。
- Current Foundation Application Target Set（現在の基盤適用対象集合）の宣言、Target-specific Rule Selection（対象固有規則選択）の宣言・解決、およびEffective Foundation State（有効基盤状態）の導出。→ [Foundation Application State Specification](foundation-application-state.md)による。
- AI Integration（AI連携）がEffective Foundation State（有効基盤状態）を参照・利用する責務。→ [AI Integration Architecture](../architecture/ai-integration.md)による。
- Foundation ProviderのLocationとProvider内部のSource Locationの区別と合成。→ [AI Context Resolution Specification](ai-context-resolution.md)による。

本文書が定めるのは、これらによってすでに成立しているModelと解決結果を前提として、Candidate Rule Set（候補規則集合）へ至る解決をどのように分割し、その結果をどのように保持・再利用するかである。

### Position（設計上の位置づけ）

本文書は、[Convention Architecture](../architecture/convention.md)、[Repository Governance](../architecture/repository-governance.md)、および[Foundation Application State Specification](foundation-application-state.md)を前提とする。

Rule Applicability Resolution Support（規則適用解決補助）は、[Foundation Application State Specification](foundation-application-state.md)が定める宣言と解決の結果を入力として利用し、その後段で、各Normative Rule（規範的規則）のApplicability Scope（適用範囲）とRule Statement（規則文）に照らして候補を絞り込む。本文書はいずれのSourceもRefinement（具体化）しない。

Design Dependency（設計依存）は次の一方向とする。

```text
Convention Architecture / Repository Governance / Foundation Application State Specification
        ▲
        │ depends on
Rule Applicability Resolution Support Specification
```

本文書は、上位Architecture（アーキテクチャ）およびSpecification（仕様）の意味を変更・補完しない。本文書が定めるConcrete Contract（具体契約）から、上位のConcept（概念）・Responsibility（責務）・Relationship・Boundary（境界）を導出・上書きしない。

## Scope（対象範囲）

### In Scope（本文書が定義する範囲）

- Rule Applicability Resolution Support（規則適用解決補助）の位置づけと、Definition Authority（定義権限）との境界
- 4つのResolution Phase（解決フェーズ）の構成と、Candidate Rule Set（候補規則集合）の成立
- Resolution Result（解決結果）の保持・再利用の範囲と、共通のPhysical Representation（物理表現）
- Minimum Connection Contract（最小接続契約）
- 各Resolution Phase（解決フェーズ）の対象、入力、解決、Physical Location（物理配置）、内容、検証条件、および利用停止条件

### Out of Scope（本文書が定義しない範囲）

- Foundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityの意味
- 各Normative Rule（規範的規則）のRule Applicabilityの最終判断
- Target-specific Rule Selection（対象固有規則選択）の宣言・解決方式
- 変更検知機構、Generator、Hook、Skill、Agent / Workflow、CI / Enforcement
- AI Consumer（AI利用主体）によるResolution Result（解決結果）の利用方式、およびRouting

## Position of Support（補助の位置づけ）

### Derived Information（派生情報）

Rule Applicability Resolution Support（規則適用解決補助）が保持する情報は、Current Authoritative Source（現在の正式Source）から導出されるDerived Information（派生情報）である。Current Authoritative Source（現在の正式Source）とは、各Resolution Phase（解決フェーズ）が必要とするDefinition Authority（定義権限）を持つ、現在のSourceである。本文書は、これらのSourceの固定一覧または分類を定めない。

Rule Applicability Resolution Support（規則適用解決補助）はSource of Truth（正本）ではない。保持された情報とCurrent Authoritative Source（現在の正式Source）から導出される結果とが一致しない場合、成立している内容はCurrent Authoritative Source（現在の正式Source）側である。

### Authority Boundary（権限の境界）

Rule Applicability Resolution Support（規則適用解決補助）は、Foundation Application、Target-specific Rule Selection（対象固有規則選択）、Rule Applicability、およびNormative Rule（規範的規則）のいずれも定義・変更・上書きしない。

```text
Rule Applicability Resolution Support
  derives from
Current Authoritative Source

Rule Applicability Resolution Support
  does not define
Foundation Application / Target-specific Rule Selection / Rule Applicability
```

Rule ApplicabilityのDefinition Authority（定義権限）は、[Convention Architecture](../architecture/convention.md)および各Normative Rule（規範的規則）のApplicability Scope（適用範囲）とRule Statement（規則文）に残る。

### Candidate Rule Set（候補規則集合）

Candidate Rule Set（候補規則集合）は、ある対象Fileについて、最終的なRule Applicabilityの判断へ渡すNormative Rule（規範的規則）の集合である。

Candidate Rule Set（候補規則集合）は、Applicable Rule Set（適用規則集合）ではない。Candidate Rule Set（候補規則集合）に含まれることは、そのRuleがApplicableであること、またはNormative Effect（規範的効力）を持つことを意味しない。最終的なApplicabilityの判断は、実行時に、各Ruleの正式なApplicability Scope（適用範囲）とRule Statement（規則文）から行う。

```text
Candidate Rule Set
≠ Applicable Rule Set
```

Applicability Scope（適用範囲）とRule Statement（規則文）が定めるRuntime Applicability Unit（実行時適用単位）、すなわちFile・Section・Representation（表現）・Occurrence・Development Action等の単位を、本Supportは変更しない。

## Resolution Phases（解決フェーズ）

### Phase Composition（フェーズの構成）

Candidate Rule Set（候補規則集合）は、次の4つのResolution Phase（解決フェーズ）を経て成立する。

1. Rule Catalog Resolution（規則一覧解決）：Target Convention（対象規約）が定めるすべてのNormative Rule（規範的規則）と、その所属を解決する。適用・選択の設定によって一覧を変えない。
2. Repository-level Rule Resolution（Repository共通規則解決）：Repository共通の正式な適用判断を解決し、Rule Catalog Resolution（規則一覧解決）の結果を、`applied` のTarget Convention（対象規約）とその全Ruleと、`not-applied` のTarget Convention（対象規約）とその全Ruleとに二分する。Target-specific Rule Selection（対象固有規則選択）を反映しない。
3. Target-specific Rule Resolution（対象固有規則解決）：Repository-level Rule Resolution（Repository共通規則解決）が有効としたRuleについて、対象FileのTarget-specific Rule Selection（対象固有規則選択）を[Foundation Application State Specification](foundation-application-state.md)どおりに解決し、選択されたRuleと、選択から外れたRuleとに二分する。
4. Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）：Target-specific Rule Resolution（対象固有規則解決）が選択したRuleについて、正式なApplicability Scope（適用範囲）とRule Statement（規則文）、Target State（対象状態）、および必要な正式定義から、対象File全体についてNot Applicable（非適用）を十分確定したRuleを除き、残るRuleをCandidate Rule Set（候補規則集合）とする。

```text
Rule Catalog Resolution
  → Repository-level Rule Resolution
  → Target-specific Rule Resolution
  → Applicability Pre-resolution and Candidate Composition
```

```text
Candidate Rule Set(T)
= rules(Target-specific Rule Resolution, T) − { r | Not Applicable to the whole of T is sufficiently determined }
```

### Phase-local Exclusion（段階ごとの除外）

各Phaseが規則一覧から外すRuleは、Phaseごとに意味が異なる。

| Phase | 外す理由 | 意味 |
| --- | --- | --- |
| Repository-level Rule Resolution（Repository共通規則解決） | Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `not-applied` である | Configuration Exclusion（設定による除外） |
| Target-specific Rule Resolution（対象固有規則解決） | 対象FileのResolved Rule Selection（解決済み規則選択）に含まれない | Selection Exclusion（選択による除外） |
| Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成） | 対象File全体についてNot Applicable（非適用）を十分確定した | Not-applicable Exclusion（非適用による除外） |

設定・選択による除外と、非適用による除外は、別の意味として扱う。設定・選択による除外を、Rule Applicabilityの判断として扱わない。

```text
Configuration / Selection Exclusion
≠ Not-applicable Exclusion
```

各Phaseが保持する除外の一覧には、そのPhaseで外したRuleだけを含める。前段階で外したRuleを、累積して再列挙しない。後続Phaseは、前段階で外したRuleを再び含めない。

### Conservative Exclusion（保守的な除外）

Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）がNot-applicable Exclusion（非適用による除外）とするのは、対象File全体についてNot Applicable（非適用）を十分確定できるRuleに限られる。Not Applicable（非適用）を十分確定できないRule、すなわち不明または未確定のRuleは、Candidate Rule Set（候補規則集合）へ残す。

本文書は、Candidate Rule Set（候補規則集合）へ残すRuleについて、Applicableと確定できるか否か、すなわちTrue / Unknownの区別を要求しない。また、異なるAI Consumer（AI利用主体）の間で解決結果が完全に一致することを要求しない。要求するのは、Not-applicable Exclusion（非適用による除外）が十分確定したNot Applicable（非適用）だけから成ることである。

```text
not sufficiently determined as Not Applicable to the whole target file
→ remains in Candidate Rule Set
```

## Result Retention and Reuse（結果の保持と再利用）

### Retained Results（保持する結果）

各Resolution Phase（解決フェーズ）の結果は、人が直接確認できるDerived Information（派生情報）として、次の基点の下に保持する。

```text
.ai/resolution-support/rule-applicability/
```

| Resolution Phase | 配置 | 結果の範囲 |
| --- | --- | --- |
| Rule Catalog Resolution（規則一覧解決） | `rule-catalog/` | Repository共通 |
| Repository-level Rule Resolution（Repository共通規則解決） | `effective-rules/` | Repository共通 |
| Target-specific Rule Resolution（対象固有規則解決） | `target-selection/<対象FileのRepository相対Path>/` | 対象File |
| Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成） | `candidate-rules/<対象FileのRepository相対Path>/` | 対象File |

対象Fileごとの結果は、現在の解決に必要な対象Fileについてのみ保持する。Repository内のすべてのFileについての生成は要求しない。

配置は、結果の対応関係を認識しやすくするための整理である。対象FileのPathは結果の対象を識別するために用い、PathからRule Applicability、その他の意味を導出しない。`.ai/` 以下の配置は本SupportのPhysical Location（物理配置）であり、本文書は、これらのDirectoryに対してDocumentation Area（文書責務領域）その他のSemantic Responsibility（意味上の責務）を成立させない。

### Result File Set（結果のFileの組）

各Phaseの結果は、次のFileの組として表現する。

| File | 保持する内容 | 該当Phase |
| --- | --- | --- |
| `rules.yaml` | そのPhaseの結果として残るRuleの一覧 | すべて |
| `excluded.yaml` | そのPhaseで外したRuleの一覧 | Rule Catalog Resolution（規則一覧解決）以外 |
| `inputs.yaml` | 対応する解決で直接使用した入力File | すべて |

- 同一Phase・同一対象のFileは、同一の解決によって、対応する組として生成・更新する。一部だけを別の解決の結果で生成・更新しない。いずれのFileも正本ではない。
- 対応関係を確認できない `inputs.yaml` を、再利用可否の判断に用いない。
- 本文書は、対応関係を成立させるためのID、Timestamp、Fingerprint等を導入しない。
- 除外理由の文章、および除外の根拠を示すFieldを保持しない。除外の妥当性は、対象、規則一覧、および入力の内容から確認・再解決する。

### Common Content（共通の内容）

`rules.yaml` と `excluded.yaml` のFile FormatはYAMLとし、意味構造は次である。

```yaml
conventions:
  <convention-reference>:
    - <rule-id>
```

- Top-level Fieldは `conventions` のみである。`conventions` は、Convention Reference（規約参照）から、列挙したRule ID（規則ID）のListへのMappingである。
- Rule ID（規則ID）は列挙して保持する。すべてのRuleを示す記号、Wildcard、および他の一覧の参照によって列挙を省略しない。
- Rule Name（規則名）・Rule Statement（規則文）の複製、判定結果、Task Relevance（タスク関連性）、行番号、Timestamp、およびFingerprintを保持しない。

`inputs.yaml` のFile FormatはYAMLとし、意味構造は次である。

```yaml
inputs:
  - <source-reference>
```

- Top-level Fieldは `inputs` のみである。
- `inputs` は、対応する解決で直接使用した入力Fileの記録である。前段階の入力を機械的に再列挙しない。前段階の結果を用いた場合は、その結果のFileを記録する。
- `inputs` は固定の必須一覧、および全Phaseに共通する完全な入力一覧ではない。Source Record（使用Source記録）として扱い、記録されていないSourceを無関係とは扱わない（「Source Record（使用Source記録）」を参照）。

Convention Reference（規約参照）・Rule Reference（規則参照）・Source Reference（Source参照）の形式、およびbyte-wise ascendingの正規順序は、「Rule Catalog Resolution（規則一覧解決）」の「Reference Form（参照の形式）」と「Canonical Order（正規順序）」に従う。Foundation Provider（基盤提供主体）とConsumer Repository（利用Repository）が同一のRepositoryである場合、Source Reference（Source参照）は当該RepositoryのRepository rootを基準とするRelative Path（相対Path）である。

### Source Record（使用Source記録）

Resolution Result（解決結果）が、その解決に使用したSourceを記録する場合、その記録は次の用途に用いる。

- 再解決または確認のための探索の手掛かり
- 記録された入力の変更を、Resolution Result（解決結果）の再利用可否と照合するための材料

前回の解決で使用されなかったSourceを、そのResolution Result（解決結果）に無関係であるとは扱わない。Source Record（使用Source記録）は、入力範囲を閉じた集合として確定するものではない。

```text
not used in previous resolution
≠ irrelevant to the resolution
```

本文書は、Source間・Resolution Result（解決結果）間のComplete Dependency Graph（完全依存グラフ）を要求しない。

## Minimum Connection Contract（最小接続契約）

本節は、Resolution Phase（解決フェーズ）間の接続と、Resolution Result（解決結果）の再利用について、すべてのPhaseが満たすべき最小の条件を定める。

### Result Scope Correspondence（結果の対象・範囲の対応）

各Resolution Result（解決結果）は、それが成立する対象と範囲を持つ。後続Phaseは、先行Phaseの結果を、その対象・範囲が対応する場合にのみ用いる。

対象Fileごとの結果は、その対象File全体について成立する。ある対象Fileについての結果を、別の対象Fileへ流用しない。Not-applicable Exclusion（非適用による除外）を、それが成立した対象File、および成立時に用いた規則一覧の範囲外のRuleへ適用しない。一部のSection（節）等についてのみ成立するNot Applicable（非適用）を、対象File全体のNot-applicable Exclusion（非適用による除外）へ拡張しない。

### Result Availability States（結果の利用可能状態）

Resolution Result（解決結果）について、次の3つの状態を区別する。

| 状態 | 意味 |
| --- | --- |
| Not Generated（未生成） | 当該対象・範囲についてのResolution Result（解決結果）が存在しない |
| Invalidated（利用停止） | Resolution Result（解決結果）は存在するが、現在の候補の解決へ用いることができない |
| Empty（空） | 現在利用可能なResolution Result（解決結果）であり、その要素がない |

Empty（空）は、Not Generated（未生成）およびInvalidated（利用停止）のいずれでもない。Not Generated（未生成）またはInvalidated（利用停止）を、Empty（空）として扱わない。

```text
Not Generated
≠ Invalidated
≠ Empty
```

`excluded.yaml` が `conventions: {}` であることは、当該対象・範囲についてそのPhaseで外したRuleがないことを意味する。`excluded.yaml` が存在しないことを、`conventions: {}` として扱わない。

### Fallback Resolution（結果が利用不能な場合の解決）

Not Generated（未生成）またはInvalidated（利用停止）であるResolution Result（解決結果）は、利用不能である。

- Rule Catalog Resolution（規則一覧解決）、Repository-level Rule Resolution（Repository共通規則解決）、またはTarget-specific Rule Resolution（対象固有規則解決）の結果が利用不能である場合、必要な対象・範囲について、Current Authoritative Source（現在の正式Source）から解決してから候補を提供する。
- Target-specific Rule Resolution（対象固有規則解決）を解決できない場合、不完全な規則集合を正常な結果として後続Phaseへ渡さない。
- Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）の結果が利用不能である場合、当該対象Fileの現在のTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` 全体を、Candidate Rule Set（候補規則集合）として用いることができる。

```text
Not-applicable Exclusion unavailable
→ Candidate Rule Set(T) = rules(Target-specific Rule Resolution, T)
```

### Invalidation（利用停止）

次の変更が、あるResolution Phase（解決フェーズ）の入力に影響し得る場合、当該Phaseの影響し得る結果と、それを用いる後続Phaseの結果の再利用を停止する。

- Current Authoritative Source（現在の正式Source）の変更
- 対象Fileの内容・属性等、Target State（対象状態）の変更

対象Fileごとの結果は、File単位の組として利用停止する。影響し得る変更がある場合、Ruleごとに部分的に継続利用せず、当該対象Fileの当該Phaseの結果全体の再利用を停止する。

あるPhaseの結果が変更前後で同じであっても、後続Phaseが自身の入力として用いるSourceの変更は無視しない。たとえば、Rule Catalog Resolution（規則一覧解決）の結果が変わらない場合でも、あるRuleの正式なApplicability Scope（適用範囲）またはRule Statement（規則文）の変更は、そのRuleを含む対象FileのApplicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）の結果の再利用を停止させる。

```text
unchanged intermediate result
≠ unchanged downstream input
```

Source Record（使用Source記録）に記録されていないSourceの変更、および新規に追加されたSourceも、各Phaseの入力範囲に照らして扱う。その影響範囲を限定できない場合、全Phaseの結果の再利用を停止する。

Current Authoritative Source（現在の正式Source）またはTarget State（対象状態）の変更、あるいはその影響を十分把握できない状態では、Not-applicable Exclusion（非適用による除外）の安全な継続利用を認めない。

これらの再利用の停止は、すべての対象の即時再生成を要求しない（「Invalidation and Regeneration Separation（利用停止と再生成の分離）」を参照）。

本文書の契約の変更は、全Phaseの入力に影響し得る変更として扱う。

### Invalidation and Regeneration Separation（利用停止と再生成の分離）

Invalidation（利用停止）は、Immediate Regeneration（即時再生成）を要求しない。Invalidated（利用停止）である結果は、その対象・範囲が必要となった時点で、必要な対象・範囲についてのみ再解決すればよい。

Invalidated（利用停止）である過去の結果は、確認のための資料として保持できる。ただし、利用不能であるNot-applicable Exclusion（非適用による除外）を、現在の候補の削減へ用いない。

### Not Required（要求しない事項）

本文書は次を要求しない。

- Repository内のすべてのFileについての、対象Fileごとの結果の網羅
- 生成のたびにすべての対象を再生成するFull Regeneration（完全再生成）
- Repository全体のResolution Result（解決結果）を常に最新に保つこと

### Change Handling Examples（変更の扱いの例示）

次は、Minimum Connection Contract（最小接続契約）から導かれる扱いの例示である。新たな規定ではない。

| 変更・状態 | 扱い |
| --- | --- |
| Convention（規約）へのNormative Rule（規範的規則）の追加 | Rule Catalog Resolution（規則一覧解決）の結果、および後続Phaseの結果の再利用を停止する。追加されたRuleは、再解決したRule Catalog Resolution（規則一覧解決）の結果から後続Phaseへ渡る |
| `applications` 等のRepository共通の適用判断の変更 | Repository-level Rule Resolution（Repository共通規則解決）以降の結果の再利用を停止する。その変更がRule Catalog Resolution（規則一覧解決）の解決に影響せず、他の利用停止条件にも該当しない場合、Rule Catalog Resolution（規則一覧解決）の結果は再利用できる |
| Target Declaration（対象宣言）の変更 | 影響し得る対象FileのTarget-specific Rule Resolution（対象固有規則解決）以降の結果の再利用を停止する。影響し得る対象Fileを限定できない場合は、すべての対象Fileについて停止する。Target Declaration（対象宣言）だけの変更であっても、`effective-rules/inputs.yaml` に記録された `.foundation/application.yaml` が変更された場合は、Repository-level Rule Resolution（Repository共通規則解決）の結果の再利用も停止する |
| 正式なApplicability Scope（適用範囲）またはRule Statement（規則文）の変更 | Rule Catalog Resolution（規則一覧解決）の結果が変わらない場合でも、当該Ruleを含む対象FileのApplicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）の結果の再利用を停止する |
| 対象Fileの内容・属性等、Target State（対象状態）の変更 | 当該対象FileのApplicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）の結果の再利用を停止する |
| Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）の結果のInvalidation（利用停止） | 当該対象Fileの現在のTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` 全体を候補として用いることができる |
| 保存されたResolution Result（解決結果）がない | Rule Catalog Resolution（規則一覧解決）からTarget-specific Rule Resolution（対象固有規則解決）までをCurrent Authoritative Source（現在の正式Source）から解決し、Not-applicable Exclusion（非適用による除外）なしで候補を提供する |
| 影響範囲を限定できない変更、または変更・影響を十分把握できない状態 | 全Phaseの結果の再利用を停止する。Not-applicable Exclusion（非適用による除外）を継続利用しない |

## Rule Catalog Resolution（規則一覧解決）

### Target Conventions（対象規約）

Rule Catalog Resolution（規則一覧解決）の対象は、Current Foundation Application Target Set（現在の基盤適用対象集合）に含まれるFoundation Application Target（基盤適用対象）のうち、現在Convention（規約）として成立するものである。本文書ではこれをTarget Convention（対象規約）と呼ぶ。

- Current Foundation Application Target Set（現在の基盤適用対象集合）は、[Foundation Application State Specification](foundation-application-state.md)が定めるとおり、Provider Declaration（提供側宣言）の `defaults` のKey集合から特定する。
- Foundation Application Target（基盤適用対象）がConvention（規約）として成立するか否かは、当該Asset、および[Convention Architecture](../architecture/convention.md)と[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定める意味に照らして判断する。File名、Directory、その他のPhysical Location（物理配置）から推論しない。
- Target Convention（対象規約）は、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `applied` であるか `not-applied` であるかにかかわらず含める。

Consumer Declaration（利用側宣言）である `.foundation/application.yaml` は、Repository-level Rule Resolution（Repository共通規則解決）およびTarget-specific Rule Resolution（対象固有規則解決）の入力である。適用・選択の設定だけを扱うことを理由として、Rule Catalog Resolution（規則一覧解決）の入力に含めない。

### Rule Extraction（規則の抽出）

Rule Catalog Resolution（規則一覧解決）が規則として抽出するのは、各Target Convention（対象規約）が明示的に定義するNormative Rule（規範的規則）に限られる。

- 各Normative Rule（規範的規則）は、そのConvention Asset（規約資産）上の既存のRule ID（規則ID）によって識別する。
- Non-normative Content（非規範的内容）、すなわち説明・Example・記述例・Concrete Declaration等に現れるRule ID（規則ID）またはRuleに類する記述は抽出しない。
- Retired Rule ID（廃止済み規則ID）は、Current Normative Ruleではないため抽出しない。
- Normative Rule（規範的規則）を持たないTarget Convention（対象規約）も、Resolved Rule Catalog（解決済み規則一覧）へ含める。

### Physical Location（物理配置）

Resolved Rule Catalog（解決済み規則一覧）は、本Supportを保持するRepositoryの次のPhysical Location（物理配置）に、2つのFileとして表現する。Phaseごとの配置は、結果の対応関係を認識しやすくするための整理である。PathからRule Applicability、その他の意味を導出しない。

```text
Repository root
└─ .ai/
   └─ resolution-support/
      └─ rule-applicability/
         └─ rule-catalog/
            ├─ rules.yaml
            └─ inputs.yaml
```

| File | 保持する内容 |
| --- | --- |
| `rule-catalog/rules.yaml` | Rule List（規則一覧）：Target Convention（対象規約）ごとのRule ID（規則ID） |
| `rule-catalog/inputs.yaml` | Catalog Input Record（規則一覧入力記録）：対応するRule List（規則一覧）の解決に実際に使用したSource |

`.ai/` 以下の配置は、本SupportのPhysical Location（物理配置）である。本文書は、これらのDirectoryに対して、Documentation Area（文書責務領域）その他のSemantic Responsibility（意味上の責務）を成立させない。

### File Separation（Fileの分離）

2つのFileへ分離するのは、Rule List（規則一覧）とCatalog Input Record（規則一覧入力記録）を、それぞれ必要とする用途でのみ読めるようにし、AI Context（AI文脈）として読み込む量を削減するためである。Rule List（規則一覧）を用いる解決はCatalog Input Record（規則一覧入力記録）を読む必要がなく、再利用可否の判断はCatalog Input Record（規則一覧入力記録）を用いる。

2つのFileは、1つのResolved Rule Catalog（解決済み規則一覧）に対応する表現である。それぞれが独立したResolution Phase（解決フェーズ）の結果ではなく、いずれも正本ではない。

```text
rule-catalog/rules.yaml + rule-catalog/inputs.yaml
= one Resolved Rule Catalog
```

- 2つのFileは、同一の解決によって、対応する組として生成・更新する。一方だけを別の解決の結果で生成・更新しない。
- Catalog Input Record（規則一覧入力記録）は、対応するRule List（規則一覧）の解決に実際に使用したSourceの記録である。全Phaseに共通する完全な入力一覧ではない。
- 対応関係を確認できないCatalog Input Record（規則一覧入力記録）を、Rule List（規則一覧）の再利用可否の判断に用いない。
- 本文書は、対応関係を成立させるためのID、Timestamp、Fingerprint等を導入しない。

### Rule List Content（規則一覧の内容）

`rule-catalog/rules.yaml` のFile FormatはYAMLとする。意味構造は次である。

```yaml
conventions:
  <convention-reference>:
    - <rule-id>
```

```yaml
conventions:
  docs/conventions/naming.md:
    - NAM-SF-001
    - NAM-SF-002
  docs/conventions/writing.md:
    - WRT-SF-001
```

上記の第2例は意味構造を示すための例示であり、Current State（現在状態）の宣言ではない。

| Field | 必須性 | Allowed Value | 意味 |
| --- | --- | --- | --- |
| `conventions` | 必須 | Convention Reference（規約参照）からRule ID（規則ID）のListへのMapping | Target Convention（対象規約）ごとの、現在のNormative Rule（規範的規則）のRule ID（規則ID） |

- `conventions` は、すべてのTarget Convention（対象規約）をKeyとして含む。Normative Rule（規範的規則）を持たないTarget Convention（対象規約）の値は、空のList `[]` とする。
- 各Ruleは、所属するTarget Convention（対象規約）のConvention Reference（規約参照）と既存のRule ID（規則ID）によって、そのConvention Asset（規約資産）上の正式定義へ到達できる。
- `rule-catalog/rules.yaml` は、`conventions` 以外のTop-level Fieldを持たない。Rule Name（規則名）・Rule Statement（規則文）の複製、Application State（適用状態）、判定結果、行番号、Timestamp、およびFingerprintを保持しない。

### Catalog Input Record Content（規則一覧入力記録の内容）

`rule-catalog/inputs.yaml` のFile FormatはYAMLとする。意味構造は次である。

```yaml
inputs:
  - <source-reference>
```

| Field | 必須性 | Allowed Value | 意味 |
| --- | --- | --- | --- |
| `inputs` | 必須 | Source Reference（Source参照）のList | 対応するRule List（規則一覧）の解決に実際に使用した入力File |

`inputs` には、次を記録する。

- Target Convention（対象規約）の集合を特定するために使用した正式な宣言・契約のSource
- Normative Rule（規範的規則）の抽出に使用したSource
- 上記以外に、当該解決のために実際に必要としたSource

`inputs` は、実際に使用したSourceの記録である。固定の必須一覧ではない。Source Record（使用Source記録）として扱い、入力範囲の閉じた一覧として扱わない（「Source Record（使用Source記録）」を参照）。

`rule-catalog/inputs.yaml` は、`inputs` 以外のTop-level Fieldを持たない。Timestamp、Fingerprint、およびSourceごとの使用理由を保持しない。

### Reference Form（参照の形式）

| 参照 | 形式 |
| --- | --- |
| Convention Reference（規約参照） | [Foundation Application State Specification](foundation-application-state.md)が定めるConvention Reference（規約参照）と同じく、Foundation Provider（基盤提供主体）のRepository rootを基準とするRelative Path（相対Path） |
| Rule Reference（規則参照） | 既存のRule ID（規則ID）。例：`WRT-SF-001` |
| Source Reference（Source参照） | Foundation Provider（基盤提供主体）側のSourceについて、Foundation Provider（基盤提供主体）のRepository rootを基準とするRelative Path（相対Path） |

いずれのFileも、Consumer Repository（利用Repository）の環境上でのFoundation ProviderのLocationを保持しない。その区別と合成は[AI Context Resolution Specification](ai-context-resolution.md)による。

Foundation Provider（基盤提供主体）のRepository root以外を基準とする参照を必要とする入力が判明した場合、本文書はそのための参照方式を定めていない。その入力を独自の方式で表現せず、未確定事項として扱う。

### Canonical Order（正規順序）

同一の解決結果からは、同一のPhysical Result（物理結果）が生成されなければならない。

- `rule-catalog/rules.yaml` の `conventions` のKeyは、Convention Reference（規約参照）のbyte-wise ascendingに並べる。
- `rule-catalog/rules.yaml` の各List内のRule ID（規則ID）は、Rule ID（規則ID）のbyte-wise ascendingに並べる。
- `rule-catalog/inputs.yaml` の `inputs` のSource Reference（Source参照）は、byte-wise ascendingに並べる。

いずれの比較もLocaleに依存しない。Indent、Quote、Document Marker等、Semantic Need（意味上の必要性）を持たないSerializationの詳細は本文書が固定しない。

### Validation Conditions（検証条件）

`rule-catalog/rules.yaml` は、次のすべてを満たす場合に有効である。

- YAMLとして解釈でき、Top-level Fieldは `conventions` のみである。
- `conventions` のKey集合は、Target Convention（対象規約）の集合と一致する。
- 各Keyの値は、当該Target Convention（対象規約）が現在明示的に定義するNormative Rule（規範的規則）のRule ID（規則ID）の集合と一致し、欠落・混入がない。
- 同一のMapping内でKeyを重複させず、同一のList内でRule ID（規則ID）を重複させない。
- 各Rule ID（規則ID）は、それが属するTarget Convention（対象規約）のListにのみ現れる。
- 「Canonical Order（正規順序）」に従う。

`rule-catalog/inputs.yaml` は、次のすべてを満たす場合に有効である。

- YAMLとして解釈でき、Top-level Fieldは `inputs` のみである。
- `inputs` は、対応する `rule-catalog/rules.yaml` の解決において、Target Convention（対象規約）の集合の特定とNormative Rule（規範的規則）の抽出に実際に使用したSourceを含む。
- 同一のList内でSource Reference（Source参照）を重複させない。
- 「Canonical Order（正規順序）」に従う。

2つのFileは、同一の解決によって生成・更新された組である。

### Catalog Invalidation（規則一覧の利用停止）

Resolved Rule Catalog（解決済み規則一覧）は、次のいずれかに該当する場合、Invalidated（利用停止）となる。

- 対応するCatalog Input Record（規則一覧入力記録）の `inputs` に記録されたSourceが変更された。
- `inputs` に記録されていないSourceの変更または追加が、Target Convention（対象規約）の集合、またはNormative Rule（規範的規則）の抽出に影響し得る。
- 上記に該当するか否かを判断できない。対応関係を確認できるCatalog Input Record（規則一覧入力記録）がない場合を含む。

Invalidated（利用停止）であるResolved Rule Catalog（解決済み規則一覧）を用いる後続Phaseの結果も、「Invalidation（利用停止）」に従って扱う。

## Repository-level Rule Resolution（Repository共通規則解決）

### Repository-level Position（位置づけ）

Repository-level Rule Resolution（Repository共通規則解決）は、[Foundation Application State Specification](foundation-application-state.md)が定めるRepository-level Resolution（Repositoryレベルの解決）を用いて、Target Convention（対象規約）ごとのResolved Repository-level Application State（解決済みRepositoryレベル適用状態）を解決する。本文書は、新しいApplication State（適用状態）、解決方式、およびValidation Condition（検証条件）を定義しない。

Target Declaration（対象宣言）は、Repository-level Rule Resolution（Repository共通規則解決）の結果へ適用しない。Target-specific Rule Selection（対象固有規則選択）は、Target-specific Rule Resolution（対象固有規則解決）においてのみ反映される。

### Repository-level Input（入力）

| 入力 | 用途 |
| --- | --- |
| 現在利用可能なRule Catalog Resolution（規則一覧解決）の `rule-catalog/rules.yaml` | Target Convention（対象規約）の集合、および各Convention（規約）が定めるすべてのRule、すなわち `All(C)` |
| Provider Declaration（提供側宣言）`.foundation/application-defaults.yaml` | Shared Application Default（共有適用既定） |
| Consumer Declaration（利用側宣言）`.foundation/application.yaml` | Repository-level Application Difference（Repositoryレベル適用差分） |
| [Foundation Application State Specification](foundation-application-state.md)が定める条件を満たし、Repository-specific Application Decision（Repository固有適用判断）を一意に成立させている他のAuthoritative Declaration（正式宣言） | Repository-specific Application Decision（Repository固有適用判断） |

Rule Catalog Resolution（規則一覧解決）の結果が利用不能である場合は、「Fallback Resolution（結果が利用不能な場合の解決）」に従い、Current Authoritative Source（現在の正式Source）から解決してから用いる。`rule-catalog/inputs.yaml` は、Repository-level Rule Resolution（Repository共通規則解決）の入力ではない。Rule Catalog Resolution（規則一覧解決）の結果が利用可能かの判断にのみ用いる。

### Repository-level Result（結果）

Repository-level Rule Resolution（Repository共通規則解決）の結果は、本Supportを保持するRepositoryの `.ai/resolution-support/rule-applicability/effective-rules/` に、3つのFileとして保持する。

| File | 保持する内容 |
| --- | --- |
| `effective-rules/rules.yaml` | Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `applied` であるTarget Convention（対象規約）と、そのすべてのRule |
| `effective-rules/excluded.yaml` | Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `not-applied` であるTarget Convention（対象規約）と、そのすべてのRule |
| `effective-rules/inputs.yaml` | 対応する両一覧の解決で直接使用した入力File |

両一覧は、Rule Catalog Resolution（規則一覧解決）の結果を、適用状態によって二分したものである。各Target Convention（対象規約）は、そのすべてのRuleとともに、いずれか一方の一覧にのみ現れる。

```text
conventions(rules) ∩ conventions(excluded) = ∅
conventions(rules) ∪ conventions(excluded) = conventions(rule-catalog)
rules(rules) ∩ rules(excluded) = ∅
rules(rules) ∪ rules(excluded) = rules(rule-catalog)
```

- Normative Rule（規範的規則）を持たないTarget Convention（対象規約）の値は、空のList `[]` とする。
- 一覧へ振り分けるTarget Convention（対象規約）がない場合、そのFileは `conventions: {}` とする。
- `effective-rules/inputs.yaml` には、用いた `rule-catalog/rules.yaml` を記録する。Rule Catalog Resolution（規則一覧解決）の入力を機械的に再列挙しない。Repository-level Rule Resolution（Repository共通規則解決）が直接使用したSourceは、Rule Catalog Resolution（規則一覧解決）の入力でもある場合を含めて記録する。

`effective-rules/rules.yaml` は、Target-specific Rule Selection（対象固有規則選択）を反映しない。いずれの対象FileについてのRule Set（規則集合）でもなく、最終的なApplicable Rule Set（適用規則集合）でもない。

### Repository-level Validation Conditions（検証条件）

Provider Declaration（提供側宣言）およびConsumer Declaration（利用側宣言）が[Foundation Application State Specification](foundation-application-state.md)のValidation Conditions（検証条件）を満たし、用いるRule Catalog Resolution（規則一覧解決）の結果が現在利用可能である場合にのみ、結果を正常な解決結果として保持する。満たさない場合は不足する内容を補完せず、不整合として報告する。

保持する3つのFileは、次のすべてを満たす場合に有効である。

- 「Common Content（共通の内容）」に従う。
- `effective-rules/rules.yaml` のKey集合は `applied` であるTarget Convention（対象規約）の集合と、`effective-rules/excluded.yaml` のKey集合は `not-applied` であるTarget Convention（対象規約）の集合と、それぞれ一致する。各値は当該Convention（規約）の `All(C)` と一致する。
- 両一覧のConvention Reference（規約参照）の集合、およびRule ID（規則ID）の集合は、それぞれ互いに素であり、その和集合はRule Catalog Resolution（規則一覧解決）の結果と一致する。
- `effective-rules/inputs.yaml` は、対応する解決で直接使用したSourceを含み、用いた `rule-catalog/rules.yaml` を含む。
- 同一のMapping内でKeyを重複させず、同一のList内でRule ID（規則ID）またはSource Reference（Source参照）を重複させない。

### Repository-level Invalidation（利用停止）

Repository-level Rule Resolution（Repository共通規則解決）の結果は、次のいずれかに該当する場合、Invalidated（利用停止）となる。

- `effective-rules/inputs.yaml` に記録されたSourceが変更された。
- 記録されていないSourceの変更または追加が、結果に影響し得る。
- 用いたRule Catalog Resolution（規則一覧解決）の結果がInvalidated（利用停止）となった、または更新された。
- 上記に該当するか否かを判断できない。対応関係を確認できる `effective-rules/inputs.yaml` がない場合を含む。

適用・選択の設定変更がRule Catalog Resolution（規則一覧解決）の解決に影響せず、かつ他の利用停止条件にも該当しない場合、Rule Catalog Resolution（規則一覧解決）の結果は再利用できる。`rule-catalog/inputs.yaml` に記録されていないことだけを、Rule Catalog Resolution（規則一覧解決）に影響しないことの根拠としない。Rule Catalog Resolution（規則一覧解決）の結果の再利用可否は、「Catalog Invalidation（規則一覧の利用停止）」に従って判断する。

## Target-specific Rule Resolution（対象固有規則解決）

### Target-specific Position（位置づけ）

Target-specific Rule Resolution（対象固有規則解決）は、Repository-level Rule Resolution（Repository共通規則解決）が `effective-rules/rules.yaml` に保持したRuleについて、対象FileのResolved Rule Selection（解決済み規則選択）を、[Foundation Application State Specification](foundation-application-state.md)のHierarchical Resolution（階層的解決）とConvention-level Composition（規約単位の合成）に従って解決する。本文書は、Rule Selection（規則選択）の方式、`independent` / `refine` の意味、およびDeclarationのValidation Conditions（検証条件）を再定義しない。

Target-specific Rule Resolution（対象固有規則解決）は、Repository-level Rule Resolution（Repository共通規則解決）が外したRuleを再び含めない。また、Rule Applicability、Not Applicable（非適用）、およびTask Relevance（タスク関連性）を判断しない。解決結果は、Declaration上の記述順、Declarationの読込順、および解決を行う主体に依存しない。

### Target File（対象File）

対象Fileは、現在の解決に必要なRepository内のFileに限られる。Repository内のすべてのFileの列挙、およびすべてのFileの解決は要求しない。

対象Fileは、Repository内の対象を特定でき、かつ既存のTarget Declaration（対象宣言）の `path` と `scope` が当該対象Fileを包含するかを判定できる形で示されなければならない。[Foundation Application State Specification](foundation-application-state.md)が定める `path` の形式条件は、Target Declaration（対象宣言）そのものの検証条件である。本文書は、これを対象Fileの受入条件へ転用しない。Target Declaration（対象宣言）の `path` は、引き続き同仕様のValidation Conditions（検証条件）に従って検証する。

Pathは、対象Fileの識別と、Target Declaration（対象宣言）による包含の判定にのみ用いる。Pathから対象FileのSemantic Responsibility（意味上の責務）、Classification（分類）、またはRule Applicabilityを推論しない。

### Target-specific Input（入力）

| 入力 | 用途 |
| --- | --- |
| 現在利用可能なRepository-level Rule Resolution（Repository共通規則解決）の `effective-rules/rules.yaml` | 有効なTarget Convention（対象規約）と、その `All(C)` |
| Target Declaration（対象宣言）を保持するConsumer Declaration（利用側宣言）`.foundation/application.yaml` | Target-specific Rule Selection（対象固有規則選択） |
| [Foundation Application State Specification](foundation-application-state.md) `docs/specifications/foundation-application-state.md` | Target-specific Rule Selection（対象固有規則選択）の解決方式と、Declarationの検証条件 |
| 対象File | 解決の対象 |

Repository-level Rule Resolution（Repository共通規則解決）の結果が利用不能である場合は、「Fallback Resolution（結果が利用不能な場合の解決）」に従い、Current Authoritative Source（現在の正式Source）から解決してから用いる。

### Target-specific Result（結果）

Target-specific Rule Resolution（対象固有規則解決）の結果は、本Supportを保持するRepositoryの次のPhysical Location（物理配置）に、3つのFileとして保持する。

```text
.ai/resolution-support/rule-applicability/target-selection/<対象FileのRepository相対Path>/
├─ rules.yaml
├─ excluded.yaml
└─ inputs.yaml
```

| File | 保持する内容 |
| --- | --- |
| `rules.yaml` | 対象FileのResolved Rule Selection（解決済み規則選択）として選択されたRule |
| `excluded.yaml` | `effective-rules/rules.yaml` のRuleのうち、対象Fileの選択から外れたRule |
| `inputs.yaml` | 対応する解決で直接使用した入力File |

- `rules.yaml` は、`effective-rules/rules.yaml` のすべてのConvention Reference（規約参照）をKeyとして保持する。すべてのRuleが選択から外れたConvention（規約）の値は、空のList `[]` とする。
- `excluded.yaml` は、選択から外れたRuleを持つConvention（規約）だけをKeyとして保持する。選択から外れたRuleがない場合は、`conventions: {}` とする。
- 同一のConvention Reference（規約参照）が、`rules.yaml` と `excluded.yaml` の双方に現れてよい。
- 各Convention（規約）について、両一覧のRule ID（規則ID）は重ならず、その和集合は `effective-rules/rules.yaml` の当該Convention（規約）のRule ID（規則ID）の一覧と一致する。
- `inputs.yaml` には、用いた `effective-rules/rules.yaml`、Target Declaration（対象宣言）を保持するConsumer Declaration（利用側宣言）、および対応する解決で使用した[Foundation Application State Specification](foundation-application-state.md)を記録する。前段階の入力を一律に再列挙しない。

`rules.yaml` は、対象FileのEffective Rule Set（有効規則集合）であり、Applicable Rule Set（適用規則集合）ではない。

### Target-specific Validation Conditions（検証条件）

次のすべてを満たす場合にのみ、結果を正常な解決結果として保持し、後続Phaseへ渡す。

- Provider Declaration（提供側宣言）およびConsumer Declaration（利用側宣言）が、[Foundation Application State Specification](foundation-application-state.md)のValidation Conditions（検証条件）を満たす。
- 用いるRepository-level Rule Resolution（Repository共通規則解決）の結果が現在利用可能である。
- Target Declaration（対象宣言）の各Convention Reference（規約参照）が、Target Convention（対象規約）である。
- 対象Fileが、対象を特定でき、Target Declaration（対象宣言）との包含関係を判定できる形で示されている。

いずれかを満たさない場合、Rule Selection（規則選択）を解決できない。不足する内容を補完せず、不整合として報告する。不完全な規則集合を、正常な解決結果として保持・後続Phaseへ渡さない。

保持する3つのFileは、「Common Content（共通の内容）」と「Target-specific Result（結果）」の内容契約に従い、同一のMapping内でKeyを、同一のList内でRule ID（規則ID）またはSource Reference（Source参照）を重複させない場合に有効である。

### Target-specific Invalidation（利用停止）

対象Fileの結果は、次のいずれかに該当する場合、その対象File単位でInvalidated（利用停止）となる。

- 当該 `inputs.yaml` に記録されたSourceが変更された。
- 記録されていないSourceの変更または追加が、当該結果に影響し得る。
- 用いたRepository-level Rule Resolution（Repository共通規則解決）の結果がInvalidated（利用停止）となった、または更新された。
- 上記に該当するか否かを判断できない。対応関係を確認できる `inputs.yaml` がない場合を含む。

## Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）

### Pre-resolution Position（位置づけ）

Applicability Pre-resolution and Candidate Composition（適用性事前解決と候補合成）は、対象FileのTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` の各Ruleについて、Not Applicable（非適用）を事前に判断し、残るRuleをCandidate Rule Set（候補規則集合）とする。

その結果は、最終的なRule Applicabilityの判定ではない。

### Pre-resolution Input（入力）

| 入力 | 用途 |
| --- | --- |
| 現在利用可能な対象FileのTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` | 判断の対象とするRule |
| 対象File | Target State（対象状態） |
| 判断に用いたRuleを定めるConvention Asset（規約資産） | 正式なApplicability Scope（適用範囲）とRule Statement（規則文） |
| 判断に必要な正式定義のSource | 対象Fileについての事実を成立させるDefinition Authority（定義権限）を持つ定義 |

Target-specific Rule Resolution（対象固有規則解決）の結果が利用不能である場合は、「Fallback Resolution（結果が利用不能な場合の解決）」に従う。

### Not-applicable Determination（非適用の判断）

Not-applicable Exclusion（非適用による除外）とするのは、正式なApplicability Scope（適用範囲）とRule Statement（規則文）、Target State（対象状態）、および必要な正式定義から、対象File全体についてNot Applicable（非適用）を十分確定したRuleに限られる。次を根拠としてRuleを除外しない。

- 不明または未確定であること
- 一部のSection（節）等についてのみNot Applicable（非適用）が成立すること
- 現在の作業で使用しなさそうであること
- Ruleが対象とする表現またはDevelopment Action（開発行為）が、現在存在しないこと
- Path・名称だけから推測した対象Fileの意味
- Development Action（開発行為）を対象とするRuleが、File本文に対するRuleではないこと

現在存在しない表現またはDevelopment Action（開発行為）については、対象Fileの責務の範囲内で成立し得るものと、対象Fileの責務の変更を要するものとを区別する。前者を対象とするRuleは、その不在だけを根拠として除外しない。後者の成立可能性は、Ruleを候補として残す根拠としない。別の文書種別への転換、または別のFileの変更を、対象Fileについて自動的に想定しない。いずれに当たるかが不明または未確定であるRuleは、Candidate Rule Set（候補規則集合）へ残す。この候補保持は、当該RuleのRule Applicabilityが現在成立することを意味しない。

Repository共通のDevelopment Action（開発行為）を対象とするRuleは、そのDevelopment Action（開発行為）が現在発生していないこと、対象File本文に対するRuleではないこと、または対象Fileがその結果の表示先ではないことだけを理由として、対象FileのCandidate Rule Set（候補規則集合）から除外しない。一方、Development Action（開発行為）を対象とすることだけを理由として、正式なApplicability Scope（適用範囲）が定める限定を無視しない。

### Pre-resolution Result（結果）

結果は、本Supportを保持するRepositoryの次のPhysical Location（物理配置）に、3つのFileとして保持する。

```text
.ai/resolution-support/rule-applicability/candidate-rules/<対象FileのRepository相対Path>/
├─ rules.yaml
├─ excluded.yaml
└─ inputs.yaml
```

| File | 保持する内容 |
| --- | --- |
| `rules.yaml` | Candidate Rule Set（候補規則集合） |
| `excluded.yaml` | Not-applicable Exclusion（非適用による除外）としたRule |
| `inputs.yaml` | 対応する解決で直接使用した入力File |

- `rules.yaml` は、Target-specific Rule Resolution（対象固有規則解決）の `rules.yaml` のすべてのConvention Reference（規約参照）をKeyとして保持する。すべてのRuleが除外されたConvention（規約）の値は、空のList `[]` とする。
- `excluded.yaml` は、Not-applicable Exclusion（非適用による除外）としたRuleを持つConvention（規約）だけをKeyとして保持する。除外したRuleがない場合は、`conventions: {}` とする。
- 同一のConvention Reference（規約参照）が、`rules.yaml` と `excluded.yaml` の双方に現れてよい。
- 各Convention（規約）について、両一覧のRule ID（規則ID）は重ならず、その和集合はTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` の当該Convention（規約）のRule ID（規則ID）の一覧と一致する。Target-specific Rule Resolution（対象固有規則解決）が外したRuleを、いずれの一覧にも含めない。
- `inputs.yaml` には、用いたTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml`、対象File、および判断に直接使用したSourceを記録する。

### Pre-resolution Validation Conditions（検証条件）

用いるTarget-specific Rule Resolution（対象固有規則解決）の結果が現在利用可能である場合にのみ、結果を保持する。保持する3つのFileは、「Common Content（共通の内容）」と「Pre-resolution Result（結果）」の内容契約に従い、同一のMapping内でKeyを、同一のList内でRule ID（規則ID）またはSource Reference（Source参照）を重複させない場合に有効である。

### Pre-resolution Invalidation（利用停止）

対象Fileの結果は、次のいずれかに該当する場合、その対象File単位でInvalidated（利用停止）となる。

- 当該 `inputs.yaml` に記録されたSource、または対象Fileが変更された。
- 記録されていないSourceの変更または追加、あるいはTarget State（対象状態）の変更が、当該結果に影響し得る。
- 用いたTarget-specific Rule Resolution（対象固有規則解決）の結果がInvalidated（利用停止）となった、または更新された。
- 上記に該当するか否かを判断できない。対応関係を確認できる `inputs.yaml` がない場合を含む。

Invalidated（利用停止）である場合、当該対象Fileの現在のTarget-specific Rule Resolution（対象固有規則解決）の `rules.yaml` 全体を、Candidate Rule Set（候補規則集合）として用いることができる。

## Self Application（`.github`自身への適用）

`.github` も、本文書が定めるContract（契約）に従う。`.github` のためのModel上の例外を設けない。

`.github` がConsumer Repository（利用Repository）である場合、Foundation Provider（基盤提供主体）は当該Repository自身である。このとき、Convention Reference（規約参照）およびSource Reference（Source参照）は、`.github` のRepository root相対Pathとしてそのまま解決される。

## Deferred to Downstream Design（後続設計へ委譲する事項）

本文書は次を定義しない。ここで示す事項は、本文書の現在の責務に基づいて、意図的に定義・解決の対象外としている事項である。

- 本Supportが生成するDerived Output（派生出力）自身の扱い。
- Consumer Repository（利用Repository）におけるRule Catalog Resolution（規則一覧解決）の結果の保持・参照の方式。
- Foundation Provider（基盤提供主体）のRepository root以外を基準とする入力の参照方式、およびFoundation Provider（基盤提供主体）とConsumer Repository（利用Repository）が別のRepositoryである場合の入力の参照方式。
- 同一Phase・同一対象のFileの組が、同一の解決によるものであることを確認する具体的な方式。
- 対象FileとしてのRepository root・未作成の対象の扱い、およびPathの正規化方式。
- 変更検知機構、Generator、Hook、Skill、Agent / Workflow。
- 本Contract（契約）に対するValidation Tool、Enforcement、およびCI。
- AI Consumer（AI利用主体）によるResolution Result（解決結果）の利用方式、およびRouting。→ AI Consumption Workflowへ委譲する。

これらが未確定であることは、本文書のDesign Gap（設計上の不足）ではない。
