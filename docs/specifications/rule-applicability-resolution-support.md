# Rule Applicability Resolution Support Specification（規則適用解決補助仕様）

## Purpose（目的）

本文書は、`noxris42` において**Repository内のTarget File（対象File）ごとに、Normative Rule（規範的規則）のCandidate Rule Set（候補規則集合）をRepository-managed Derived Information（Repository管理の派生情報）として保持するRule Applicability Resolution Support（規則適用解決補助）について、そのConcrete Contract（具体契約）を定義する**Specification Asset（仕様資産）である。

本文書が扱う問いは次の5点である。

1. Rule Applicability Resolution Support（規則適用解決補助）は、既存のFoundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityに対して、どの位置を占めるのか。
2. Candidate Rule Set（候補規則集合）は、何から、どのように解決されるのか。
3. どのTarget File（対象File）について解決し、何を解決対象としないのか。
4. 解決結果は、どのPhysical Representation（物理表現）として保持されるのか。
5. 解決結果は、どのように生成・再生成され、Current Authoritative State（現在の正式状態）と整合した状態に保たれるのか。

本文書が定義するのは、この5点に対するConcrete Contract（具体契約）に限られる。本文書は、Rule ApplicabilityのSemantic Model（意味モデル）を定義しない。

## Relationships（関係）

本文書は[Repository Governance Documentation Framework](../architecture/repository-governance-documentation-framework.md)が定義するSpecifications Area（仕様領域）に属する通常のDocumentation Asset（文書資産）である。Rule Applicabilityの解決という特定Subjectについて、その解決を補助するDerived Information（派生情報）を生成・保持可能にするConcrete Contract（具体契約）として成立する。AreaまたはFramework（体系）を代表・集約するAssetではない。

Rule Applicability Resolution Support（規則適用解決補助）のConcrete Contract（具体契約）、すなわちTarget-specific Applicability Pre-resolution（対象固有適用性事前解決）の結果の扱い、Resolution Target（解決対象）のCoverage（網羅）、Target Shard（対象Shard）のPhysical Representation（物理表現）、および生成についてのDefinition Authority（定義権限）は本文書が持つ。

### Responsibility Boundary（責務境界）

本文書が使用する次のConcept（概念）のDefinition Authority（定義権限）は本文書の外にある。本文書はこれらを参照するのみで、再定義・上書きしない。

- Foundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityの意味と、三者の境界
- Convention（規約）、Normative Rule（規範的規則）、Rule Identity（規則同一性）、およびRule ApplicabilityがRule Statement（規則文）の規定する対象・条件から定まること
- Rule ID（規則ID）およびConvention Code（規約コード）の形式
- Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）、Resolved Rule Selection（解決済み規則選択）、およびEffective Foundation State（有効基盤状態）の具体的な構成と導出
- Foundation Provider（基盤提供主体）・Consumer Repository（利用Repository）・AI Consumer（AI利用主体）の間のResponsibility Relationship（責務関係）

したがって次は本文書の責務ではない。

- Foundation ApplicationおよびTarget-specific Rule Selection（対象固有規則選択）の意味と境界。→ [Repository Governance](../architecture/repository-governance.md)による。
- Rule Applicabilityの意味。→ [Convention Architecture](../architecture/convention.md)による。
- 各Normative Rule（規範的規則）のRule Applicability。→ 当該Normative Rule（規範的規則）のRule Statement（規則文）による。
- Rule ID（規則ID）およびConvention Code（規約コード）の形式。→ [Convention Authoring Convention](../conventions/convention-authoring.md)による。
- Target-specific Rule Selection（対象固有規則選択）の宣言・解決、およびEffective Foundation State（有効基盤状態）の導出。→ [Foundation Application State Specification](foundation-application-state.md)による。
- AI Integration（AI連携）がEffective Foundation State（有効基盤状態）およびDerived Information（派生情報）を参照・利用する責務。→ [AI Integration Architecture](../architecture/ai-integration.md)による。

