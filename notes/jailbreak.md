# Jailbreak notes

Date: 2026-05-15

Purpose: build the second worked case for the paper. These notes are
source-grounded planning notes, not polished prose.

Security handling: the source papers contain live attack examples. This note
does not reproduce reusable jailbreak prompts, adversarial suffixes, or harmful
request text. It records taxonomies, mechanisms, evaluation designs, and page
references.

## Draft use

`Jailbreak` is the cleanest second worked case because it is relational in a
way hallucination is not. A jailbreak is not simply an unsafe output. It is an
adversarially shaped interaction that causes a model or LLM-integrated
application to cross a specified safety or policy boundary that it would
otherwise be expected to maintain.

That makes it a strong case for the paper's typology. The category includes a
model, a policy boundary, a user or attacker goal, an input channel, a defense
surface, a deployment context, and an evaluation procedure. Direct chat
jailbreaks, transferable adversarial suffixes, persuasion-based attacks, and
indirect prompt injection are not one mechanism. They are a family of
network-positioned failures.

The category is still projectible. Calling an interaction a jailbreak licenses
expectations about recurrence, transfer, defense fragility, evaluation design,
and deployment risk. The inferences are purpose-relative: a security engineer,
benchmark designer, and policy evaluator may carve different subtypes. But the
profile is not arbitrary.

## Source notes

### Yi et al. 2024, `yi2024jailbreak.pdf`

Core claim: jailbreak research is best understood through an attack/defense
taxonomy. Yi et al. divide attacks by model transparency, then subdivide them
into white-box and black-box strategies; they divide defenses into prompt-level
and model-level strategies and review evaluation metrics and benchmarks.

Key pages:

- p. 1: defines jailbreaking as adversarial prompting that induces a model to
  generate responses against usage policy and social expectations. The survey
  covers attack taxonomy, defense taxonomy, evaluation, and benchmarks.
- p. 2: Table 1 separates white-box attacks into gradient-based, logits-based,
  and fine-tuning-based methods, and black-box attacks into template
  completion, prompt rewriting, and LLM-based generation. Defenses are
  separated into prompt-level and model-level families.
- p. 3: Figure 1 lays out the attack/defense taxonomy. The white-box section
  frames gradient-based attacks as input manipulation guided by model
  gradients.
- pp. 7--8: black-box template-completion methods exploit capabilities such as
  role playing, contextual framing, and code comprehension. The authors treat
  these as cost-effective but increasingly countered by safety alignment.
- pp. 9--10: prompt-rewriting methods exploit long-tailed or underrepresented
  input distributions, including ciphers and low-resource languages.
- pp. 10--11: LLM-based attack generation uses one or more models to simulate
  attackers and to combine strategies.
- pp. 11--15: prompt-level defenses include prompt detection, perturbation, and
  system-prompt safeguards. Model-level defenses include SFT, RLHF,
  gradient/logit analysis, refinement, and proxy defenses.
- pp. 15--17: evaluation commonly reports attack success rate, but success
  criteria are not unified. Rule-based and LLM-based safety evaluators can
  diverge. The survey compares benchmark datasets such as XSTEST, AdvBench,
  Do-Not-Answer, HarmBench, Safety-Prompts, JailbreakBench, and DoAnythingNow.
- p. 17: the conclusion emphasises that attacks are becoming more effective and
  require less knowledge of the target model, which makes them more practical.

Use in paper: main taxonomy source. Yi et al. support the claim that
`jailbreak` is already treated as a structured family of attack and defense
relations, not as a single output property.

Risk: the survey is broad. Use it to define the profile and evaluation space,
not as evidence that every attack subtype shares one mechanism.

### Shen et al. 2024, `shen2024do.pdf`

Core claim: in-the-wild jailbreak prompts are socially organized, iterated, and
evaluated against concrete policy categories. Shen et al. build JailbreakHub
from 1,405 prompts collected between December 2022 and December 2023, identify
communities of prompt variants, and test them across forbidden-question
scenarios and target models.

Key pages:

- p. 1671: the abstract reports 1,405 jailbreak prompts, 131 prompt
  communities, temporal movement from online communities to prompt-aggregation
  sites, and a large evaluation set spanning 13 forbidden scenarios and six
  LLMs.
- p. 1672: 803 accounts created or shared prompts; 28 accounts curated prompts
  over more than 100 days. Later in the period, prompt-aggregation websites
  became the dominant source. The authors also report that RLHF-trained models
  resist direct forbidden questions better than jailbreak prompts.
- pp. 1672--1673: the paper defines jailbreak prompts as prompts designed to
  bypass built-in safeguards and elicit content that violates usage policy.
  JailbreakHub combines data collection, prompt analysis, and response
  evaluation.
- p. 1677: community analysis shows distinct families of prompt variants and
  their migration across platforms. The paper treats jailbreak prompts as an
  evolving social and technical population.
