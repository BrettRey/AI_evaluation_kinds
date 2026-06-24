# Hallucination notes

Date: 2026-05-15

Purpose: build the first worked case for the paper. These notes are
source-grounded planning notes, not polished prose.

## Draft use

`Hallucination` is the cleanest first worked case because the literature already
treats it as a family of related failures rather than a single essence. The
term is not just a synonym for false output. It picks out a profile involving
plausible generation, factuality or faithfulness failure, source- or
world-grounding, unsupportedness, user context, and detection/mitigation
practices.

This is a good HPC-style case. The category is heterogeneous, but it is not
arbitrary. It is stabilised by recurring mechanisms: pretraining data,
knowledge boundaries, SFT/RLHF incentives, inability to abstain, decoding,
uncertainty, retrieval failures, context use, and evaluation design. It is
projectible because the label licenses useful expectations about what evidence
will detect the failure, when it will recur, and which interventions should
help.

The draft should not say that hallucination is a natural kind. It should say
that hallucination is closer to a homeostatic-profile kind than to either a
mere folk label or a classical kind. Its boundaries are purpose-relative, but
the cluster has enough structure to support prediction, explanation, and
intervention.

## Source notes

### Huang et al. 2025, `huang2025survey.pdf`

Core claim: LLM hallucination needs a broader taxonomy than older
source-conditioned NLG. Huang et al. divide LLM hallucinations into factuality
hallucinations and faithfulness hallucinations, then connect them to data,
training, inference, detection, mitigation, and RAG bottlenecks.

Key pages:

- p. 1: frames LLM hallucination as plausible but nonfactual content; the survey
  covers taxonomy, causes, detection, benchmarks, mitigation, RAG, and open
  problems.
- p. 2: older NLG definitions focused on nonsensical or source-unfaithful
  generation; LLMs require a broader factuality/faithfulness taxonomy.
- p. 5: intrinsic hallucination contradicts source content; extrinsic
  hallucination is not verifiable from the source or external knowledge.
- p. 5: pretraining, SFT, and RLHF each play different roles in capability and
  preference alignment.
- p. 7: faithfulness hallucination includes instruction inconsistency, context
  inconsistency, and logical inconsistency.
- pp. 7--10: data-related causes include misinformation, bias, long-tail
  knowledge gaps, out-of-date knowledge, copyright-sensitive gaps, and inferior
  alignment data.
- pp. 10--12: training-related causes include pretraining limits, SFT beyond
  the model's knowledge boundary, inability to reject, RLHF-driven sycophancy,
  stochastic decoding, over-confidence, softmax bottlenecks, and reasoning
  failure.
- pp. 12--16: detection splits into factuality detection and faithfulness
  detection. Factuality detection often decomposes outputs into factual claims
  and verifies them against sources; uncertainty methods try to detect risk
  without retrieval.
- pp. 17--19: benchmarks differ by whether they test factuality or faithfulness,
  whether they use QA or detection, whether they use human labels, and what
  metric they report.
- pp. 19--20: mitigation maps back to causes: filtering, editing, and
  retrieval-augmented generation target data-related hallucinations.
- pp. 27--32: RAG itself introduces failure points: retrieval intent,
  ambiguous queries, complex queries, source quality, retriever quality, noisy
  context, context conflict, insufficient context use, and source attribution.

Use in paper: main taxonomy and mechanism anchor. Huang lets the draft say that
hallucination is already treated as a structured family. It also gives the
bridge to sycophancy: if RLHF rewards pleasing or preference-matching answers,
some hallucination-like untruthfulness is an alignment artefact rather than a
mere failure to align.

Risk: the survey is very broad and tends to enumerate mechanisms. The paper
should not reproduce the taxonomy as a list. Use it to support the claim that
the category has an organised profile.

### Ji et al. 2023, `ji2023survey.pdf`

Core claim: in NLG, hallucination is generated text that appears fluent and
natural while being nonsensical or unfaithful to the source. The intrinsic vs
extrinsic distinction predates the LLM-specific factuality/faithfulness
taxonomy.

Key pages:

- p. 1: hallucination degrades NLG performance and fails user expectations; the
  survey covers metrics, mitigation, and task settings.
- p. 3: standard definition: generated content is nonsensical or unfaithful to
  source content; intrinsic hallucination contradicts the source, while
  extrinsic hallucination cannot be verified from the source.
- p. 3: extrinsic content can sometimes be factually correct or useful, so
  hallucination cannot be reduced to literal falsity.
- p. 5: source type and tolerance differ by task. Summarization and data-to-text
  tolerate hallucination poorly; dialogue can tolerate more unverified content
  because engagement and continuation matter.