本文書が定めるのは、これらによってすでに成立しているModelと解決結果を前提として、Target File（対象File）ごとのCandidate Rule Set（候補規則集合）をどのように解決・保持するかである。

### Position（設計上の位置づけ）

本文書は、[Convention Architecture](../architecture/convention.md)、[Repository Governance](../architecture/repository-governance.md)、および[Foundation Application State Specification](foundation-application-state.md)を前提とする。

Rule Applicability Resolution Support（規則適用解決補助）は、[Foundation Application State Specification](foundation-application-state.md)が定める解決の結果を入力として利用し、その後段で、各Normative Rule（規範的規則）のRule Statement（規則文）に照らしてTarget File（対象File）ごとの候補を絞り込む。本文書はいずれのSourceもRefinement（具体化）しない。

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
- Target-specific Effective Rule Set（対象固有有効規則集合）の参照
- Target-specific Applicability Pre-resolution（対象固有適用性事前解決）の結果と、Candidate Rule Set（候補規則集合）の成立
- Pre-resolution Unit（事前解決単位）とRuntime Applicability Unit（実行時適用単位）の境界
- Resolution Target（解決対象）のRepository Locality（Repository局所性）とCoverage（網羅）
- 自己再帰を防ぐStructural Boundary（構造境界）
- Target Shard（対象Shard）のPhysical Location（物理配置）、Path Mapping、および内容
- Canonical / Deterministic Generation（正規／決定論的生成）とFull Regeneration（完全再生成）
- Repositoryが本Supportを維持する責務

### Out of Scope（本文書が定義しない範囲）

- Foundation Application、Target-specific Rule Selection（対象固有規則選択）、およびRule Applicabilityの意味
- 各Normative Rule（規範的規則）のRule Applicability、およびその判断内容
- Target-specific Rule Selection（対象固有規則選択）の宣言・解決方式
- Target Shard（対象Shard）の実体、およびその生成を行うGenerator・Script
- 変更検知、Regeneration Trigger、Hook、Skill、Agent / Workflow、CI / Enforcement
- Partial Regeneration、およびSemantic Impactの事前判定
- AI Consumer（AI利用主体）によるTarget Shard（対象Shard）の利用方式、およびRouting
- 本Supportが生成するDerived Output（派生出力）自身へのConvention（規約）およびRuleの適用判断

## Position of Support（補助の位置づけ）

### Derived Information（派生情報）

Rule Applicability Resolution Support（規則適用解決補助）は、Current Authoritative State（現在の正式状態）から導出され、Repositoryが管理するDerived Information（派生情報）である。Current Authoritative State（現在の正式状態）とは、次の現在の内容である。

- Foundation Application State（基盤適用状態）のDeclaration、およびそこから導出されるEffective Foundation State（有効基盤状態）
- 各Convention（規約）が定めるNormative Rule（規範的規則）とそのRule Statement（規則文）
- 各Target File（対象File）自身
- Target-specific Applicability Pre-resolution（対象固有適用性事前解決）に必要なConcept（概念）・Classification（分類）・Condition（条件）等のTarget-level Semantic Fact（対象レベル意味事実）について、Definition Authority（定義権限）を持つCurrent Authoritative Source（現在の正式Source）

たとえば、あるTarget File（対象File）がDocumentation Asset（文書資産）として成立するかという事実は、Target File（対象File）自身やRule Statement（規則文）ではなく、そのDefinition Authority（定義権限）を持つArchitecture（アーキテクチャ）・Specification（仕様）等から成立し得る。Current Authoritative State（現在の正式状態）が含むのは、Pre-resolutionに必要なTarget-level Semantic Fact（対象レベル意味事実）のDefinition Authority（定義権限）を持つSourceに限られる。Repository内のあらゆる情報を含むものではない。本文書は、これらのSourceの固定一覧または分類を定めない。

