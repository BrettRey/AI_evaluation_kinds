# Review-board synthesis

Date: 2026-05-15

Review type: role-simulated independent Codex reviews. These are not claims
about the named people's actual views.

Review packet: `DECISIONS.md`, `STATUS.md`, `NOTES.md`,
`literature-intake.md`, `references-local.bib`, and the working notes in
`notes/`.

Reviewers simulated:

- Laura Portwood-Stacer
- John Ramsey
- Muhammad Ali Khalidi
- Hasok Chang
- Inioluwa Deborah Raji
- Percy Liang
- Alexandra Chouldechova
- Iman Mirzadeh

## Overall verdict

All eight reviews converge on **Revise and Resubmit**. The project has a strong
publishable core, but the paper should not be drafted as a term map or survey.
It needs to become an inference-and-measurement argument: different AI
evaluation terms license different kinds of inference, fail in different ways,
and require different validation evidence.

## Consensus strengths

1. The core move is strong: AI evaluation debates misfire when they treat
   unlike terms as if they needed the same kind of definition.
2. The construct-validity spine is the right bridge from philosophical kind
   theory to AI evaluation practice.
3. The three worked cases are well chosen: hallucination, jailbreak/robustness,
   and reasoning/emergence/agency mark different inferential structures.
4. Sycophancy is correctly placed as a pressure case for alignment as an
   umbrella construct, not a fourth worked case.
5. The hallucination and jailbreak notes already do useful projectibility work:
   recurrence, detection, intervention, transfer, defense brittleness, and
   deployment risk.

## Consensus weaknesses

1. The paper still lacks a clear classification rule: what makes a term an HPC
   profile, a Khalidian causal-network kind, a capability-attribution term, or
   an umbrella construct?
2. Projectibility is present but not yet governing the architecture. The paper
   must foreground what each classification lets us predict, explain, or refuse
   to infer.
3. The capability-attribution case is the weakest. It is currently more
   skeptical than constructive: it says why benchmark scores do not prove
   reasoning, but not yet what evidence would license a projectible capability
   attribution.
4. The measurement apparatus is too verbal. Each case needs an explicit chain
   from construct to operationalization to task population to metric to score
   to licensed claim to intended use.
5. The accountability layer is thin. Institutional use, affected stakeholders,
   benchmark performativity, measurement invariance, and model-ranking claims
   need to be cross-cutting constraints.

## Productive tensions

The reviews do not disagree about the diagnosis. They differ mainly on emphasis.

- Editorial reviewers want the antagonist sharpened: the bad inference from
  score or label to capability, model property, or governance conclusion.
- Philosophy reviewers want the Boyd/Khalidi/validity division of labor made
  explicit and projectibility placed at the center.
- Measurement reviewers want operational chains, comparison validity,
  invariance, uncertainty, and task/metric dependence.
- AI-evaluation reviewers want the typology to change benchmark design:
  scenario selection, metric choice, aggregation, reporting, and deployment
  interpretation.
- Accountability review wants institutional use and affected stakeholders
  treated as part of the measurement system.

## Prioritized revision list

1. Write the introduction around one recurring failure: AI evaluation discourse
   treats unlike terms as if they licensed the same kind of inference. Examples:
   score to capability, label to model property, benchmark result to governance
   conclusion.
2. Add a framework table early in the paper with these columns: term type,
   object classified, stabilizing structure, operationalization, licensed
   inference, invalid inference, projectibility payoff, validity threat, and
   institutional use.
3. Add a short framework subsection distinguishing Boyd-style HPC profiles from
   Khalidian causal-network nodes. Use hallucination and jailbreak as the
   contrast pair.
4. Rebuild the capability-attribution case around positive standards. Separate
   mathematical reasoning, emergence, and agency because they fail differently:
   item-distribution fragility, metric fragility, prompt/scaffold fragility,
   contamination, and system-boundary dependence.
5. End every worked case with a projectibility paragraph: classifying this as X
   lets us predict/explain/generalize Y, under conditions C, because
   mechanisms/network relations M stabilize the profile.
6. Add a cross-cutting measurement-validity section on comparisons: when a score
   licenses ranking model A above model B, when it does not, and what invariance
   assumptions must hold across tasks, model families, languages, users,
   annotators, evaluator systems, and deployment settings.
7. Add institutional-use constraints without making bias a fourth worked case:
   user of label, decision licensed, invalid inference, affected stakeholder,
   audit failure mode, and benchmark performativity.

## Reviewer-specific notes

### Laura Portwood-Stacer

Main concern: the paper needs a sharper antagonist and cleaner reader promise.
The typology should be presented as a tool for avoiding bad inferences, not as a
survey map.

Key move: write the intro around the recurring inference failure and add a
master table.

### John Ramsey

Main concern: the typology's classification rule is implicit. The paper must
explain why a term belongs in one box rather than another.

Key move: build an inference ladder from observation/output to score/label to
construct interpretation to kind attribution to governance/deployment use.

### Muhammad Ali Khalidi

Main concern: the relation between Boyd-style HPC and Khalidi-style
causal-network kindhood is still under-theorized. Mechanisms must explain
projectibility rather than replace it.

Key move: specify central properties, derivative properties, and recurrent
processes for the causal-network cases.

### Hasok Chang

Main concern: the measurement framing is too validation-theory centered and not
yet historical/pragmatic enough. Measurement practices co-evolve with
benchmarks, communities, instruments, and standards.

Key move: add an early measurement-practices section and a decision procedure
for productive pluralism.

### Inioluwa Deborah Raji

Main concern: accountability and institutional use are thin. The paper should
show how labels travel into product releases, procurement, regulation, release
gates, and audit claims.

Key move: add institutional-use and affected-stakeholder columns to the master
table.

### Percy Liang

Main concern: the typology is not yet evaluation infrastructure. It should
change scenario selection, metric selection, aggregation, reporting, uncertainty,
and deployment interpretation.

Key move: integrate HELM as ally and foil: holistic evaluation needs a theory of
which coverage axes and metrics matter.

### Alexandra Chouldechova

Main concern: the measurement apparatus is too verbal. The paper needs explicit
construct-to-score chains and a section on valid comparison.

Key move: add tables for construct, operational definition, instance population,
metric, score interpretation, intended use, projectible inference, and validity
threats.

### Iman Mirzadeh

Main concern: the capability case is too compressed. Reasoning, emergence, and
agency share a score-to-kind problem but fail in different ways.

Key move: rewrite the reasoning subsection around controlled variation:
GSM8K/GSM-Symbolic variants, GSM-NoOp distractors, clause-count sensitivity, and
what each reveals about score-to-capability inference.