- p. 19: open-domain dialogue lacks a standard hallucination metric; external
  knowledge can function as the source for judging intrinsic/extrinsic
  hallucination.
- p. 24: data-to-text has low tolerance for hallucination in real applications;
  metrics include overlap, entity, QA, and NLI-based approaches.
- p. 28: NMT detection methods rely on entropy, attention, token-level, and
  similarity assumptions; these can fail with paraphrase and synonymy.
- p. 31: causes include noisy data, erroneous parametric knowledge, incorrect
  attention, and training choices; intrinsic and extrinsic hallucination call
  for different mitigation strategies.

Use in paper: use Ji as the historical baseline. The LLM-era category inherits
the source-faithfulness problem but extends it to open-domain factuality,
instruction following, and user context.

Risk: do not make Ji's source-conditioned framing carry all of the LLM case.
It is better as a contrast point.

### Manakul et al. 2023, `manakul2023selfcheckgpt.pdf`

Core claim: SelfCheckGPT detects hallucination in black-box LLMs by sampling
multiple responses. If the model knows the relevant facts, samples tend to
agree. If the output is hallucinated, sampled responses tend to diverge or
contradict one another.

Key pages:

- p. 9004: LLMs produce fluent responses but hallucinate facts; SelfCheckGPT is
  a zero-resource, black-box method needing no external database.
- pp. 9004--9005: the motivating idea is consistency across sampled outputs:
  supported facts recur, hallucinated facts vary.
- p. 9005: existing fact-checking methods can require token probabilities or
  external databases; SelfCheckGPT targets cases where those are unavailable.
- pp. 9006--9007: factual sentences are expected to have lower uncertainty;
  SelfCheckGPT compares a main response with stochastic samples at sentence
  level.

Use in paper: measurement example. It shows one projectible consequence of the
hallucination profile: unsupported facts tend to be unstable under resampling,
so behavioural consistency can serve as a detection signal when external ground
truth is unavailable.

Risk: SelfCheckGPT assumes sampled consistency tracks factuality. That can fail
when the model consistently repeats the same falsehood or inconsistently states
rare true facts. Use it as a detection signal, not a definition.

### Min et al. 2023, `min2023factscore.pdf`

Core claim: long-form factuality cannot be evaluated well with binary
whole-output judgments because a single generation mixes supported and
unsupported pieces of information. FActScore decomposes generations into atomic
facts and measures the percentage supported by a reliable knowledge source.

Key pages:

- p. 12076: long-form factuality evaluation is difficult because generations
  contain mixed supported and unsupported information; FActScore uses atomic
  facts.
- pp. 12076--12077: the metric computes factual precision by checking atomic
  facts against a source; human evaluation is costly, so the authors introduce
  an automated estimator.
- p. 12078: the definition explicitly makes factual precision relative to a
  chosen knowledge source. It assumes support judgments are undebatable, facts
  have equal weight, and the source is non-conflicting.
- p. 12079: in biography generation, InstructGPT, ChatGPT, and PerplexityAI
  achieve FActScores of 42.5%, 58.3%, and 71.5%, respectively.

Use in paper: validity/operationalization example. FActScore makes visible that
`hallucination` labels are granular and source-relative. A generation can be
partly supported, partly unsupported, and partly irrelevant.

Risk: FActScore measures factual precision, not full hallucination. It does not
measure recall, relevance, pragmatic helpfulness, or whether a model should have
abstained.

### Shuster et al. 2021, `shuster2021retrieval.pdf`

Core claim: retrieval augmentation reduces knowledge hallucination in dialogue
while preserving conversational ability, especially when the model has to
generalize beyond training topics.

Key pages:

- p. 3784: state-of-the-art dialogue models can produce plausible but factually
  incorrect statements; retrieval augmentation is tested as a mitigation.
- pp. 3784--3785: knowledge is otherwise stored implicitly in model weights,
  and large models can mix facts between similar entities or make single-token
  factual errors.
- p. 3785: the paper reports that best retrieval-augmented models reduce
  hallucinated responses by over 60%.
- pp. 3787--3788: Knowledge F1 is introduced to capture whether a dialogue
  response overlaps with the knowledge used by human interlocutors.
- pp. 3791--3792: discussion: retrieval strength matters; standard dialogue
  metrics are insufficient for hallucination; retrieval helps but conditioning
  on more documents can also increase hallucination.

Use in paper: mechanism/intervention example. If hallucination were merely
"false text," retrieval would be an external add-on. In the literature, though,
retrieval is part of the causal profile: when parametric knowledge is weak,
external evidence changes the expected failure rate.

Risk: retrieval is not a general cure. Huang's RAG discussion gives the
necessary caveat: retrieval can introduce wrong, noisy, conflicting, or
misused evidence.

