# STATUS

## Project

AI evaluation kinds. Framework / typology paper applying Boyd's HPC and Khalidi's causal-network kind theory to the vocabulary of AI evaluation and ML governance.

## Stage

Structurally rewritten draft (2026-07-02). `main.tex` builds to a 19-page draft
centred on the missing projectibility norm (reliability / construct validity /
projectibility), with the licence life-cycle (§4: generation, scope, narrowing,
erosion, expiry, defeat, revocation; misrecognition and maintenance as
cross-cutting axes) as the positive apparatus. The 2026-05-16 diagnosis is
implemented; the typology is now a diagnostic, not the centrepiece. Template
lessons imported from the moral-act-kinds sister paper (status-vs-uptake,
two-stage taxonomy, falsification conditions, dispute-relocation move).

## Working title

*From Scores to Kinds: Projectibility and Validity in AI Evaluation*
(provisional; re-title at polish).

## Working thesis

AI evaluation and governance vocabulary contains several kinds of kind-term. Some (*hallucination*, *jailbreak*) are HPC- or Khalidi-network candidates with identifiable sustaining mechanisms. Others (*reasoning*, *agency*, *emergence*) are capability-attribution terms whose projectibility depends on benchmark design and deployment context. Still others (*alignment*, *trustworthiness*) are umbrella governance constructs that organise lower-level kinds. The framework distinguishes these and explains why a single treatment of "what is X?" misfires.

## Scope decision

Framework paper first, with three worked cases (*hallucination*; *jailbreak/robustness*; *reasoning/emergence/agency*). *Alignment* and *trustworthiness* are umbrella constructs. Sycophancy is a pressure case for the alignment umbrella, not a fourth worked case. Standalone papers on individual terms come later if the HPC/Khalidi treatment changes an existing debate.

## Target venue

Shortlist set 2026-07-03 (venue-selection screen). **Primary: *Minds and
Machines*** — best journal-reader match: the first two pages (Wei/Schaeffer,
Raji, inference licences) already carry the contract for philosophy-of-AI
readers, and the predecessor AGI paper under review there signals programme
fit. Concurrency with the AGI submission is a timing question, not a bar:
decide at submission-gate time; if the AGI decision has landed, M&M is
unambiguous; if still pending, either submit anyway (distinct manuscripts) or
use the first backup to decorrelate.
**Backup 1: *Philosophy & Technology*** — strong for the governance side
(thin verdicts, coordination regimes, licence statements), but would want the
intro reweighted toward trustworthy-AI/governance so the first two pages carry
that contract. **Backup 2: *Synthese*** — the kind-theoretic machinery fits,
but referees there would demand deeper validity-theory engagement
(Messick/Borsboom) and may read §§7–8 as applied; slower pipeline; sister
moral-act-kinds paper already targets it. *AI & Society* dropped except under
a full governance reframing. Before any submission: CrossRef recent-issue
survey of the chosen venue (per venue-outcomes standing lesson: run the
desk-editor screen before first submission).

## Carryovers / next actions

- Done 2026-07-02: structural rewrite (see Stage); Weinberger integrated as the
  maintenance/control stage (§4.3, §7); Goodman cited at first mention of
  projectibility (house rule; also fixed in the moral-act-kinds draft); Ryle
  1949 added as pedigree for "inference licence"; Bareinboim & Pearl 2016 added
  (verified) for the transportability differentiation (§3, §9); AGI paper
  engaged as predecessor with one sentence in §6 (`reynolds2025agi`);
  acknowledgements corrected to models actually used; keywords added.
- Brett to read and judge the rewrite: does the licence life-cycle carry the
  paper, and do the two deep cases (hallucination structure; capability
  narrowing/erosion) hold up?
- Add Groeger, Wen, and Brbic (2026) as a methods case for the missing
  projectibility norm in AI evaluation. Central note:
  `../../../literature/groeger_wen_brbic_2026_aristotelian_representation_hypothesis.notes.md`.
  Their result is a compact example: representation-similarity claims across
  model scale, architecture, or modality do not travel until width/depth and
  aggregation confounds are calibrated away. Natural home: §6 (capability
  licences), as a narrowing example beyond GSM-Symbolic.
- Continue source verification before any submission-oriented pass. Some local
  bib entries were model-assisted and need authoritative checking.
- Re-title at polish: current title over-promises "kinds" (the paper argues most
  of these terms aren't kinds); candidates should foreground the licence
  life-cycle or the missing norm.
- Bib hygiene: ~30 keys are duplicated between the central bib and
  `references-local.bib` (benign biber warnings; biber uses the central
  copies). Prune local duplicates at `/push-bib` time.
- The moral-act-kinds paper and this one now share an unpublished structural
  template; cross-cite once either is public so they read as one programme.

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
