# Notes — AI evaluation kinds

Working material accumulated during the project's seedling phase.

## 1. Strategic framing (2026-05-15)

Brett's strategic decision: not nine papers, not one paper that tries to settle all the AI-evaluation vocabulary at once. The first paper is a framework / typology paper, with three or four worked cases. Standalone papers on individual terms come later only where the HPC/Khalidi treatment changes an existing debate.

The framework paper's job is to show that AI evaluation and governance vocabulary contains *several kinds of kind-term*. The philosophical advance is the typology, not exhaustive treatment of any one label.

### Working title

> AI evaluation kinds are not definitions: HPC and causal-network structure in ML governance

(Re-title at polish; current title flags the move but is provisional.)

### Working thesis

AI evaluation and governance rely on kind-terms whose projectibility is often assumed but rarely analysed.

- Some, such as *hallucination* and *jailbreak*, pick out recurrent clusters of behaviour sustained by identifiable mechanisms.
- Others, such as *reasoning*, *agency*, and *emergence*, are capability-attribution terms whose projectibility depends on benchmark design, metric choice, architecture, training history, and deployment conditions.
- Still others, such as *alignment* and *trustworthiness*, are umbrella constructs that organise lower-level projectible kinds rather than naming unified kinds themselves.
- Bias sits at the edge: deployment-sensitive rather than model-internal.

Boyd's HPC theory explains why these terms need not have analytic definitions to be useful; Khalidi's nodes-in-causal-networks approach explains why the useful ones must have internal explanatory structure rather than merely recurring features. The typology lets us read AI-evaluation debates as disputes about which kind of kind-term is at issue, which is currently confused in the literature.

## 2. Typology of AI-evaluation kind-terms

Model-assisted survey (GPT-5.5 Pro, 2026-05-15).

| Cluster | Terms | Best treatment |
| ------- | ----- | -------------- |
| Output / behaviour failure kinds | *hallucination*, perhaps *bias* | Good HPC candidates: observable clusters with multiple sustaining mechanisms. |
| Adversarial / security kinds | *jailbreak*, *robustness* | Better Khalidian candidates: relational, adversarial, mechanism-sensitive nodes. |
| Capability-attribution kinds | *reasoning*, *agency*, *emergence* | Best treated together: the issue is whether benchmark performance licenses capability-kind attribution. |
| Governance umbrella kinds | *alignment*, *trustworthiness* | Probably not first-order HPC kinds; better treated as high-level regulatory or evaluative constructs that organise lower-level kinds. |

## 3. Worked cases (planned)

### Hallucination (output / behaviour failure)

Already has a large technical literature and multiple taxonomies, including distinctions among kinds of hallucination and accounts of contributing factors in LLMs. *Hallucination* is not well captured by a single essence such as "false output," because the relevant cluster involves factuality, faithfulness to source, unsupportedness, fluency, confidence, context of use, retrieval failure, training/evaluation incentives, and user uptake.

- Anchor reference: Huang et al. 2023 (arXiv:2311.05232) "A Survey on Hallucination in Large Language Models" — and the references therein.
- HPC angle: hallucination is not one phenomenon but a family of projectible failure patterns stabilised by training, decoding, retrieval, evaluation, source-use, uncertainty, and interactional context.
- Khalidian refinement: which features generate which others (e.g., decoding-temperature choices generate fluency-inflation effects that mask unsupportedness; evaluation-incentive choices generate the confidence-calibration profile; retrieval-failure modes generate the source-faithfulness profile).

### Jailbreak / robustness (adversarial / security kinds)

Already treated through taxonomies of attacks and defences, including black-box/white-box attacks and prompt-level/model-level defences.

- Anchor reference: Yi et al. 2024 (arXiv:2407.04295) "Jailbreak Attacks and Defenses Against Large Language Models: A Survey."
- Khalidian angle: *jailbreak* is not just a behaviour of the model. It is a relation among model policy, user goal, prompt strategy, safety training, interface constraints, adversarial adaptation, and institutional definition of prohibited output.
- Pair with *robustness* rather than isolate. The two are complementary: jailbreaks are the action-side, robustness the defensive-side, of the same adversarial-network structure.

### Reasoning / agency / emergence (capability-attribution kinds)

Best treated together. Shared problem: not "what is the cluster for each term?" but "when does benchmark performance justify a kind-attribution?"

- *Emergence*: Schaeffer, Miranda & Koyejo 2023 (arXiv:2304.15004) "Are Emergent Abilities of Large Language Models a Mirage?" — alleged emergent abilities may be artefacts of metric choice, not discontinuous changes.
- *Agency*: heavily tied to LLM-agent work; agentic systems characterised in terms of reasoning, acting, and interacting. Anchor: Plaat et al. 2025 (JAIR 84, article 29; DOI 10.1613/jair.1.18675; arXiv:2503.23037). Earlier notes had this as "Liu et al. 2025"; that was a source-identification error.
- *Reasoning*: embedded in benchmark design, prompting, tool use, training regimes, and interpretive disputes about whether behaviour reflects reasoning or merely performance on reasoning-shaped tasks. Huang and Chang 2023 give the survey frame; Mirzadeh et al. 2025 give a controlled mathematical-reasoning benchmark challenge.

Joint move: capability terms in AI are field-relative projectibility claims, not simple psychological attributions. Benchmark essentialism (passing a task cleanly reveals a capability-kind) is the target.

