# Capability-attribution notes

Date: 2026-05-15

Purpose: build the worked case for `reasoning`, `emergence`, and `agency`.
These are source-grounded planning notes, not polished prose.

## Draft use

Capability-attribution terms should be the third worked case, after
`hallucination` and `jailbreak/robustness`. The target is benchmark
essentialism: the slide from a score, leaderboard, or impressive trace to a
claim that the system has a capability-kind.

The case should not deny capabilities. It should ask what inference is licensed:
from which task distribution, under which metric, prompting regime, architecture,
tool scaffold, and interaction context, to which capability claim?

This is where construct validity and Khalidi meet. A capability term is useful
when it marks a projectible node in an evaluation network. It is weak when it is
only a label placed on a high score.

## Source notes

### Khalidi 2018, `khalidi2018causal.pdf`

Core claim: natural kind predicates are projectible because the properties
associated with the kind are causally structured. Kinds are not undifferentiated
property lists; they are clusters of core causal properties that generate
derivative properties in recurrent causal processes.

Use in paper: this is the direct bridge from "score cluster" to "kind claim."
If `reasoning` or `agency` is a projectible kind-term in AI evaluation, the
paper needs a causal-network story: which central features generate which
downstream regularities, and in which environments?

Risk: do not require one internal model mechanism. Khalidi's account is useful
because it is looser than a single essence or a single homeostatic mechanism.

### Wei et al. 2022, `wei2022emergent.pdf`

Core claim: some LLM abilities appear only above a scale threshold. The paper
defines emergence operationally: an ability is absent in smaller models but
present in larger ones, with scale measured through compute, parameters, or
training data.

Use in paper: positive account of capability attribution. It shows why the field
wants capability language: scaling curves sometimes make a behavior look
qualitatively new.

Risk: the emergence claim is benchmark- and metric-relative. Use it as the
motivating view, not as a settled metaphysical claim.

### Schaeffer et al. 2023, `schaeffer2023emergent.pdf`

Core claim: many alleged emergent abilities may be artefacts of metric choice.
Nonlinear or discontinuous metrics can make smooth underlying performance
changes look sharp, while continuous metrics often reveal gradual improvement.

Use in paper: the cleanest anti-essentialist counterpoint. If changing the
metric changes whether a capability "emerges," then benchmark results are not
self-interpreting kind discoveries.

Risk: do not overstate this as "emergence is fake." The source challenges one
interpretation of emergence, especially sharp and unpredictable emergence.

### Huang and Chang 2023, `huang2023reasoning.pdf`

Core claim: reasoning in LLMs is a live attribution problem. The survey reviews
elicitation methods, benchmarks, and analyses, but repeatedly notes that it is
unclear whether LLMs are reasoning or producing reasoning-like outputs.

Key pages:

- pp. 1--2: reasoning is treated as a central human-intelligence capacity, but
  the paper states that it remains unclear whether LLMs actually reason and to
  what extent.
- p. 2: the survey distinguishes deductive, inductive, abductive, analogical,
  causal, probabilistic, formal, and informal reasoning. This blocks a flat
  reading of `reasoning`.
- p. 3: the authors explicitly warn that their use of `reasoning` does not imply
  that LLMs reason in the same way as humans.
- pp. 9--10: high benchmark performance, chain-of-thought traces, and
  human-like content effects are not enough to conclude that LLMs truly reason.
  The survey flags heuristics, inconsistent rationales, benchmark artefacts,
  training-data frequency effects, and lack of robustness.

Use in paper: reasoning is the contested-attribution anchor. It lets the paper
say that even the survey literature treats `reasoning` as an operationally
plural, unsettled construct.

Risk: surveys can smooth over disagreements. Pair with Mirzadeh et al. for a
concrete benchmark-fragility example.

### Mirzadeh et al. 2025, `mirzadeh2025gsm.pdf`

Core claim: high performance on a standard mathematical-reasoning benchmark
does not by itself show robust mathematical reasoning. GSM-Symbolic generates
variants of GSM8K problems and shows substantial variance and performance drops
under changes to values, clause count, and irrelevant but tempting information.

Key pages:

- pp. 1--3: GSM8K provides a single metric on a fixed test set; this risks data
  contamination and hides behavior under controlled variants.
- p. 2: the paper reports that model performance can be treated as a distribution
  with unwarranted variance across instantiations of the same question.
- pp. 8--10: GSM-NoOp adds seemingly relevant but irrelevant clauses; models
  often convert those clauses into operations and suffer large drops, including
  drops up to 65% for some models.
- p. 11: the conclusion interprets high variance, difficulty sensitivity, and
  sensitivity to irrelevant information as evidence that mathematical reasoning
  is fragile and may resemble sophisticated pattern matching more than formal
  logical reasoning.

Use in paper: concrete example for the claim that a benchmark score can fail to
license the intended capability attribution. This is construct validity in the
wild: changing the population of items changes the interpretation.

