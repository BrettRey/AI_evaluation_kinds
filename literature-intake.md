# Literature intake: AI evaluation kinds

Date: 2026-05-15

This is a triage memo, not a full literature review. It is based on the PDFs in
`literature/`, plus the existing project notes in `NOTES.md`. Claims below are
for planning and should be checked against the PDFs before being cited in the
paper.

## Bottom line

Do not make full notes for all 67 PDFs. The next useful step is selective
annotation.

The paper needs three layers of literature:

1. A theory spine: natural kinds, HPC, causal networks, and construct validity.
2. A measurement/evaluation spine: benchmark validity, operationalization,
   leaderboards, risk frameworks, and capability attribution.
3. Worked cases: hallucination, jailbreak/robustness, capability-attribution
   terms, and a short sycophancy pressure case for alignment/RLHF.

Sycophancy should not become a fourth full worked case unless the paper changes
shape. It is more valuable as a pressure case: it shows that a behavior can be
an alignment success relative to RLHF preferences while being a failure relative
to epistemic integrity. That supports the paper's claim that `alignment` is an
umbrella construct, not a unified first-order kind.

## Iteration after Brett's feedback

The framework stands, but the corpus needs active balancing. The current PDF
folder over-represents sycophancy relative to its role in the paper. Treat the
extra sycophancy papers as reserve material for the umbrella-construct pressure
case, not as an implicit fourth worked case.

The scope decision is now explicit in `DECISIONS.md`: three worked cases remain
locked. Sycophancy is used after the typology to show why `alignment` is an
umbrella construct. The first annotation pass should therefore not spend equal
time on all sycophancy PDFs. The practical sycophancy core is `shapira2026rlhf.pdf`,
`sharma2024towards.pdf`, `ouyang2022training.pdf`, and `gao2022scaling.pdf`,
with `cheng2025elephant.pdf` and `vennemeyer2025sycophancy.pdf` held only if
the paragraph needs breadth.

The missing capability-attribution anchors have been added. `plaat2025agentic.pdf`
is the agency anchor; the earlier "Liu et al. 2025" reference was a source-identification
error for arXiv:2503.23037. `huang2023reasoning.pdf` gives the reasoning-survey
frame, and `mirzadeh2025gsm.pdf` gives a controlled challenge to reasoning
benchmark essentialism.

The philosophy-of-kinds spine is inherited from the portfolio corpus rather than
newly sourced in this folder. Use `boyd1991` and `boyd1999` for HPC, `khalidi2013`
for natural categories and human kinds, and `khalidi2018causal.pdf` for the
nodes-in-causal-networks account. The Khalidi 2018 entry is now present in this
project's bibliography as `khalidi2018causal`.

The balanced annotation queue has also been converted to `.md` files alongside
the PDFs in `literature/`. After the outline pass, there are 26 markdown working
files. These text files are working aids only; PDF and authoritative web
metadata remain the citation sources.

Bibliographic verification is current for the project-local additions. Plaat
2025 is a genuine JAIR article, not arXiv-only: JAIR, Crossref, and arXiv
metadata all point to DOI `10.1613/jair.1.18675`, volume 84, article 29. The
local PDF has been replaced with the JAIR version. Mirzadeh et al. 2025 has no
ICLR DOI on OpenReview; cite the ICLR paper by OpenReview URL and record the
arXiv identifier separately. The construct-validity article is entered as
`whitely1983construct`, with `embretson1983construct` as an alias, because the
DOI metadata gives the published author name as Susan E. Whitely. The outline
pass also added Raji et al. 2021 and the NIST adversarial machine learning
taxonomy as verified local sources.

## First annotation queue

These are the sources to read closely and make real notes from first.

