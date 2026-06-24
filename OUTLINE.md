# Paper outline: AI evaluation kinds

**Working title.** *From Scores to Kinds: Projectibility and Validity in AI Evaluation* (provisional; supersedes "AI evaluation kinds are not definitions").

**Governing question.** Not "what kind of kind is each AI evaluation term?" but: what inferences does each AI evaluation term license, and what structure makes those inferences projectible?

**Thesis.** AI evaluation and governance vocabulary works by licensing inferences, from an observation (an output, an interaction, a score, an aggregate label) to a claim (about recurrence, vulnerability, capability, or governance). Different terms license different kinds of inference and carry different projectibility profiles: different conditions under which an inference may legitimately travel to another model, benchmark, attack, or deployment. Construct validity explains why that movement needs a construct, an operationalization, a metric, a population, and a use context. Boyd and Khalidi explain why some such terms are projectible without analytic definitions, because they pick out structured causal clusters, not mere recurring features. A four-way typology, classifying terms by their primary inferential role, lets the field re-read a class of confused debates as one profile mistaken for another.

**Scope and terminology.** The typology classifies each term by its *primary inferential role*, not by a metaphysical essence. Most terms carry secondary features of other types: hallucination has relational features, jailbreak culminates in an output failure, reasoning can be read as a capability, a benchmark construct, or an architectural property. The claim is about which inferential role does the main work, and which failure mode follows from misreading it.

**Length.** ~9,400 words. Framework paper, three worked cases, one pressure case.

**Central table (anchors §4):**

| Term type | Observation | Operationalization | Licensed inference | Projectibility payoff | Invalid inference | Use context |
|---|---|---|---|---|---|---|
| Output-centred failure profile | a generated output | factuality, faithfulness, support, uncertainty, granularity | this failure is likely to recur under specified mechanisms | predicts recurrence, detection, and mitigation transfer under similar generation/grounding conditions | treating *hallucination* as "false output" or treating one low score as deployment safety | model evaluation, RAG evaluation, user-facing factuality claims |
| Adversarial relation kind | an interaction crosses a boundary | attack distribution, policy category, evaluator, target system | this system is vulnerable under a specified adversarial network | predicts vulnerability and defense brittleness relative to attacker class, interface, and policy boundary | treating *jailbreak resistance* as a model property or projecting resistance across attacker classes | red-teaming, release gates, security evaluation |
| Capability-attribution term | task performance | benchmark, metric, item population, prompting/scaffold | this performance supports a capability claim over some domain | predicts transfer or robustness across item variants, metrics, scaffolds, and system boundaries when the capability claim is validated | treating a score as a capability or a benchmark as the domain | benchmark reporting, model comparison, deployment claims |
| Umbrella governance construct | an aggregate risk or value label | component taxonomy, governance use | lower-level constructs are being coordinated for a purpose | predicts which lower-level evaluations must travel together for a stated governance decision | treating *alignment* or *trustworthiness* as a first-order kind with a single score | procurement, audit, policy, release and risk-management decisions |

The diagnostic runs the same way for every case: observation → operationalization → licensed inference → projectibility → characteristic misanalysis.

---

## 1  Introduction: from scores to kinds  (~900 words)

**1.1 The recurring failure.** AI evaluation discourse repeatedly slides from a label to a score to a property: "the model reasons," "the model is aligned," "the model is jailbreak-resistant," "it hallucinates less." Opening exhibit: the emergence dispute. Wei 2022 treats discontinuous benchmark jumps as evidence of emergent abilities; Schaeffer 2023 shows that some of the apparent discontinuity can be produced by metric choice. Run this as a dispute over which inference a score licenses, not as a dispute over whether models have capabilities at all. Use Raji 2021 immediately after as the broader benchmark-generalization critique.

**1.2 The diagnosis.** The problem is not vague language. It is an inferential problem: each phrase licenses a move from an observation to a claim, and the moves are not the same kind of move. Three recurring bad inferences: score → capability, label → model property, benchmark result → governance conclusion. "Define X, then measure X" misreads what the terms do.