Rule Applicability Resolution Support（規則適用解決補助）はSource of Truth（正本）ではない。その内容とCurrent Authoritative State（現在の正式状態）から導出される結果とが一致しない場合、成立している内容はCurrent Authoritative State（現在の正式状態）側である。

### Authority Boundary（権限の境界）

Rule Applicability Resolution Support（規則適用解決補助）は、Foundation Application、Target-specific Rule Selection（対象固有規則選択）、Rule Applicability、およびNormative Rule（規範的規則）のいずれも定義・変更・上書きしない。

```text
Rule Applicability Resolution Support
  derives from
Current Authoritative State

Rule Applicability Resolution Support
  does not define
Foundation Application / Target-specific Rule Selection / Rule Applicability
```

Rule ApplicabilityのDefinition Authority（定義権限）は、[Convention Architecture](../architecture/convention.md)および各Normative Rule（規範的規則）のRule Statement（規則文）に残る。

## Resolution Model（解決モデル）

### Target-specific Effective Rule Set（対象固有有効規則集合）

Target-specific Effective Rule Set（対象固有有効規則集合）は、あるTarget File（対象File）について、Resolved Repository-level Application State（解決済みRepositoryレベル適用状態）が `applied` である各Convention（規約）のResolved Rule Selection（解決済み規則選択）を合わせたRule Set（規則集合）である。

本文書は、その解決方式を新たに定めない。[Foundation Application State Specification](foundation-application-state.md)が定める解決の結果をそのまま用いる。

### Target-specific Applicability Pre-resolution（対象固有適用性事前解決）

Target-specific Applicability Pre-resolution（対象固有適用性事前解決）は、Target-specific Effective Rule Set（対象固有有効規則集合）の各Normative Rule（規範的規則）について、そのTarget File（対象File）に対するApplicabilityを、Current Authoritative State（現在の正式状態）から事前に判定することである。

判定結果は次の3つのいずれかであり、Candidate Rule Set（候補規則集合）への扱いは次のとおりである。

| 判定結果 | 意味 | Candidate Rule Set（候補規則集合） |
| --- | --- | --- |
| `False` | Current Authoritative State（現在の正式状態）とTarget-levelの状態から、当該Target File（対象File）についてNot Applicable（非適用）と確定できる | 除外する |
| `True` | Current Authoritative State（現在の正式状態）とTarget-levelの状態から、当該Target File（対象File）についてApplicableと確定できる | 残す |
| `Unknown` | Applicableか否かをCurrent Authoritative State（現在の正式状態）とTarget-levelの状態から確定できない | 残す |

判定は、各Normative Rule（規範的規則）のRule Statement（規則文）が規定する対象・条件に照らして行う。当該Target File（対象File）自身、その属性、または当該Target File（対象File）内に成立するObject・Representation（表現）がRule Statement（規則文）の対象となり得る場合、判定結果は `True` または `Unknown` となり得る。

当該Target File（対象File）が、Rule Statement（規則文）の対象である行為・判断の素材、入力、参照元、または結果の保持先となり得ることだけでは、当該Target File（対象File）についてApplicableとはならない。同様に、ある定義を参照・利用することだけでは、その定義を成立させるNormative Rule（規範的規則）が参照側のTarget File（対象File）についてApplicableとはならない。

```text
Target File is material / input / reference / storage for a ruled action
≠ Rule is applicable to the Target File
```

これらは新たな判定基準ではない。ApplicabilityがRule Statement（規則文）の規定する対象・条件から定まるという[Convention Architecture](../architecture/convention.md)の意味と、判定結果が当該Target File（対象File）についてのものであることを明確にするものである。

`False` とするのは、Not Applicable（非適用）が確定できる場合に限られる。確定できない場合は `Unknown` とする。