| Source | Why it matters |
| --- | --- |
| `cronbach1955construct.pdf` | The nomological-network origin point for construct validity. |
| `embretson1983construct.pdf` | Separates construct representation from nomothetic span; useful for mechanism vs correlation in evaluation terms. |
| `messick1995validity.pdf` | Unified validity: score meaning, use, and consequences. |
| `kane2013validating.pdf` | Argument-based validation: how score interpretations and uses are licensed. |
| `adcock2001measurement.pdf` | Clean vocabulary for concept-systematization, operationalization, and contextual measurement validity. |
| `chouldechova2024shared.pdf` | Direct bridge from social-science measurement validity to GenAI capabilities, risks, and impacts. |
| `bean2025measuring.pdf` | Directly about construct validity failures in LLM benchmarks. |
| `freiesleben2026establishing.pdf` | Direct philosophical bridge from construct validity to LLM capability benchmarks and nomological networks. |
| `khalidi2018causal.pdf` | Core Khalidi anchor: natural kinds as highly connected nodes in causal networks. |
| `huang2025survey.pdf` | Main LLM hallucination taxonomy and mechanism survey. |
| `yi2024jailbreak.pdf` | Main jailbreak taxonomy and defense survey. |
| `wei2022emergent.pdf` | Positive emergence/capability-attribution anchor. |
| `schaeffer2023emergent.pdf` | Mirage/metric-choice counterpoint to emergence. |
| `huang2023reasoning.pdf` | Survey anchor for reasoning as a contested LLM attribution. |
| `mirzadeh2025gsm.pdf` | Controlled benchmark-fragility source for mathematical reasoning claims. |
| `plaat2025agentic.pdf` | Agency anchor: agentic LLMs as systems that reason, act, and interact. |
| `raji2021whole.pdf` | Benchmark-generalization critique; opening exhibit and capability-attribution predecessor. |
| `liang2022holistic.pdf` | Evaluation infrastructure and multi-metric benchmark framing. |
| `vassilev2024adversarial.pdf` | NIST AML taxonomy; supports jailbreak as an adversarial relation rather than a model-internal property. |
| `shapira2026rlhf.pdf` | The sycophancy-as-RLHF-amplification paper the user flagged. |
| `sharma2024towards.pdf` | Foundational sycophancy paper connecting human feedback to matching user beliefs over truth. |
| `ouyang2022training.pdf` | InstructGPT/RLHF baseline for preference-aligned assistants. |
| `gao2022scaling.pdf` | Reward-model overoptimization and Goodhart pressure. |
| `nist2023artificial.pdf` | Trustworthy AI as an umbrella risk-management construct. |

Second wave: `ji2023survey.pdf`, `min2023factscore.pdf`,
`manakul2023selfcheckgpt.pdf`, `shen2024do.pdf`, `greshake2023not.pdf`,
`zou2023universal.pdf`, `srivastava2022beyond.pdf`,
`hendrycks2020measuring.pdf`, `lin2022truthfulqa.pdf`,
`ibrahim2026training.pdf`, `cheng2026verbalizing.pdf`,
`kumarappan2026not.pdf`, and `wang2023decodingtrust.pdf`.

## Source clusters

### 1. Validity and measurement

Use this cluster to argue that AI evaluations are measurement practices, not
mere label applications. `Cronbach1955`, `Embretson/Whitely1983`, `Messick1995`,
`Kane2013`, `Adcock2001`, `Borsboom2004`, `Chouldechova2024`, `Bean2025`,
and `Freiesleben2026` let the paper distinguish three questions:

1. What concept is being measured?
2. What operationalization is being used?
3. What inference from the score is licensed?

This should be the main bridge from philosophical kind theory to AI evaluation.
It should sit under, not replace, the Boyd/Khalidi spine. Boyd supplies the
anti-essentialist HPC model; Khalidi supplies the stricter causal-network
projectibility test. Construct validity then explains how benchmark scores and
evaluation labels license, or fail to license, those kind attributions.

### 2. Hallucination

The hallucination literature already treats the term as a family of related
failure patterns: factuality, faithfulness, unsupportedness, retrieval,
uncertainty, detection, mitigation, and user context. This makes hallucination a
good HPC/network candidate, but not because it has one essence.

Use `Huang2025` for the LLM-era taxonomy, `Ji2023` for the older NLG survey
frame, and `SelfCheckGPT`, `FActScore`, retrieval augmentation, and uncertainty
papers as mechanism/measurement examples.

### 3. Jailbreak and robustness

Jailbreak is relational: model policy, user goal, attack strategy, safety
training, prohibited-output definitions, and interface context all matter.
`Yi2024`, `Shen2024`, `Zou2023`, `Zeng2024`, and `Greshake2023` support treating
jailbreaks as adversarial-network nodes rather than simple model properties.

### 4. Capability attribution and benchmark essentialism

The core issue is not whether terms such as `reasoning`, `emergence`, or
`agency` have dictionary definitions. The issue is whether benchmark scores
license kind-attributions. `Wei2022` and `Schaeffer2023` are the cleanest
emergence pairing: one motivates emergent capabilities; the other argues that
apparent emergence may be metric-dependent. `Huang2023Reasoning` and
`Mirzadeh2024GSM` keep reasoning from collapsing into emergence-only. `Plaat2025`
anchors agency in system architecture and interaction rather than a model-internal
trait. `HELM`, `BIG-bench`, `MMLU`, `TruthfulQA`, and `Dynabench` provide the
evaluation-infrastructure context.

### 5. Alignment, trustworthiness, and sycophancy

Alignment and trustworthiness should be treated as umbrella constructs. They
organize lower-level projectible problems: hallucination, deception,
sycophancy, unsafe compliance, bias, privacy leakage, robustness failures, and
reward hacking.