### Xiao and Wang 2021, `xiao2021hallucination.pdf`

Core claim: in conditional language generation, hallucination is connected to
predictive uncertainty. Higher uncertainty corresponds to a higher chance of
hallucination, and epistemic uncertainty is more informative than aleatoric
uncertainty.

Key pages:

- p. 2734: hallucination is generated description not supported by source
  input; the paper connects hallucination to predictive uncertainty across
  image captioning and data-to-text generation.
- p. 2735: hallucination is context-dependent; the probability of choosing an
  unsuitable token depends on the current context.
- p. 2737: object and action hallucination rates rise with predictive
  uncertainty in image captioning; epistemic uncertainty has stronger
  correlations than aleatoric uncertainty.
- p. 2741: uncertainty-aware beam search can reduce hallucination, but may
  trade off BLEU, fluency, and coverage.
- p. 2742: the authors conclude that higher uncertainty predicts hallucination
  risk, especially epistemic uncertainty, while noting that confident
  hallucination remains possible.

Use in paper: mechanism/projectibility example. The category supports a
predictive inference: when a model is uncertain about the source-conditioned
continuation, hallucination risk rises, and uncertainty-aware decoding can
shift the risk profile.

Risk: the paper is not LLM-specific and studies conditional generation tasks.
Use it as evidence for one stabilizing mechanism, not as the master account.

### Lin et al. 2022, `lin2022truthfulqa.pdf`

Core claim: TruthfulQA measures whether models generate truthful answers to
questions designed to elicit common human falsehoods. Larger models were less
truthful on this benchmark, suggesting that scaling can improve imitation of
false training-distribution beliefs rather than truthfulness.

Key pages:

- p. 1: TruthfulQA has 817 questions across 38 categories; best model tested
  was truthful on 58% of questions, while humans reached 94%.
- p. 1: the paper defines `imitative falsehoods` as false answers with high
  likelihood under the training distribution.
- pp. 2--3: truthfulness is separated from informativeness; non-committal
  answers count as truthful but can be uninformative.
- p. 7: evidence for imitative falsehoods includes consistency across model
  families, matched controls, and paraphrases.
- pp. 8--9: TruthfulQA is related to factuality and hallucination but targets a
  specific failure of text imitation objectives.

Use in paper: bridge case. TruthfulQA is not simply a hallucination benchmark;
it is useful because it shows that falsehood can arise from successful
imitation. This supports the sycophancy/RLHF pressure point: some epistemic
failures are alignment-to-objective phenomena.

Risk: do not collapse truthfulness into hallucination. Truthfulness includes
refusal, uncertainty, and informativeness in ways that standard hallucination
metrics often do not.

## Synthesis

### Category Profile

Hallucination has at least five recurrent dimensions:

1. Plausible surface form: the output often appears fluent, confident, or
   natural.
2. Grounding failure: the output fails against a source, world facts, user
   context, instruction, or internal logical constraints.
3. Evidence relation: the relevant question is often support or verifiability,
   not bare truth alone.
4. Granularity: hallucination can attach to tokens, entities, sentences,
   atomic facts, whole passages, dialogue turns, or task outcomes.
5. Use context: the same unsupported content may be intolerable in
   summarization or data-to-text, more ambiguous in open-domain dialogue, and
   differently operationalized in QA, long-form biography, or RAG.

This profile explains why `false output` is too crude. Some falsehoods are not
hallucinations in the evaluation sense; some extrinsic content is true but
unsupported; some outputs are logically inconsistent without being a single
wrong fact; some failures are instruction- or context-faithfulness failures.

### Stabilizing Mechanisms

The literature repeatedly returns to a small set of mechanisms:

1. Data: misinformation, social bias, duplication, missing long-tail knowledge,
   outdated knowledge, unavailable copyrighted knowledge, and misaligned
   instruction data.
2. Training: next-token pretraining, SFT beyond knowledge boundaries, inability
   to reject, and RLHF preference pressure.
3. Inference: stochastic decoding, temperature, exposure bias, over-confidence,
   softmax limitations, reasoning failure, and uncertainty.
4. Retrieval: whether retrieval is triggered, what source is available, how the
   query is interpreted, how chunks are retrieved, and whether the generator
   uses or ignores evidence.
5. Measurement: source choice, atomic-fact decomposition, sampling consistency,
   QA/NLI/classifier metrics, LLM judges, and human annotation.

These mechanisms are not rival essences. They stabilize different regions of
the same family. That is exactly why the category is useful but not classical.

### Projectibility

The projectible content of `hallucination` is what makes it useful as an
evaluation kind:

1. If the task supplies a stable source document, intrinsic or
   context-faithfulness hallucination should be easier to detect than
   open-domain factual fabrication.