Current TargetにRule Statement（規則文）が対象とするRepresentation（表現）・Occurrenceが現在存在しないことだけでは、`False` としない。Taskによる当該Target File（対象File）自身の内容・表現・属性の変更の結果として、そのRepresentation（表現）・Occurrenceが当該Target File（対象File）内または当該Target File（対象File）自身について成立し得る場合、そのRuleは `Unknown` である。

```text
Current absence
≠ structural impossibility
```

ここでいう変更は、当該Target File（対象File）自身に対する変更に限られる。新規Fileの作成、Directoryの作成・改名、Commit、Candidate Recommendation（候補提案）、他のTarget File（対象File）の変更等、当該Target File（対象File）以外を対象とする作業は含まない。

### Candidate Rule Set（候補規則集合）

Candidate Rule Set（候補規則集合）は、Target-specific Effective Rule Set（対象固有有効規則集合）から、Target-specific Applicability Pre-resolution（対象固有適用性事前解決）が `False` としたNormative Rule（規範的規則）を除いたRule Set（規則集合）である。

```text
Candidate Rule Set
= Target-specific Effective Rule Set − { r | Pre-resolution(r) = False }
```

あるNormative Rule（規範的規則）がすべてのResolution Target（解決対象）について `False` となり、いずれのTarget Shard（対象Shard）にも現れないことは、正常な解決結果である。本SupportのResolution FailureまたはCoverageの不足を意味しない。

Candidate Rule Set（候補規則集合）は、Applicable Rule Set（適用規則集合）ではない。Candidate Rule Set（候補規則集合）に含まれることは、そのRuleがApplicableであること、またはNormative Effect（規範的効力）を持つことを意味しない。各RuleがApplicableであるかは、引き続きそのRule Statement（規則文）によって判定される。

```text
Candidate Rule Set
≠ Applicable Rule Set
```

Target-specific Applicability Pre-resolution（対象固有適用性事前解決）は、Target-specific Rule Selection（対象固有規則選択）ではない。前者はRule Applicabilityについての事前判定であり、後者が選択したRule Set（規則集合）を変更しない。

### Pre-resolution Unit and Runtime Applicability Unit（事前解決単位と実行時適用単位）

Target Shard（対象Shard）はPre-resolution Unit（事前解決単位）である。Runtime Applicability Unit（実行時適用単位）ではない。

Runtime Applicability Unit（実行時適用単位）は、各Rule Statement（規則文）が定める。File・Section・Representation（表現）・Occurrence・Usage・Development Action等、Rule Statement（規則文）が規定する単位を、本SupportはFile単位へ変更しない。

たとえば、Commit等、File Target（File対象）へ帰属しないDevelopment Action（開発行為）をRule Statement（規則文）の対象とするNormative Rule（規範的規則）は、Rule Statement（規則文）の対象がTarget File（対象File）自身・その属性・その内部に成立するObject・Representation（表現）のいずれでもないため、すべてのTarget File（対象File）について `False` となる。その結果、いずれのTarget Shard（対象Shard）にも現れない。これは「Target-specific Applicability Pre-resolution（対象固有適用性事前解決）」の判定から導かれる例であり、別の除外機構ではない。

## Resolution Target（解決対象）

### Repository Locality（Repository局所性）

Rule Applicability Resolution Support（規則適用解決補助）はRepository-localである。各Repositoryは、そのRepository自身のTarget File（対象File）について本Supportを生成する。

Foundation Provider（基盤提供主体）側のAuthoritative Source（正式Source）は、Resolution Source（解決Source）として用いられ得る。Consumer Repository（利用Repository）側のResolution Target（解決対象）にはしない。

### Complete Coverage（完全網羅）

Resolution Target（解決対象）は、当該RepositoryがVersion管理する各File、すなわちRepository-managed Target File（Repository管理対象File）である。ただし「Self-recursion Boundary（自己再帰の境界）」が定めるDerived Output（派生出力）を除く。

各Resolution Target（解決対象）について、Target Shard（対象Shard）を1つ生成する。Candidate Rule Set（候補規則集合）が空であっても、Target Shard（対象Shard）を生成する。

