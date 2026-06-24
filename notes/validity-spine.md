# Validity spine notes

Date: 2026-05-15

Purpose: build the construct-validity bridge for the paper. These notes are
source-grounded planning notes, not polished prose.

## Draft use

The paper should use validity theory to block a misleading alternative: that
AI-evaluation terms are mainly a problem of definition. The better framing is
that evaluation terms license inferences from scores, model outputs, or observed
interactions to higher-level claims. The question is not simply what
`hallucination`, `jailbreak`, `reasoning`, or `alignment` mean. It is what
interpretation a measurement supports, under what operationalization, and in
what use context.

The spine can be stated this way:

1. Cronbach and Meehl: construct claims require a network of theoretical and
   observable relations.
2. Embretson/Whitely and Borsboom: validity has a mechanism question, not just
   a correlation question.
3. Messick and Kane: validity attaches to score meaning, interpretation, and
   use, not to a test in isolation.
4. Adcock and Collier: measurement validity depends on the movement from
   background concepts to systematized concepts, indicators, and scores.
5. Chouldechova et al., Bean et al., and Freiesleben: LLM evaluations inherit
   these problems directly.

## Source notes

### Cronbach and Meehl 1955, `cronbach1955construct.pdf`

Core claim: construct validation is needed when a test score is interpreted as
measuring an attribute not operationally defined. It requires a theory-like
network linking constructs and observables, not a single criterion correlation.

Key pages:

- p. 282: construct validation is triggered by interpretation of a test as a
  measure of an attribute not operationally defined. Short usable phrase:
  "What constructs account for variance in test performance?"
- p. 284: construct validation defends a proposed interpretation of a test.
- p. 285: warns against treating a single criterion as sufficient when the
  construct is the central concern.
- p. 286: analysis of factors determining behavior is itself a central type of
  validation.
- p. 300: summary: construct validity is possible only when network statements
  lead to predicted observable relations, and the network must be explicit
  enough for evidence to be interpreted.

Use in paper: introduce the idea that AI evaluation terms need a network of
relations. A benchmark score for `reasoning` or a detection label for
`hallucination` cannot by itself establish the construct. It must be embedded in
a network: task design, model behavior, mechanisms, contrast classes, and
predictive/explanatory roles.

Risk: Cronbach and Meehl's original formulation is human-testing-centered and
psychological. Do not transfer it wholesale to LLMs as if LLMs had the same
psychological attributes. Use it as a structure for asking what a construct
claim would need.

### Embretson/Whitely 1983, `embretson1983construct.pdf`

Core claim: construct validation has two separable parts. Construct
representation concerns mechanisms underlying item responses; nomothetic span
concerns the relation between a score and other variables.

Key pages:

- p. 179: separates construct representation from nomothetic span.
- p. 180: construct representation is about identifying mechanisms underlying
  task performance; its goal is task decomposition.
- p. 195: construct representation and nomothetic span are interactive phases;
  nomothetic span can test theory but is not the primary evidence about the
  mechanism reflected in the test.

Use in paper: this is useful for the HPC/Khalidi move. It lets us say that a
projectible evaluation kind should not merely correlate with downstream
outcomes; we also need some account of the structures or mechanisms that make
the label travel. For hallucination, this points toward retrieval failures,
source-use failures, decoding, uncertainty, and evaluation incentives. For
jailbreak, it points toward the adversarial relation among model policy, prompt
strategy, safety tuning, and prohibited-output definitions.

Risk: Embretson/Whitely's language of item responses and cognitive processing is
again human-testing-centered. For LLMs, "mechanism" may mean internal model
mechanism, training/inference mechanism, deployment mechanism, or interactional
mechanism. The paper should keep those levels distinct.

### Messick 1995, `messick1995validity.pdf`

Core claim: validity is an evaluative judgment about the evidence and rationales
supporting interpretations and actions based on scores. It is not a property of
the test as such. Consequences and values belong inside validation because they
are part of score meaning and use.

Key pages:

- p. 741: validity concerns support for interpretations and actions based on
  scores; it is not a property of the assessment alone.
- p. 741: score meaning depends on items, persons responding, and assessment
  context.
- p. 743: construct validity integrates evidence bearing on score
  interpretation, including content- and criterion-related evidence.
- p. 748: values and consequences are part of the unified validity matrix.

Use in paper: use Messick to connect evaluation terms to use contexts. A
`trustworthiness` or `alignment` score cannot be valid in the abstract; it is
valid only relative to a proposed interpretation and use. This supports the
umbrella-construct treatment of alignment and trustworthiness.

Risk: Messick's broad view can blur the line between construct validity and all
things worth caring about. Use Kane and Borsboom as correctives: we need
explicit arguments and we need to keep the mechanism/construct question from
disappearing into consequences.

### Kane 2013, `kane2013validating.pdf`

Core claim: validation evaluates the plausibility of claims based on scores.
The claims should be laid out as an interpretation/use argument specifying
inferences and assumptions from observed responses to interpretations and uses.

