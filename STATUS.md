# STATUS

## Project

AI evaluation kinds. Framework / typology paper applying Boyd's HPC and Khalidi's causal-network kind theory to the vocabulary of AI evaluation and ML governance.

## Stage

Zero draft (2026-05-16). `main.tex` now builds to a 15-page framework draft, but
the current shape is underpowered and should not be polished locally without a
structural rethink.

## Working title

*From Scores to Kinds: Projectibility and Validity in AI Evaluation*
(provisional; re-title at polish).

## Working thesis

AI evaluation and governance vocabulary contains several kinds of kind-term. Some (*hallucination*, *jailbreak*) are HPC- or Khalidi-network candidates with identifiable sustaining mechanisms. Others (*reasoning*, *agency*, *emergence*) are capability-attribution terms whose projectibility depends on benchmark design and deployment context. Still others (*alignment*, *trustworthiness*) are umbrella governance constructs that organise lower-level kinds. The framework distinguishes these and explains why a single treatment of "what is X?" misfires.

## Scope decision

Framework paper first, with three worked cases (*hallucination*; *jailbreak/robustness*; *reasoning/emergence/agency*). *Alignment* and *trustworthiness* are umbrella constructs. Sycophancy is a pressure case for the alignment umbrella, not a fourth worked case. Standalone papers on individual terms come later if the HPC/Khalidi treatment changes an existing debate.

## Target venue

TBD. Candidates: *Minds and Machines*, *Philosophy & Technology*, *Synthese*, *AI & Society*. Decision deferred until paper structure is clearer.

## Carryovers / next actions

- Do not keep line-polishing the current zero draft. The next real move is a
  structural rewrite around the missing projectibility norm in AI evaluation:
  reliability can show that a result is stable; construct validity can show what
  it means in the measured setting; projectibility should say when the claim may
  travel across models, prompts, attacks, benchmarks, or governance uses.
- Demote the four-way typology from centrepiece to diagnostic tool. It should
  serve the reliability/validity/projectibility argument, not substitute for it.
- Deepen fewer cases rather than broadening the survey. Reasoning and
  alignment/sycophancy are the likely load-bearing cases; jailbreak is currently
  too thin, and hallucination is serviceable but mostly classificatory.
- Add Weinberger (2026), `weinberger2026HomeostasisCausalControl`, to the
  structural rewrite. It gives the missing distinction between stable benchmark
  behaviour and controlled robustness: benchmark reliability is not homeostasis;
  monitoring, red-teaming, release gates, retraining, and policy enforcement may
  be control-like stabilisers when they correct perturbations.
- Continue source verification before any submission-oriented pass. Some local
  bib entries were model-assisted and need authoritative checking.
- Decide whether to engage the existing AGI evaluation paper as predecessor or as
  a worked case within this framework.

### 2026-05-16 Session Notes

- Produced a real zero draft in `main.tex`: abstract, nine-section structure,
  central typology table, and compact worked cases for hallucination, jailbreak,
  reasoning/emergence/agency, and alignment/trustworthiness with sycophancy as a
  pressure case.
- Revised terminology and house style repeatedly: `\term{}` now carries
  conceptual uses; `\mention{}` is reserved for linguistic mention; `class`
  handles ordinary groupings, while `kind` is reserved for projectible classes.
- Removed `LLM-metry` as a freestanding coinage. The retained measurement point
  is now framed in terms of reliability, construct validity, score compression,
  and projectibility.
- Full-draft read left the paper feeling underwhelming. Diagnosis: the current
  draft is clear and tidy, but it mostly presents a typology of sensible
  distinctions. The stronger paper is about the missing projectibility norm:
  reliability and construct validity aren't enough to govern when AI evaluation
  claims may travel.
- Future session should start from that structural diagnosis rather than
  continuing local polish.

## Related projects in portfolio

- `papers/Moral_act-kinds_as_nodes_in_causal-normative_networks/` — sister project; same Boyd/Khalidi framework, different domain.
- `papers/AGI_evaluation_HPC/` — predecessor on AGI specifically (arXiv:2510.15236, under review at *Minds and Machines* per PORTFOLIO).
- `papers/What_do_we_mean_by_language/` — methodological cousin; pluralist map of a contested term.