Complete Coverage（完全網羅）が要求するのはResolution Target（解決対象）の網羅である。各Normative Rule（規範的規則）がいずれかのTarget Shard（対象Shard）に現れることは要求しない。

Candidate Rule Set（候補規則集合）が空であることは、明示的な解決結果として次のとおり保持する。

```yaml
candidate_rules: {}
```

Target Shard（対象Shard）が存在しないことを、Candidate Rule Set（候補規則集合）が空であることとして扱わない。

```text
Target Shard absent
≠ candidate_rules: {}
```

### Self-recursion Boundary（自己再帰の境界）

Rule Applicability Resolution Support（規則適用解決補助）自身が生成したDerived Output（派生出力）は、Resolution Target（解決対象）としない。

これは、解決結果がさらに解決対象となる自己再帰を防ぐための、本Resolution Mechanism固有のStructural Boundary（構造境界）である。Convention（規約）のApplicabilityに対する例外ではない。

Derived Output（派生出力）自身に、どのConvention（規約）およびRuleがApplicableであるかは、Foundation ApplicationおよびRule Applicabilityによって定まる。本文書はこれを変更しない。

## Target Shard（対象Shard）

### Physical Location（物理配置）

Target Shard（対象Shard）は、次のPhysical Location（物理配置）に置く。

```text
Repository root
└─ .ai/
   └─ resolution-support/
      └─ rule-applicability/
         └─ targets/
```

`.ai/` 以下の配置は、本SupportのPhysical Location（物理配置）である。本文書は、これらのDirectoryに対して、Documentation Area（文書責務領域）その他のSemantic Responsibility（意味上の責務）を成立させない。

### Path Mapping（Pathの対応）

Resolution Target（解決対象）からTarget Shard（対象Shard）へのPath Mappingは次である。

```text
<repository-relative target path>
→ .ai/resolution-support/rule-applicability/targets/<repository-relative target path>.yaml
```

```text
AGENTS.md
→ .ai/resolution-support/rule-applicability/targets/AGENTS.md.yaml

docs/architecture/convention.md
→ .ai/resolution-support/rule-applicability/targets/docs/architecture/convention.md.yaml
```

Target File（対象File）のRepository root相対Pathは、名称を変換せずに保持し、末尾へ `.yaml` を追加する。

Target Shard（対象Shard）のPathのうち、Target File（対象File）に由来する部分は、Target Identity（対象同一性）を機械的に保持するRepresentation（表現）である。本Supportによる独立したPhysical Name（物理名称）の選択ではない。

`.ai/resolution-support/rule-applicability/targets/` までの、本Supportが所有する部分は、通常のRepository-controlled Physical Structure（物理構造）として扱う。

本文書は、[Naming Convention](../conventions/naming.md)のRuleおよびそのRule Applicabilityを変更しない。

### Content（内容）

Target Shard（対象Shard）のFile FormatはYAMLとする。意味構造は次である。

```yaml
candidate_rules:
  <convention-code>:
    - <rule-id>
```

```yaml
candidate_rules:
  MDK:
    - MDK-SF-003
    - MDK-SF-004
  WRT:
    - WRT-SF-001
```

| Field | 必須性 | Allowed Value | 意味 |
| --- | --- | --- | --- |
| `candidate_rules` | 必須 | Convention Code（規約コード）からRule ID（規則ID）のListへのMapping | 当該Target File（対象File）のCandidate Rule Set（候補規則集合） |

- Candidate Rule Set（候補規則集合）は、各Rule ID（規則ID）が属するConvention Code（規約コード）でGroupingする。このGroupingは、既存のRule ID（規則ID）およびConvention Code（規約コード）を用いたRetrieval Structure（取得構造）であり、新たなSemantic Classification（意味分類）ではない。
- Candidateを持たないConvention Code（規約コード）のGroupは出力しない。
- Candidate Rule Set（候補規則集合）全体が空である場合は、`candidate_rules: {}` とする。
- 同一のRule ID（規則ID）を重複させない。