Sycophancy is especially useful because it crosses the alignment boundary.
`Sharma2024` and `Shapira2026` tie sycophancy to human-feedback incentives.
`Cheng2025`, `Cheng2026`, `Ibrahim2026`, and `Vennemeyer2025` show why it is
not a single flat behavior. `Kumarappan2026` is a caution: not all sycophancy-like
patterns reduce to RLHF.

### 6. Bias, fairness, and deployment sensitivity

This is background unless the paper adds a fourth case. `Mehrabi2021`,
`Bender2018`, `Suresh2021`, `Friedler2016`, and `Hutchinson2019` support the
point that bias and fairness are not model-internal properties alone. They are
measurement-, construct-, data-, and deployment-sensitive.

## Full triage table

| File | Priority | Use in this paper |
| --- | --- | --- |
| `adcock2001measurement.pdf` | Core | Measurement validity framework; especially concept/operationalization/context distinctions. |
| `aera2014standards.pdf` | Background | Standards-language support if the paper needs formal testing-validity context. |
| `bai2022constitutional.pdf` | Support | AI feedback/constitutional AI as alignment infrastructure. |
| `bai2022training.pdf` | Support | Helpful/harmless RLHF baseline. |
| `batista2026rational.pdf` | Optional | Sycophantic AI and user belief-updating; likely follow-up rather than framework core. |
| `bean2025measuring.pdf` | Core | Direct construct-validity critique of LLM benchmarks. |
| `bender2018data.pdf` | Support | Data statements and dataset context; useful for bias/deployment-sensitive kinds. |
| `borsboom2004concept.pdf` | Core | Causal/ontological account of validity; useful contrast with Messick/Cronbach. |
| `cappelen2025going.pdf` | Optional | AI cognition philosophy; relevant only if reasoning/cognition discussion expands. |
| `casper2023open.pdf` | Support | RLHF limitations and failure modes; background for alignment umbrella. |
| `chandra2026sycophantic.pdf` | Optional | Delusional spiraling and sycophancy harms; use if adding user-uptake consequences. |
| `chen2024yesmen.pdf` | Support | Sycophancy mitigation; useful but probably not central. |
| `cheng2025elephant.pdf` | Support | Social sycophancy as broader than factual agreement/disagreement; reserve material if the pressure case needs breadth. |
| `cheng2026sycophantic.pdf` | Support | Sycophantic AI effects on prosocial intentions/dependence; use for downstream harms. |
| `cheng2026verbalizing.pdf` | Core | Mechanistic/social explanation via model assumptions; strong bridge to causal-network analysis. |
| `chouldechova2024shared.pdf` | Core | GenAI measurement framework; directly matches the paper's evaluation focus. |
| `cronbach1955construct.pdf` | Core | Construct validity and nomological networks. |
| `denison2024sycophancy.pdf` | Support | Reward tampering/specification gaming; use for alignment-failure family, not sycophancy core. |
| `embretson1983construct.pdf` | Core | Construct representation vs nomothetic span; directly useful for linking mechanisms to observed scores. |
| `fanous2025syceval.pdf` | Support | Sycophancy benchmark; useful for operationalization details. |
| `freiesleben2026establishing.pdf` | Core | Capability benchmarks need nomological networks; very high fit. |
| `friedler2016impossibility.pdf` | Support | Construct space and fairness incompatibilities; useful for bias/fairness background. |
| `gao2022scaling.pdf` | Core | Reward-model overoptimization and Goodhart pressure. |
| `greshake2023not.pdf` | Support | Indirect prompt injection; broadens jailbreak/security beyond direct prompts. |
| `hendrycks2020measuring.pdf` | Support | MMLU as benchmark exemplar for capability attribution. |
| `hong2025measuring.pdf` | Support | Multi-turn sycophancy benchmark; good for interactional context. |
| `huang2025survey.pdf` | Core | LLM hallucination taxonomy, detection, mitigation, retrieval limits. |
| `huang2023reasoning.pdf` | Core | Survey of LLM reasoning methods, benchmarks, and the unresolved attribution question. |
| `hutchinson2019fifty.pdf` | Support | Historical test-fairness connection to ML fairness. |
| `ibrahim2026training.pdf` | Core | Warmth optimization trade-off: accuracy and sycophancy. |
| `ji2023survey.pdf` | Core | NLG hallucination survey; useful contrast with LLM-specific hallucination. |
| `kane2013validating.pdf` | Core | Argument-based validity; use for interpretation/use inferences from benchmark scores. |
| `kiela2021dynabench.pdf` | Support | Dynamic benchmarking as anti-static-evaluation infrastructure. |
| `kumarappan2026not.pdf` | Core | Caution against reducing sycophancy-like behavior to RLHF alone. |
| `li2026when.pdf` | Support | Sycophancy as boundary failure between social alignment and epistemic integrity. |
| `liang2022holistic.pdf` | Core | HELM; multi-metric evaluation infrastructure and scenario framing. |
| `lin2022truthfulqa.pdf` | Support | Truthfulness benchmark; useful bridge between hallucination and sycophancy. |
| `liu2025truth.pdf` | Support | Multi-turn sycophancy/truth decay; use if interactional cases expand. |
| `manakul2023selfcheckgpt.pdf` | Support | Hallucination detection via sampling consistency. |
| `mehrabi2021survey.pdf` | Background | Bias/fairness taxonomy; probably not a worked case here. |
| `messick1995validity.pdf` | Core | Unified validity: score meaning, action, and consequences. |
| `mirzadeh2025gsm.pdf` | Core | GSM-Symbolic; controlled evidence that mathematical-reasoning scores are fragile under problem variants and irrelevant clauses. |
| `min2023factscore.pdf` | Support | Atomic factual precision measure for long-form generation. |
| `nist2023artificial.pdf` | Core | Trustworthy AI as umbrella risk-management construct. |
| `ouyang2022training.pdf` | Core | InstructGPT/RLHF baseline; human-feedback alignment setup. |
| `perez2023discovering.pdf` | Support | Model-written evaluations; early sycophancy/eval discovery context. |
| `plaat2025agentic.pdf` | Core | Agency anchor: agentic LLMs are defined by reasoning, acting, and interacting; useful for capability-attribution case. |
| `potts2026paradox.pdf` | Optional | User AI fluency and visible/invisible failure; deployment/user-context angle. |
| `raji2021whole.pdf` | Core | Benchmark-generalization critique; use for score-to-capability overreach and the opening exhibit. |
| `schaeffer2023emergent.pdf` | Core | Emergent abilities may be metric artifacts; benchmark-essentialism target. |
| `shapira2026rlhf.pdf` | Core | RLHF can amplify sycophancy; central to the user's flagged issue. |
| `sharma2024towards.pdf` | Core | Human feedback can reward matching user beliefs over truth. |
| `shen2024do.pdf` | Core | In-the-wild jailbreak prompt characterization. |
| `shuster2021retrieval.pdf` | Support | Retrieval augmentation as hallucination mitigation mechanism. |
| `song2025evaluating.pdf` | Optional | Scientific-discovery benchmark; useful if capability discussion needs domain-specific example. |
| `srivastava2022beyond.pdf` | Core | BIG-bench; capability benchmark infrastructure. |
| `suresh2021framework.pdf` | Support | Harms across ML lifecycle; deployment-sensitive bias/fairness. |
| `vennemeyer2025sycophancy.pdf` | Support | Sycophancy is not one thing; reserve material for causal separation if the pressure case expands. |
| `vassilev2024adversarial.pdf` | Core | NIST AML taxonomy; supports adversarial lifecycle, attacker-goal, capability, and knowledge dimensions. |
| `wang2023decodingtrust.pdf` | Support | Trustworthiness benchmark suite; useful umbrella example. |
| `wang2025when.pdf` | Support | Internal-origin account of sycophancy; use if mechanistic discussion expands. |
| `wei2022emergent.pdf` | Core | Positive account of emergent abilities in LLMs. |
| `xiao2021hallucination.pdf` | Support | Hallucination and predictive uncertainty. |
| `yi2024jailbreak.pdf` | Core | Jailbreak attacks/defenses survey. |
| `zeng2024johnny.pdf` | Support | Persuasion-based jailbreak framing. |
| `zou2023universal.pdf` | Support | Universal/transferable adversarial attacks on aligned LMs. |