- pp. 1678--1679: the evaluation uses 13 forbidden scenarios drawn from usage
  policy, generates questions for those scenarios, and tests six target models.
  Metrics include baseline attack success and maximum success across prompt
  variants.
- p. 1679: Table 4 reports that jailbreak prompts substantially raise attack
  success relative to direct forbidden questions for several target models,
  though levels vary by model.
- p. 1685: the appendix reports an automated labeling setup for judging whether
  model responses satisfy the forbidden request.

Use in paper: empirical in-the-wild anchor. Shen et al. show that jailbreaks
are not just laboratory artifacts. The category tracks communities, prompt
lineages, vendor patches, policy taxonomies, and evaluator choices.

Risk: the paper's empirical object is collected prompt text. The draft should
not reproduce prompt content. The useful fact is the population structure and
evaluation design.

### Zou et al. 2023, `zou2023universal.pdf`

Core claim: aligned models can be attacked by automatically generated,
transferable adversarial suffixes. Zou et al. use greedy and gradient-based
search to optimize suffixes that increase the probability of affirmative
responses, then show transfer from open models to black-box production models.

Key pages:

- p. 1: the abstract frames the method as a way of producing objectionable
  behavior from aligned models by attaching optimized suffixes to harmful
  queries. It reports transfer to several public chat interfaces and
  open-source models.
- p. 2: alignment is used in the narrow LLM safety sense: preventing harmful
  outputs from models that are otherwise capable of producing them. The authors
  contrast automated attacks with brittle human-written jailbreaks.
- p. 3: the attack has three elements: an affirmative-response target, a
  greedy/gradient search procedure over discrete tokens, and optimization
  across prompts and models for robustness.
- pp. 7--8: the paper presents the greedy coordinate gradient procedure and the
  multi-prompt/multi-model universal optimization setup.
- pp. 8--9: AdvBench is used as the evaluation dataset. The evaluation tests
  whether attacks circumvent specified guardrails, not whether the underlying
  policy categories are themselves correct.
- p. 9: Table 1 shows strong attack success against the open models studied,
  with differences by model and target condition.
- p. 12: Table 2 reports transfer to black-box systems. Transfer is substantial
  for some systems and much weaker for others.
- pp. 13--16: transfer is pervasive but uneven. Overfitting, model family,
  concatenation strategy, and ensemble choice all affect results.
- pp. 16--17: the discussion treats content filters as attackable too and
  raises the broader question of whether post-hoc alignment can reliably
  constrain models capable of harmful generation.

Use in paper: projectibility source. The attack is important because it makes a
prediction: vulnerabilities can transfer across models that share enough
instruction-following and refusal machinery, but transfer will vary with model
family, filtering, training lineage, and overfitting.

Risk: do not describe the suffix content or operational procedure in more
detail than the abstract methodological level. The useful point is not how to
run the attack, but what the existence of transferable attacks implies for the
kind profile.

### Greshake et al. 2023, `greshake2023not.pdf`

Core claim: indirect prompt injection extends jailbreak-style vulnerability
from direct user interaction to LLM-integrated applications. When systems
retrieve external data or call tools, adversarial instructions can enter
through data channels rather than through the user's prompt.

Key pages:

- p. 1: the abstract argues that LLM-integrated applications blur the line
  between data and instructions. Indirect prompt injection lets adversaries
  affect applications by placing adversarial text in data likely to be
  retrieved.
- p. 2: the paper contrasts indirect prompt injection with direct prompting.
  A remote adversary can affect other users by manipulating retrieved data, and
  impacts include information theft, denial of service, disinformation, and
  manipulation.
- p. 3: the attack surface is described in terms of retrieval, trust
  boundaries, and injection channels. The threat model includes passive
  retrieval, active delivery channels, user-driven retrieval, and hidden
  injections.
- pp. 4--5: the taxonomy connects injection methods to security consequences.
  Tool and API integration increases the stakes because the model may mediate
  actions beyond text generation.
- pp. 8--10: demonstrations include persistence, remote control, manipulation
  of summaries and source use, and interference with application availability.
- pp. 11--12: the authors stress that success is difficult to quantify in
  dynamic applications and that mitigation is likely to be a moving target.
- p. 12: proposed mitigations include filtering, LLM supervision, and
  interpretability-style work, but the paper is cautious about any simple
  solution.

Use in paper: deployment-surface source. Greshake et al. show why `jailbreak`
cannot be treated as a model-internal property. In an agentic or retrieval
setting, the relevant object is a model-application system with trust
boundaries, external content, tool permissions, and persistence.

Risk: this paper uses a security lens rather than the same jailbreak
vocabulary throughout. Present it as a neighbouring and partly overlapping
case: indirect prompt injection broadens the adversarial-network profile.