**1.3 Thesis.** Evaluation terms are inference licences with distinct projectibility profiles; a four-way typology, by primary inferential role, sorts them.

**1.4 Contribution, and what it is not.** Not a survey, and not a construct-validity complaint restated. Boyd and Khalidi add what validity alone cannot: an account of when a licensed inference may legitimately travel across models, benchmarks, attacks, and deployments.

**1.5 Roadmap.**

## 2  Evaluation terms as inference licences  (~1,100 words)

**2.1 The inference ladder.** Every evaluation term moves the reader up a ladder: observation/output → score/label → construct interpretation → kind attribution → governance or deployment use. Name each rung; the worked cases each climb it.

**2.2 What the movement requires: construct validity.** A score means something only relative to a construct, an operationalization, a metric, a population, and a use context. → Cronbach 1955; Messick 1995; Kane 2013; Adcock 2001; Embretson/Whitely 1983; Borsboom 2004.

**2.3 Construct validity in AI evaluation.** Evaluations are measurement practices, not label applications. → Chouldechova 2024 (measuring an amount of a concept in instances from a population; validity turns on concepts, contexts, metrics); Bean 2025 (systematic benchmark-validity review); Freiesleben 2026 (benchmark-to-capability attribution needs nomological networks).

**2.4 A note on which validity.** The validity literature is not one tradition: the consequentialist/nomological line (Messick) and the causal/ontological line (Borsboom) diverge. The paper leans causal-structural, because that coheres with the projectibility account in §3. Flag the choice; do not conflate the traditions.

**2.5 Valid comparison.** When does a score license ranking model A above model B, and when not? What invariance must hold across tasks, model families, languages, users, annotators, evaluator systems, and deployment settings? Comparison is where most governance inferences actually live.

**2.6 What validity leaves open.** Validity says when a score licenses a claim *here*. It does not say when the claim *projects* elsewhere, or who acts on it. Measurement practices co-evolve with benchmarks, communities, and standards; the label travels into releases, procurement, and audits. Keep construct validity subordinate: §3 supplies the projectibility account it points to.

## 3  Projectibility without essences  (~1,100 words)

**3.1 The question validity hands on.** When an evaluation term travels from one benchmark, model, policy, or deployment to another, what makes that travel legitimate?

**3.2 Boyd.** A category can support projection without an analytic definition: a property cluster held together by mechanisms. Anti-essentialism.

**3.3 Khalidi.** The stronger claim, and what validity alone cannot give. Projectible categories are not mere recurring labels or score aggregates; they have causal and explanatory structure, nodes in causal networks. → Khalidi 2018.

**3.4 The key contrast.** Not "definitions vs no definitions" but *mere recurring features vs structured, projectible clusters*. Present Boyd and Khalidi as jointly answering the projectibility question; do not stage a crisp "Boyd does the easy cases, Khalidi the hard ones" two-tier split, since the worked cases use both. → Boyd 1991, 1999; Khalidi 2018, 2013.

**3.5 Field-relative projectibility, defined.** Projection is always relative to a purpose and a domain. Define the term explicitly here, with a source; it is the paper's working tool, and the rest of the paper then uses it without re-arguing it.

**3.6 The vocabulary for the cases.** For each causal-network case the paper will specify central properties, derivative properties, and the recurrent processes that stabilise them. Mechanisms *explain* projectibility; they do not replace it.

## 4  A typology of AI evaluation terms  (~800 words)

**4.1 Classification by primary inferential role.** Present the central table. Each row is a distinct rung-pattern on the §2.1 ladder.

**4.2 Walk the rows.** For each: the observation, its operationalization, the inference it licenses, the misanalysis that follows from reading it as another type.

**4.3 Not essences, not exclusive bins.** A term can carry secondary features of other types; the typology claims only a dominant inferential role. The classification rule: a term's type is fixed by the inference its evaluations are actually used to license.

**4.4 The diagnostic.** Confused debates arise when one profile is mistaken for another. Preview the four cases.

## 5  Hallucination as an output-centred failure profile  (~1,300 words)