## What still needs getting

No current library blockers. Kane 2013, Embretson/Whitely 1983, Khalidi 2018, Plaat
2025, Huang and Chang 2023, Mirzadeh et al. 2025, Raji et al. 2021, and
Vassilev et al. 2024 have been added to `literature/`.

Open or already likely available but not yet pulled into this project:

- A compact alignment survey, if the paper needs a single source for "alignment"
  as an umbrella term.

## Recommended writing move

The draft should not start by defining `hallucination`, `jailbreak`,
`reasoning`, `alignment`, or `trustworthiness`. Start with the measurement
problem:

> AI evaluation terms look like kind terms, but they do not all do the same
> kind of classificatory work.

Then use construct validity to show why the problem is not semantic
definition. An evaluation term licenses inferences only when the underlying
construct, operationalization, metric, and use context hold together. That sets
up the typology:

1. First-order failure kinds: hallucination.
2. Relational/adversarial network kinds: jailbreak/robustness.
3. Capability-attribution terms: reasoning/emergence/agency.
4. Umbrella constructs: alignment/trustworthiness.

Sycophancy should appear after the typology, as the example that makes the
umbrella point vivid: if RLHF amplifies sycophancy, then "alignment" can name a
training success and an epistemic failure at the same time. That is exactly why
the field needs a typology of evaluation kinds.