Key pages:

- article p. 1, PDF p. 2: validity concerns score interpretations and uses, not
  the test or score alone.
- article p. 3, PDF p. 4: validity is a matter of degree and can change as
  evidence accumulates.
- article p. 7, PDF p. 8: contrasts Cronbach and Meehl's strong program with a
  weak "do-it-yourself kit" of disjoint facts.
- article p. 11, PDF p. 12: interpretation/use arguments include scoring,
  generalization, extrapolation, causal, and decision inferences.
- article p. 19, PDF p. 20: warns against reification, gilding the lily, and
  statistical surrogation.

Use in paper: Kane is the clearest source for the draft's argumentative method.
For each AI evaluation kind, ask what inference chain is being made:

- From output to failure label.
- From failure label to model property.
- From benchmark score to capability attribution.
- From aggregate score to deployment decision or governance claim.

Kane is also the source for warning against benchmark essentialism: a benchmark
score is not the desired construct, and a correlate should not be treated as an
explanation.

Risk: if used too heavily, the paper could become a validity-theory paper rather
than a kind-theory paper. Keep Kane as the bridge into the typology.

### Borsboom, Mellenbergh, and van Heerden 2004, `borsboom2004concept.pdf`

Core claim: a test is valid for measuring an attribute if the attribute exists
and variations in the attribute causally produce variation in measurement
outcomes. Correlation tables are only circumstantial evidence unless connected
to a theory of response behavior.

Key pages:

- p. 1061: states the causal account of validity.
- p. 1062: validity evidence should focus on processes conveying the attribute's
  effect on measurement outcomes.
- p. 1063: distinguishes validity as a property from validation as an activity.

Use in paper: Borsboom is a useful foil. For LLM capability terms, the causal
account may be too ontologically demanding if it requires an internal model
attribute analogous to human reasoning. But the causal insistence is still
valuable for the paper's HPC/Khalidi side: projectible kinds require explanatory
structure, not just labels that correlate with scores.

Risk: do not present Borsboom as the paper's full theory of AI-evaluation
kinds. The paper needs a weaker, field-relative causal-network account: a kind
can be useful without a single internal psychological attribute.

### Adcock and Collier 2001, `adcock2001measurement.pdf`

Core claim: measurement validity asks whether scores meaningfully capture the
systematized concept that an indicator operationalizes. The framework separates
background concept, systematized concept, indicator, and score.

Key pages:

- p. 529: measurement validity concerns whether operationalization and scoring
  adequately reflect the concept.
- p. 530: four-level framework from background concept to systematized concept,
  indicators, and scores.
- p. 531: valid measurement is about interpreting scores in terms of the
  systematized concept.
- p. 533: conceptual disputes and measurement-validity disputes should not be
  conflated.
- p. 543: content, convergent/discriminant, and nomological validation provide
  different evidence within a unified assessment.

Use in paper: use this to structure the intro problem. AI governance often moves
too quickly from a background concept (`alignment`, `reasoning`, `bias`) to an
indicator or score. The paper can argue that many disputes over AI evaluation
terms are disputes about level: some are concept disputes, some are
operationalization disputes, and some are inference/use disputes.

Risk: their examples are political science. Use Chouldechova et al. to justify
the direct transfer to GenAI evaluation.

### Chouldechova et al. 2024, `chouldechova2024shared.pdf`

Core claim: valid measurement of GenAI capabilities, risks, and impacts
requires systematizing, operationalizing, and applying not only concepts, but
also contexts/instances, populations, and metrics/amounts.

Key pages:

- p. 1: GenAI evaluation can be framed as measuring an amount of a concept in
  instances from a population.
- p. 2: validity concerns arise from under-specifying amounts, populations, and
  instances, not only concepts.
- p. 3: framework extends Adcock and Collier across concept, instance,
  population, and amount.
- p. 3: the framework is intended to help "evaluate evaluations" and improve
  design.

Use in paper: this is the cleanest bridge into current AI evaluation. It allows
the paper to say that AI-evaluation kind terms are not free-floating terms.
They are measurement terms embedded in instances, populations, target
parameters, estimators, and use contexts.

Examples to connect:

- Hallucination: amount/prevalence of what failure, in which task population?
- Jailbreak: success rate under which adversarial population?
- Reasoning: average performance on which task instances, representing what
  target population of reasoning cases?
- Trustworthiness: which component concept, which population, which metric?

Risk: Chouldechova et al. give a measurement framework, not a kind theory. The
paper's contribution is to combine this measurement framework with kind
pluralism and HPC/network projectibility.

### Bean et al. 2025, `bean2025measuring.pdf`

Core claim: LLM benchmarks often make weakly supported claims because the
phenomenon, task, metric, and claim are not aligned with strong construct
validity.

Key pages:

- p. 1: reliable measurement of abstract phenomena such as safety and
  robustness requires construct validity.