Target Shard（対象Shard）は `candidate_rules` 以外のFieldを持たない。Target File（対象File）のIdentity（同一性）はTarget Shard（対象Shard）のPathが担うため、Target Fieldを持たない。Timestamp、Fingerprint、Generation Metadata、判定理由、およびSource一覧を保持しない。

## Generation（生成）

### Canonical / Deterministic Generation（正規／決定論的生成）

同一のSemantic Resolution Result（意味上の解決結果）からは、同一のPhysical Result（物理結果）が生成されなければならない。

- Convention Code（規約コード）のGroupは、Convention Code（規約コード）のbyte-wise ascendingに並べる。
- 各Group内のRule ID（規則ID）は、Rule ID（規則ID）のbyte-wise ascendingに並べる。

いずれの比較もLocaleに依存しない。

Indent、Quote、Document Marker等、Semantic Need（意味上の必要性）を持たないSerializationの詳細は本文書が固定しない。ただし、いずれの詳細を用いる場合も、同一のSemantic Resolution Result（意味上の解決結果）から同一のPhysical Result（物理結果）が生成されることを要する。

### Full Regeneration（完全再生成）

生成は、Full Regeneration（完全再生成）を基本とする。生成のたびに、次をCurrent Authoritative State（現在の正式状態）から解決し、すべてのTarget Shard（対象Shard）を再構成する。

1. Generation Input（生成入力）
2. 各Resolution Target（解決対象）のTarget-specific Effective Rule Set（対象固有有効規則集合）
3. 各Resolution Target（解決対象）のCandidate Rule Set（候補規則集合）

Generation Input Resolution（生成入力解決）は、生成時の一時的なIntermediate Step（中間段階）である。本Contract（契約）は、その結果を保持する永続的なResolution Support、Input Manifest、およびFingerprintを持たない。

Resolution Target（解決対象）の削除、またはResolution Target（解決対象）でなくなったことにより対応するTarget Shard（対象Shard）が不要となった場合、そのTarget Shard（対象Shard）は生成結果に含まれない。

### Maintenance Responsibility（維持責務）

Repositoryは、本Supportを、Current Authoritative State（現在の正式状態）と整合したCanonical Derived State（正規派生状態）として維持する責務を持つ。

本文書は、この責務を果たすための変更検知、Regeneration Trigger、およびその実行主体を定めない。

## Self Application（`.github`自身への適用）

`.github` も、本文書が定めるContract（契約）に従う。`.github` のためのModel上の例外を設けない。

`.github` がConsumer Repository（利用Repository）である場合、Foundation Provider（基盤提供主体）は当該Repository自身である。このとき `.github` がVersion管理するFileは、Foundation Provider（基盤提供主体）側のAuthoritative Source（正式Source）であることによってResolution Target（解決対象）から除かれない。`.github` 自身のRepository-managed Target File（Repository管理対象File）として、「Complete Coverage（完全網羅）」に従う。

## Deferred to Downstream Design（後続設計へ委譲する事項）

本文書は次を定義しない。ここで示す事項は、本文書の現在の責務に基づいて、意図的に定義・解決の対象外としている事項である。

- Target Shard（対象Shard）の実体生成、およびそれを行うGenerator・Script。
- 変更検知、Regeneration Trigger、Hook、Skill、Agent / Workflow。
- 本Contract（契約）に対するValidation Tool、Enforcement、およびCI。
- Partial Regeneration、Semantic Diff、Dependency Graph等の生成最適化。
- AI Consumer（AI利用主体）によるTarget Shard（対象Shard）の利用方式、およびRouting。→ AI Consumption Workflowへ委譲する。

これらが未確定であることは、本文書のDesign Gap（設計上の不足）ではない。