**5.1 Why "false output" fails.** The profile spans factuality, faithfulness to source, support and grounding, fluency, confidence, uncertainty, granularity, retrieval, task context, and user uptake. The literature's own taxonomy already treats it as plural (input-conflicting, context-conflicting, fact-conflicting). → Huang 2025; Ji 2023 (NLG-era contrast). Output-centred, but not purely first-order: source selection, context, retrieval, and uptake are relational. The label preserves the contrast with jailbreak without pretending hallucination is non-relational.

**5.2 The operational chain.** Construct (unsupported or unfaithful generation) → operationalizations (factuality, faithfulness, support, uncertainty, granularity) → metrics and probes → licensed claim. → Manakul 2023, Min 2023, Shuster 2021, Xiao 2021 as probes (probes, not mechanism proofs).

**5.3 Stabilising structure.** Central vs derivative properties; the recurrent processes (decoding, retrieval, training and evaluation incentives, uncertainty handling) that co-stabilise the profile. Treat a survey's mechanism-to-feature arrow as plausible-and-consistent, not established; flag where a primary source is needed.

**5.4 Projectibility paragraph.** Classifying hallucination as an output-centred failure profile lets us predict that the failure recurs under conditions C (specified decoding, retrieval, incentive regimes), explain why detection and mitigation transfer across those conditions, and refuse the inference that a low score on one benchmark projects to deployment. State the positive payoff, not just that a question "misfires."

## 6  Jailbreak as an adversarial relation  (~1,100 words)

**6.1 Not a model property.** Jailbreak is a relation: model policy, attacker strategy, interface and affordances, guardrail, evaluator, and the institutional definition of prohibited output. → Yi 2024, Shen 2024, Zou 2023, Zeng 2024, Greshake 2023; NIST adversarial ML taxonomy (organizes attacks by lifecycle stage, attacker goal, capability, and knowledge, not by a model-internal property).

**6.2 The operational chain.** Observation (an interaction crosses a policy boundary) → operationalization (attack distribution, policy category, evaluator, target system) → licensed inference ("this system is vulnerable under a specified adversarial network"). Central vs derivative properties; the recurrent attack/defence processes.

**6.3 Narrow the pairing.** Pair jailbreak with *jailbreak resistance*, not the polysemous *robustness* (adversarial, distributional, safety, refusal, tool-use, and deployment robustness diverge). Say explicitly that only the jailbreak-resistance region of robustness is in view.

**6.4 Projectibility paragraph.** A static benchmark measures a moving relational target; a jailbreak-resistance claim projects only relative to a specified adversary model. Classifying jailbreak as an adversarial relation lets us predict vulnerability under attacker class A and refuse the inference that resistance to A projects to attacker class B.

## 7  Reasoning, emergence, and agency as capability attributions  (~1,500 words)

**7.1 The shared inferential role, narrow target.** All three move from task performance to a capability claim. The target is benchmark essentialism: treating a score as a capability. → Raji et al. 2021 (the "whole wide world benchmark" critique) as predecessor. HELM is ally and foil: holistic evaluation is right to widen coverage, but it still needs a theory of which axes and metrics license which attribution. → Liang 2022.

**7.2 Reasoning (the main case): controlled variation.** Build the case on controlled variation, not survey assertion: GSM-Symbolic variants, irrelevant-clause distractors, clause-count sensitivity, and contamination. Each isolates a distinct score-to-capability failure (item-distribution fragility, prompt/scaffold fragility, train-test overlap). → Huang & Chang 2023 (survey frame); Mirzadeh 2025. Note: fragile measurement is compatible with genuine reasoning; the claim is about what the score licenses, not a verdict on AI cognition. Positive standard: a reasoning attribution becomes more projectible when performance is stable across semantically equivalent variants, irrelevant distractors, difficulty gradients, prompt/scaffold changes, and independently generated item populations, and when failure modes are explained rather than hidden by aggregate accuracy.

**7.3 Emergence (the metric-dependence case).** → Wei 2022 vs Schaeffer 2023. Scope the mirage argument precisely: it concerns metric choice (continuous/linear vs thresholded/discontinuous scoring), not general scepticism about capabilities. Positive standard: an emergence attribution becomes more projectible when the transition survives alternative metrics, task decompositions, and scaling analyses, rather than appearing only under thresholded or discontinuous scoring.