### Alignment / trustworthiness (umbrella constructs)

The alignment literature itself notes that there is no universally accepted definition; surveys treat it as an organising problem involving robustness, interpretability, controllability, and ethicality (alignmentsurvey.com 2023). NIST's AI RMF 1.0 treats *trustworthy AI* as an umbrella involving valid and reliable systems, safety, security and resilience, accountability and transparency, explainability and interpretability, privacy, and fairness with harmful bias managed.

- Treatment: not first-order HPC kinds. More like *health* or *fitness*: high-level evaluative constructs whose components are themselves better candidates for HPC/network treatment.
- Argument: *alignment* and *trustworthiness* are second-order regulatory constructs that coordinate lower-level projectible kinds (robustness failure, deception, hallucination, privacy leakage, unsafe compliance, discriminatory performance, adversarial vulnerability).
- Pressure case: sycophancy. Shapira et al. 2026 and Sharma et al. 2024 show why a behavior can be an apparent success relative to a preference-learning target while failing truthfulness or user welfare. This stays here; it is not a fourth worked case under the current scope decision.

### Bias (deployment-sensitive)

Already vast and taxonomy-heavy (e.g., Mehrabi et al. 2021 ACM Computing Surveys). A general "bias is an HPC kind" paper would disappear into that literature.

- Better narrow framing: *bias as a deployment-sensitive kind*, or *why algorithmic bias is not a property of models alone*. Causal-network treatment lets the model + data + deployment + user-feedback loop be the projectibility-relevant unit, not the model.
- Probably out of scope for the framework paper; held for a follow-up if it earns its keep.

## 4. Programme (papers in order)

1. **Framework / typology paper** (this project). Uses the whole set as motivating problem; develops three worked cases (*hallucination*; *jailbreak/robustness*; *reasoning/emergence/agency*); treats *alignment* and *trustworthiness* as umbrella constructs. Roughly 8,000–10,000 words.

2. *Hallucination as an HPC/network kind* (potential follow-up). The cleanest single-term spin-off.

3. *Capability attributions in AI evaluation* (potential follow-up). Puts *reasoning*, *agency*, *emergence* together. Target: benchmark essentialism.

4. *Alignment / trustworthiness as umbrella constructs* (potential follow-up). More philosophy of governance than philosophy of natural kinds. Possible co-author from a governance-oriented background.

## 5. Avoiding survey sprawl

A controlled comparative paper: enough terms to show the framework has scope, few enough worked examples to avoid survey sprawl. The temptation to treat *alignment*, *trustworthiness*, *bias*, and the rest at equal depth must be resisted in the framework paper — those are follow-up territory.

## 6. Relation to existing HPC corpus

- This project is a sister to `papers/Moral_act-kinds_as_nodes_in_causal-normative_networks/` — same Boyd/Khalidi framework applied to a different field-relative class of kinds.
- The AGI evaluation HPC paper (`papers/AGI_evaluation_HPC/`, arXiv:2510.15236) is a *predecessor* on AGI specifically. The new project's scope is broader (the typology of AI eval terms, with AGI as one possible umbrella construct or capability-attribution term).
- The pluralist-map paper (*What do we mean by language?*) shows the umbrella-vs-local-kind move done for a different concept; method here is a near cousin.
- Field-relative projectibility (per the moral-act-kinds notes §4) is the principal analytic tool.

## 7. Candidate venues

- *Minds and Machines* — natural fit for AI-evaluation philosophy work.
- *Philosophy & Technology* — broader scope, AI-governance friendly.
- *AI & Society* — more governance-policy; possible if the typology lands close to RMF-style frameworks.
- *Synthese* — Khalidi's own venue; could land there if the framework is sharp enough.
- *Studies in History and Philosophy of Science* — for a more methods-heavy version.

Decision deferred until draft is structured.

## 8. Source references (from the survey)

- Huang et al. 2023 — hallucination survey.
- Yi et al. 2024 — jailbreak attacks and defences survey.
- Schaeffer et al. 2023 — "emergent abilities are a mirage."
- Plaat et al. 2025 — agentic LLMs survey.
- Huang and Chang 2023 — reasoning in LLMs survey.
- Mirzadeh et al. 2025 — GSM-Symbolic and mathematical-reasoning benchmark fragility.
- Mehrabi et al. 2021 — bias/fairness in ML survey.
- alignmentsurvey.com 2023 — comprehensive alignment survey.
- NIST AI RMF 1.0 (2023) — trustworthy AI umbrella.
- Khalidi 2018 (*Synthese*) — nodes in causal networks.
- Khalidi 2013 — *Natural Categories and Human Kinds*.
- Boyd 1991 — homeostatic property clusters.

## 9. Weinberger 2026: stability vs control

Weinberger's "Homeostasis and causal control" should be part of the rewrite, not a side citation. The AI-evaluation version of the distinction is:

- benchmark reliability = stable score behaviour under specified conditions;
- construct validity = what the score means in the measured setting;
- projectibility = when the claim may travel across models, prompts, attacks, benchmarks, or governance uses;
- control/homeostasis = a stricter question about whether an evaluation regime corrects perturbations through monitoring, red-teaming, release gates, retraining, incident response, and policy enforcement.

This helps prevent the draft from saying that a benchmarked behaviour is "stable" and then treating that as a kind-making mechanism. A model family, benchmark suite, or governance term becomes control-like only when there is feedback-sensitive maintenance, not just repeated measurement.