### Zeng et al. 2024, `zeng2024johnny.pdf`

Core claim: persuasion-based jailbreaks exploit models as language users, not
only as token systems. Zeng et al. build a persuasion taxonomy from social
science, generate persuasive adversarial prompts, and show that persuasion
substantially increases jailbreak risk across model families and risk
categories.

Key pages:

- p. 14322: the abstract contrasts algorithm-focused attacks with everyday
  persuasive interaction. It reports that persuasive adversarial prompts
  achieve high attack success across Llama-2-7B-Chat, GPT-3.5, and GPT-4 in
  repeated trials, and that existing defenses leave a gap.
- p. 14323: the motivation is that ordinary users may intentionally or
  unintentionally use persuasive language. This shifts attention from exotic
  side channels to ordinary communicative competence.
- p. 14324: the persuasion taxonomy has 15 high-level strategies and 40
  techniques drawn from psychology, communication, sociology, marketing, and
  NLP.
- pp. 14325--14326: the method applies the taxonomy to harmful-query
  benchmarks and broad policy risk categories, producing a large set of
  persuasive paraphrases for evaluation.
- pp. 14326--14328: the broad scan finds vulnerability across risk categories,
  with attack effectiveness depending on both risk category and persuasion
  technique.
- pp. 14328--14330: the in-depth probe compares persuasion-based attacks with
  other attack families across several target models. The results vary sharply:
  some models are robust in this setting while others are highly susceptible.
- p. 14330: mutation-based defenses perform better than detection-based
  defenses in their experiments, but can alter benign queries. The authors also
  argue that more capable models may be more affected by persuasive content and
  more resistant to conventional defenses.
- p. 14330: the conclusion claims that a social-science persuasion lens reveals
  a gap in current jailbreak defenses.

Use in paper: social/interactional mechanism source. Zeng et al. let the draft
make a strong projectibility claim: if an LLM becomes more competent at
following complex human communication, some safety vulnerabilities may move
from crude prompt tricks to ordinary persuasive discourse.

Risk: do not overstate the finding as a universal law of model capability. The
results are model- and defense-dependent. Use the paper to show one
communication-mediated attack family.

## Synthesis

The jailbreak profile has at least six recurring components.

First, there is a policy or safety boundary. The boundary may be a vendor usage
policy, benchmark risk category, refusal rule, or application-level security
constraint. Without this boundary, the same output may be merely undesirable,
false, or unsafe, but not a jailbreak.

Second, there is an adversarial relation. The user, attacker, or external data
source shapes the interaction to induce behavior the system is meant to avoid.
This is why jailbreak belongs in the relational/adversarial part of the paper's
typology.

Third, there is an exploited channel. The channel can be direct chat, prompt
rewriting, optimized token suffixes, role or context framing, multilingual or
non-natural encodings, persuasion, retrieval, tool input, email, web content,
or stored application state.

Fourth, there is a model or system affordance. Jailbreaks exploit helpfulness,
instruction following, in-context learning, code comprehension, role play,
affirmative completion, social communication, retrieval integration, and tool
use. Different attack families exploit different affordances.

Fifth, there is a defense relation. Prompt filters, perturbation, system
prompts, SFT, RLHF, proxy models, output filters, and application-level
supervisors can change the profile, but each defense tends to introduce its
own trade-offs: false positives, helpfulness loss, bypass risk, evaluator
dependence, and adaptation by attackers.

Sixth, there is an evaluation setup. Attack success rate is meaningful only
relative to a policy category, target model and version, attack distribution,
success criterion, evaluator, and benign-control set. A jailbreak benchmark is
therefore a measurement practice, not just a collection of prompts.

## Why it is not just "unsafe output"

`Unsafe output` is too thin. A direct forbidden question may be refused; a
transformed interaction may succeed. An output can be harmful without being
produced through bypass. Conversely, indirect prompt injection can compromise
application behavior without primarily producing a forbidden textual answer.

The jailbreak label tracks the bypass relation: an input or retrieved context
causes a model-application system to cross a specified boundary despite a
guardrail. This is the kind-relevant structure.

## Stabilising mechanisms

The recurring mechanisms are plural:

- tension between helpful instruction following and refusal behavior;
- post-hoc safety tuning around models that retain the capability to generate
  harmful content;
- token-level adversarial optimization and transfer across related systems;
- long-tail input distributions, including rare languages, ciphers, and
  non-standard encodings;
- in-context framing, role play, and scenario nesting;
- ordinary persuasive communication;
- blurred data/instruction boundaries in retrieval and tool-using systems;
- online sharing, prompt mutation, vendor patching, and counter-adaptation.

These mechanisms do not define one essence. They stabilize a family of
profiles that are useful for prediction and intervention.

## Projectibility

The jailbreak category supports several inductive inferences.