- p. 2: a benchmark operationalizes a phenomenon via a task and metric to
  support a claim.
- p. 2: benchmark scores can be irrelevant or misleading when construct validity
  is low.
- p. 2: systematic review of 445 LLM benchmark articles.
- p. 5: many benchmark phenomena are contested or undefined; construct validity
  is often not discussed.
- pp. 8--9: recommendations include statistical methods, error analysis, and
  explicit justification of construct validity.

Use in paper: Bean et al. provide empirical support for the claim that AI evals
often treat benchmark construction as if the target phenomenon were already
settled. This backs the paper's "benchmark essentialism" target. It also gives a
practical vocabulary: phenomenon, task, metric, claim.

Risk: this source is recent and directly in the same space, so it may overlap
with the paper. The distinction should be clear: Bean et al. improve benchmark
practice; this paper classifies the different kinds of kind-term that benchmarks
attempt to operationalize.

### Freiesleben 2026, `freiesleben2026establishing.pdf`

Core claim: LLM capability benchmarks need nomological networks. The
nomological account is better suited than a strong causal account or a purely
inferential account for current LLM capability research.

Key pages:

- p. 1: LLM researchers attribute capabilities such as reasoning or theory of
  mind on the basis of benchmark performance.
- p. 2: capability language is risky because humans interpret it using broad
  human capability associations.
- p. 2: contrasts nomological, inferential, and causal accounts of construct
  validity.
- pp. 3--4: Borsboom's causal account is ontologically demanding for LLMs.
- pp. 4--5: Messick/Kane-style inferentialism avoids ontology but gives limited
  resources for theorizing the construct.
- pp. 5--6: nomological networks provide a middle ground.
- p. 7: researchers should design nomological networks before benchmarks.
- p. 10: conflicts between theory and measurement create a Duhem-Quine problem:
  the measure, theory, or both may need revision.

Use in paper: this is the closest existing source to the capability-attribution
part of the argument. It supports treating `reasoning`, `theory of mind`, and
similar terms as capability-attribution terms whose benchmark projectibility
depends on a network. It also warns against importing human psychological
constructs into LLMs without checking whether the network transfers.

Risk: Freiesleben is focused on capability benchmarks. The paper is broader:
hallucination and jailbreak are not simply capability constructs, and alignment
and trustworthiness are umbrella constructs. Use Freiesleben for one cell of the
typology, not the whole typology.

## Synthesis for the paper

### The argumentative bridge

The draft should move from validity to kinds in three steps:

1. AI evaluation terms are used to license inferences.
2. Validity theory shows that those inferences depend on construct,
   operationalization, score, context, and use.
3. Kind theory explains why different evaluation terms support different kinds
   of projectible inferences.

This lets the paper avoid two bad options:

- lexicalism: trying to define evaluation terms by necessary and sufficient
  conditions;
- benchmark essentialism: treating a benchmark score as revealing a capability
  or failure kind directly.

### Proposed paragraph-level claim

AI evaluation terms are not all constructs of the same kind. Some name
first-order failure patterns, some name adversarial relations, some name
capability attributions, and some are umbrella constructs for governance. The
validity literature explains why score interpretations require evidence; the
HPC/Khalidi literature explains why some classifications are projectible even
without analytic definitions. Together, they make room for a pluralist typology
of AI evaluation kinds.

### Where this changes the outline

The paper should probably have a dedicated early section:

`Evaluation Terms as Measurement Constructs`

Possible sequence:

1. AI evaluation labels are used to move from observations to claims.
2. Construct validity: claims from scores require a network or argument.
3. Measurement validity: background concept, systematized concept, indicator,
   score, population, and use can come apart.
4. Therefore, the taxonomy of AI evaluation terms is not cosmetic; different
   terms warrant different inferential structures.

### Citation roles

- Cronbach and Meehl: construct validity and nomological network.
- Embretson/Whitely: mechanism/task-decomposition versus nomothetic-span distinction.
- Messick: validity as score meaning, use, and consequences.
- Kane: interpretation/use argument and anti-reification of scores.
- Borsboom: causal/mechanism foil.
- Adcock and Collier: concept-to-score measurement framework.
- Chouldechova et al.: direct GenAI measurement adaptation.
- Bean et al.: empirical evidence that LLM benchmarks often lack construct
  validity.
- Freiesleben: direct bridge to LLM capability attribution.

## Open checks before citing

- Verify the exact bibliographic entries and DOIs before adding or using any
  citation in `main.tex`.
- Check whether Bean et al. 2025 and Freiesleben 2026 have non-arXiv venue
  metadata by the time the paper is drafted.
- Decide whether Borsboom goes in the first validity paragraph or in a footnote
  as a contrast to the weaker field-relative causal-network view.
- Decide whether to cite the AERA/APA/NCME Standards directly. They may be
  useful for validity orthodoxy, but the current spine already has enough
  conceptual sources.