2. If a generation is long-form, whole-output labels will hide mixed support.
   Atomic-fact or claim-level evaluation should be more informative.
3. If a model is outside its knowledge boundary, especially with long-tail or
   up-to-date facts, hallucination risk should rise unless the system can
   retrieve, abstain, or express uncertainty.
4. If stochastic samples disagree about a purported fact, hallucination risk is
   higher, though consistent falsehoods remain a failure mode.
5. If predictive uncertainty is high, source-conditioned hallucination risk
   should rise, especially where epistemic uncertainty is high.
6. If retrieval supplies relevant, reliable evidence and the generator uses it,
   knowledge hallucination should decrease. If retrieval is irrelevant, noisy,
   conflicting, or poorly used, hallucination can increase.
7. If optimization rewards helpful-looking, agreeable, or preference-matching
   answers more than truthfulness, some hallucination-like failures should be
   expected as alignment-to-objective effects.

These are the inferential payoffs the draft should foreground. They show why a
kind term matters: it lets us expect recurring evidence patterns and
intervention effects.

### Validity Link

Hallucination metrics make the validity problem concrete. A benchmark score
does not measure hallucination in the abstract. It measures a specified
operationalization over a population of tasks and outputs, under a chosen
source of truth, with a chosen granularity and metric.

FActScore measures supported atomic facts relative to a source. SelfCheckGPT
measures behavioural consistency across samples. Knowledge F1 measures overlap
with grounding knowledge in dialogue. TruthfulQA measures truthful responses to
adversarial misconception questions. These are related, but they license
different inferences.

This should connect back to Kane and Chouldechova et al.: the validity question
is what interpretation/use argument takes us from observed output, to
hallucination label, to model property, to deployment decision.

### Relation to Typology

Hallucination should be the paper's first-order failure-kind case. It is mostly
about outputs and output-producing processes, even though user context and
retrieval context matter. It contrasts with:

1. Jailbreak: more explicitly adversarial and relational. The failure exists in
   a network of attacker strategy, model policy, prohibited content, and safety
   mechanism.
2. Reasoning/emergence/agency: capability-attribution terms where the main
   problem is whether benchmark behaviour supports a higher-level attribution.
3. Alignment/trustworthiness: umbrella constructs that coordinate multiple
   first-order and relational kinds, including hallucination.

## Draft Section Shape

Start with the temptation: hallucination looks easy because everyone thinks it
means "making things up." Then reject that as too thin.

First, the literature splits hallucination into factuality and faithfulness,
and older NLG splits it into intrinsic and extrinsic failures. Second, detection
and mitigation do not track a single essence: some methods need source
comparison, some need claim decomposition, some use sampling consistency, some
use uncertainty, and some alter retrieval. Third, the category is still not
arbitrary because these methods work against recurrent mechanisms.

The section's conclusion can be:

> Hallucination is an evaluation kind because it makes a profile projectible:
> plausible unsupported generation tends to recur under identifiable
> data/training/inference/retrieval conditions, and different operationalizations
> expose different parts of that profile. The kind is real enough to guide
> measurement and intervention, but not unified enough to support benchmark
> essentialism.

## Candidate Citation Roles

- Taxonomy anchor: Huang et al. 2025; Ji et al. 2023.
- Detection by consistency: Manakul et al. 2023.
- Long-form factual precision: Min et al. 2023.
- Retrieval mitigation: Shuster et al. 2021.
- Uncertainty mechanism: Xiao and Wang 2021.
- Imitative falsehood bridge: Lin et al. 2022.

## Library/Bib Status

All PDFs needed for this note are present locally. Bibliographic entries still
need to be added before the draft cites these papers directly. DOI/source
metadata below has been checked against Crossref or ACL Anthology:

- Huang et al. 2025: `10.1145/3703155`;
  https://doi.org/10.1145/3703155
- Ji et al. 2023: `10.1145/3571730`;
  https://doi.org/10.1145/3571730
- Manakul et al. 2023: `10.18653/v1/2023.emnlp-main.557`;
  https://aclanthology.org/2023.emnlp-main.557/
- Min et al. 2023: `10.18653/v1/2023.emnlp-main.741`;
  https://aclanthology.org/2023.emnlp-main.741/
- Shuster et al. 2021: `10.18653/v1/2021.findings-emnlp.320`;
  https://aclanthology.org/2021.findings-emnlp.320/
- Xiao and Wang 2021: `10.18653/v1/2021.eacl-main.236`;
  https://aclanthology.org/2021.eacl-main.236/
- Lin et al. 2022: `10.18653/v1/2022.acl-long.229`;
  https://aclanthology.org/2022.acl-long.229/