First, an evaluation that tests only direct forbidden questions will understate
vulnerability to transformed interactions. Shen et al. make this point
empirically by contrasting direct forbidden questions with in-the-wild
jailbreak prompts.

Second, attacks that exploit shared instruction-following machinery may
transfer across models, but transfer should be uneven. Zou et al. show both
transferability and model-specific variation.

Third, prompt-level defenses should be brittle against adaptive attackers.
Yi et al.'s taxonomy and Shen et al.'s prompt-community data both predict a
patch-and-adaptation dynamic.

Fourth, model capability can shift the attack surface. Better language
understanding may reduce some crude attacks while increasing susceptibility to
social or semantically rich attacks. Zeng et al.'s persuasion results make this
especially clear.

Fifth, RAG, tools, memory, and APIs increase blast radius. Greshake et al. show
that the relevant risk can be application compromise rather than only a bad
answer in a chat window.

Sixth, benchmark results should not be generalized without the evaluation
contract. A reported attack success rate depends on forbidden category,
attacker access, prompt distribution, target date/version, refusal criterion,
and evaluator reliability.

## Validity link

The jailbreak case should connect directly to construct validity. An attack
success score is not a pure measure of "model safety." It operationalizes a
particular interpretation: given this policy, this attack distribution, this
target model, and this evaluator, how often does the system cross the boundary?

This matters for the paper because it blocks a common slide from benchmark
score to kind attribution. A model can score well on one jailbreak benchmark
while remaining vulnerable to indirect prompt injection, persuasive attacks, or
new prompt communities. The score can be useful without being the essence of
the kind.

## Relation to the typology

Hallucination is a first-order output or generation-failure case. Jailbreak is
a relational/adversarial network case. The difference matters.

For hallucination, the central questions are about truth, support,
faithfulness, uncertainty, and grounding. For jailbreak, the central questions
are about boundaries, attackers, channels, defenses, policy categories,
deployment surfaces, and evaluators.

Alignment and trustworthiness sit above both as umbrella constructs. They
organize lower-level profiles rather than naming a single projectible kind.

## Draft section shape

The section should start by rejecting the thin gloss:

> Jailbreak is often treated as a colourful name for getting a model to say
> something bad. That description misses the structure that makes the term
> useful. A jailbreak is a bypass relation: an adversarially shaped interaction
> causes a model or model-application system to cross a specified boundary that
> its safety machinery was meant to preserve.

Then use the five sources to build the profile:

1. Yi et al. for the attack/defense taxonomy.
2. Shen et al. for in-the-wild prompt populations and evaluation.
3. Zou et al. for transferability and model-family variation.
4. Greshake et al. for indirect prompt injection and deployment boundaries.
5. Zeng et al. for persuasion and ordinary communicative competence.

The payoff paragraph should be projectibility-first: once an interaction is
classified as a jailbreak, we expect transformed prompts to matter, defenses to
be attack-family-specific, transfer to be uneven, benchmarks to be
policy/evaluator-relative, and deployment integrations to change the risk
surface.

## Candidate citation roles

- Taxonomy: Yi et al. 2024.
- In-the-wild empirical population: Shen et al. 2024.
- Transferable adversarial attacks: Zou et al. 2023.
- Application-integrated/indirect injection: Greshake et al. 2023.
- Persuasion/social mechanism: Zeng et al. 2024.

## Bibliographic status

Verified metadata:

- Shen et al. 2024, `"Do Anything Now": Characterizing and Evaluating
  In-The-Wild Jailbreak Prompts on Large Language Models`, ACM CCS 2024,
  pp. 1671--1685, DOI `10.1145/3658644.3670388`,
  https://doi.org/10.1145/3658644.3670388.
- Greshake et al. 2023, `Not What You've Signed Up For: Compromising
  Real-World LLM-Integrated Applications with Indirect Prompt Injection`, ACM
  AISec 2023, pp. 79--90, DOI `10.1145/3605764.3623985`,
  https://doi.org/10.1145/3605764.3623985.
- Zeng et al. 2024, `How Johnny Can Persuade LLMs to Jailbreak Them:
  Rethinking Persuasion to Challenge AI Safety by Humanizing LLMs`, ACL 2024,
  pp. 14322--14350, DOI `10.18653/v1/2024.acl-long.773`,
  https://aclanthology.org/2024.acl-long.773/.
- Yi et al. 2024, `Jailbreak Attacks and Defenses Against Large Language
  Models: A Survey`, arXiv:2407.04295v2, DOI
  `10.48550/arXiv.2407.04295`, https://arxiv.org/abs/2407.04295.
- Zou et al. 2023, `Universal and Transferable Adversarial Attacks on Aligned
  Language Models`, arXiv:2307.15043v2, DOI
  `10.48550/arXiv.2307.15043`, https://arxiv.org/abs/2307.15043.

No library asks for this note.