Risk: this is about mathematical reasoning, not all reasoning. Do not generalize
to reasoning as a whole without the Huang and Freiesleben frame.

### Hendrycks et al. 2021, `hendrycks2020measuring.pdf`

Core claim: MMLU is a broad benchmark covering 57 academic and professional
subjects. The paper frames high accuracy as requiring world knowledge and
problem solving, while noting lopsided performance and calibration failures.

Use in paper: benchmark exemplar. MMLU shows how a score becomes a broad
capability proxy: from multiple-choice subject performance to claims about
understanding, problem solving, and professional competence.

Risk: the paper itself contains warnings about unevenness and calibration.
Those warnings are more useful for us than the aggregate score.

### Srivastava et al. 2023, `srivastava2022beyond.pdf`

Core claim: BIG-bench was designed to measure diverse, difficult, and
potentially future model capabilities. It reports both gradual scaling and
"breakthrough" behavior, while explicitly noting that breakthrough behavior can
depend on task specification and brittle metrics.

Use in paper: bridge between emergence and benchmark design. BIG-bench is not
only a data source for emergence claims; it also contains the caution that
metric choice and task decomposition affect what looks like a breakthrough.

Risk: BIG-bench is a broad collaborative benchmark with heterogeneous tasks. Its
aggregate scores need careful interpretation.

### Liang et al. 2023, `liang2022holistic.pdf`

Core claim: HELM argues for holistic evaluation through coverage,
multi-metric measurement, and standardization. It makes explicit that scenarios
and metrics are choices, and that many desired evaluations are missing.

Use in paper: infrastructure alternative to benchmark essentialism. HELM
supports the claim that capability evaluation needs a taxonomy of scenarios and
desiderata, not one canonical score.

Risk: HELM still implements a finite benchmark. It is best used as a better
evaluation architecture, not as a complete solution.

### Kiela et al. 2021, `kiela2021dynabench.pdf`

Core claim: static benchmarks saturate and can overstate model ability.
Dynabench proposes dynamic human-and-model-in-the-loop data creation, where
annotators produce examples that models fail but humans validate.

Use in paper: dynamic evaluation source. This helps argue that capability claims
are interactional and temporally unstable: what counts as robust performance
changes as models and adversaries adapt.

Risk: dynamic adversarial data can create distribution shift. The paper itself
raises this caveat; use it.

### Freiesleben 2026, `freiesleben2026establishing.pdf`

Core claim: LLM capability benchmarks need nomological networks. Isolated
benchmark scores are insufficient for constructs such as reasoning; researchers
need content, concurrent, criterion, convergent, and discriminant validity.

Use in paper: direct philosophical bridge. It says almost exactly what the
capability case needs: benchmark design should follow construct articulation,
not substitute for it.

Risk: this is a preprint. Keep it as a contemporary bridge, with Cronbach,
Messick, Kane, and Adcock doing the established validity work.

### Plaat et al. 2025, `plaat2025agentic.pdf`

Core claim: agentic LLMs are defined as agents that receive natural-language
input from the environment, reason to make decisions, and take autonomous
actions to achieve goals. The survey organizes the field around reasoning,
acting, and interacting.

Key pages:

- pp. 1--4: agentic LLMs are framed as systems that reason, act, and interact.
  The paper distinguishes passive prediction from agentic autonomy.
- p. 4: the definition includes environment input, decision-making, autonomous
  action, and goal achievement.
- pp. 8--10: reasoning methods such as chain-of-thought, self-reflection,
  planning/search, and retrieval are treated as foundations for action and
  interaction.
- Later sections connect acting to tools, APIs, robots, assistants, and
  high-impact application settings, and interaction to multi-agent simulation
  and emergent social behavior.

Use in paper: agency anchor. The point is not that an LLM has agency internally.
Agency is an architectural and interactional attribution: model plus tool use,
planning, autonomy, goals, feedback, environment, and social interaction.

Verification note: the local PDF is now the JAIR version. JAIR, Crossref, and
arXiv metadata verify volume 84, article 29, and DOI `10.1613/jair.1.18675`.

## HPC / Projectibility Check

The capability-attribution case passes the "not merely definitional" test. These
terms are doing projective work in the field: `reasoning`, `emergence`, and
`agency` are used to predict transfer, robustness, risk, and deployment
suitability.

The weak point is construct under-specification. A benchmark can cluster
behaviors without identifying the causal or nomological structure that would
make the capability claim travel. The paper should therefore phrase this case as
a warning against score-to-kind shortcuts:

1. A task score is an observation.
2. A benchmark aggregate is an operationalization.
3. A capability attribution is an interpretation.
4. A projectible AI-evaluation kind requires the interpretation to be supported
   by a causal/nomological network.

The contrast with the first two worked cases matters. `Hallucination` and
`jailbreak` start from recurring failure patterns. Capability terms start from
success attributions. They are therefore especially vulnerable to metric choice,
prompting scaffolds, contamination, tool use, and hidden interaction structure.