**7.4 Agency (the architecture and system-boundary case).** → Plaat 2025. Agency attributions track system architecture and the model-tool-environment boundary, not a model-internal trait; the attribution depends on where the system boundary is drawn. Positive standard: an agency attribution becomes more projectible when goal-directed behavior is robust across tool availability, feedback, environment variation, autonomy level, and task horizon, not merely when a passive language model succeeds on isolated QA items.

**7.5 The joint structure, earned.** What makes these one type is a shared inferential role with three distinct failure routes (metric choice; surface and item fragility; system-boundary dependence). Construct validity diagnoses; field-relative projectibility says what the attribution may travel to. → Srivastava 2022, Hendrycks 2020, Kiela 2021 as infrastructure context.

**7.6 Projectibility paragraph.** "Does the model reason?" resolves into: which capability claim, licensed by which operationalization, projectible to which domain, under which contamination and scaffold conditions. The constructive payoff is not scepticism but calibrated attribution: a capability term becomes useful when it predicts transfer, robustness, and failure boundaries better than the benchmark score alone.

## 8  Alignment and trustworthiness as umbrella governance constructs  (~1,000 words)

**8.1 Not first-order kinds.** Aggregate labels that coordinate lower-level constructs for a governance purpose, more like *health* or *fitness* than like a single kind. → NIST 2023 (the AI RMF builds trustworthiness considerations into design, development, use, and evaluation).

**8.2 The inference is coordinative.** The licensed inference is not classificatory but coordinative: the label signals that a set of lower-level constructs is being managed together for a stated use. Failure mode: treating *alignment* or *trustworthiness* as a first-order kind with its own cluster.

**8.3 The polysemy of *alignment*.** Reward-model alignment, instruction-following, user-preference alignment, value alignment, policy compliance, socio-technical governance. The umbrella reading explains the polysemy instead of explaining it away.

**8.4 Sycophancy, the pressure case (~600–800 words).** One behaviour: a success against the preference-learning target, a failure against truthfulness. → Sharma 2024, Shapira 2026; Ouyang 2022, Gao 2022 for the mechanism. The payoff: "is sycophancy a misalignment?" is a disguised question about which construct *alignment* is indexed to. Hold this to a pressure case; do not let it become a fourth worked case.

**8.5 Projectibility paragraph.** Umbrella constructs are projectible in a coordinative sense. They do not predict one first-order behavioral cluster; they predict which lower-level constructs must be evaluated together for a stated governance decision. Calling a system *trustworthy* should license expectations about the bundled management of validity, reliability, safety, security, accountability, transparency, privacy, and fairness under a specified use. Calling a system *aligned* should specify which lower-level alignment target is in view and block projection to incompatible targets. The invalid inference is from a local success on one component, such as user preference or refusal behavior, to the umbrella claim.

## 9  Conclusion: evaluation vocabulary is not one kind of thing  (~600 words)

**9.1 Recap.** Four inferential roles, four projectibility profiles, four characteristic misanalyses.

**9.2 What the typology buys.** Re-read confused debates as one profile mistaken for another. Index evaluation design (scenario and metric selection, aggregation, reporting, uncertainty) and governance language to the inferential role at issue. Who uses a label, and what decision it licenses, is part of the measurement system.

**9.3 Limits and extensions.** *Bias* as a deployment-sensitive kind, gestured at, left for a follow-up. The paper is a controlled comparison, not a survey.

**9.4 Close.** Return to inference licences and projectibility: what an evaluation term does is fixed by what it licenses and what makes that licence travel.

---

*Newly pulled and verified for this outline pass: Raji et al. 2021 (§1, §7) and Vassilev et al. 2024 / NIST AI 100-2e2023 (§6). Source tags are still author-year shortforms, to be keyed at drafting; model-assisted citations still need the verification pass STATUS.md flags.*

*Review-board asks folded in as section beats rather than standalone sections: valid comparison (§2.5), institutional use (§2.6, §9.2), measurement-practice co-evolution (§2.6). If any of these wants a full section, it is a quick promotion.*
