# Deep-research report: GitHub workflow syntax as linear constructive / dual / co-constructive logic

**Run date:** 2026-08-20
**Method:** 109-agent adversarial deep-research workflow (parallel web-search
fan-out across 5 angles → fetch and extract falsifiable claims from top
sources → 3-vote adversarial verification per claim, requiring 2/3 refutes to
kill a claim → merge semantic duplicates, rank by confidence, cite sources).
**Research question, verbatim, as submitted:**

> A canonical interpretation of github workflow syntax or a strict subset or
> a strict class or a strict category as linear constructive logical
> programming vs dual linear constructive logical programming and linear
> co-constructive logical programming.

This document reproduces the workflow's full synthesized output verbatim
(summary, all six merged findings, caveats, and open questions), exactly as
returned, with no edits to the substance.

## Summary

The research does not establish a canonical interpretation of GitHub
workflow (Actions) syntax as linear constructive vs. dual/co-constructive
logic programming: every claim that attempted to map workflow concepts
(artifacts, jobs, actions, safe-outputs, or the githubnext "agentic
workflows"/gh-aw product) onto linear-logic structure was refuted by
adversarial verification (14/14 refuted, votes 0-3 or 1-2), so no confirmed
evidence bridges GitHub's syntax to this logical framework. What did survive
verification is the pure theoretical substrate such a bridge would need:
(1) sequent-calculus proof search motivates restricting which linear
connectives (⊕/∨, ∃, ⊗, !) can appear unrestricted in goal-directed logic
programming, with Forum shown as a complete dual-connective presentation of
full linear logic from which everything else is definable; (2) the
categorical semantics of "constructive vs. dual" is formalized via closed
symmetric monoidal categories (intuitionistic/constructive linear logic)
embedding fully and conservatively into *-autonomous categories
(classical/dual linear logic) — and, crucially, this well-behaved embedding
is linear-logic-specific: the general (non-linear) bi-intuitionistic case is
known to collapse to a degenerate partial order, which is the one confirmed
result that actually explains why the research question insists on "linear";
(3) polycategories are the multi-input/multi-output, classical/dual
generalization of multicategories (single-output, intuitionistic/
constructive), correspondingly biequivalent to *-autonomous categories; and
(4) "co-constructive logic programming" has a concrete existing referent —
coinductive logic programming, formally dual to ordinary (inductive/
constructive) logic programming via the coalgebra/algebra and greatest-/
least-fixed-point dualities, with its own dedicated proof theory (coinductive
uniform proofs, CUP). In short: the logical machinery needed for a "linear
constructive vs. dual/co-constructive" reading of some formalism exists and
is well-verified in the abstract, but no verified claim in this research
connects that machinery to GitHub workflow syntax specifically — the
workflow-facing half of the question remains unanswered by this evidence
base.

## Findings

### Finding 1 — No confirmed bridge from GitHub Actions to linear logic (refuted, 14/14)

**Claim:** No confirmed evidence supports interpreting GitHub workflow
(Actions) syntax, or any strict subset/class of it, as linear constructive,
dual, or co-constructive logic programming. Every claim attempting this
bridge — artifacts as introduction/elimination (construction/consumption)
pairs, artifacts as the linear-resource channel across job boundaries,
jobs/actions composition as combinatory structure, safe-outputs as a
resource-bounded (linear-logic-like) effect model, and the githubnext
"agentic workflows" natural-language-to-YAML compilation as a construction
step — was refuted (0-3 or 1-2 votes). Two of the refuted claims concern a
distinct product (githubnext's agentic-workflows / gh-aw CLI) rather than
GitHub Actions YAML proper, so even that adjacent surface failed to yield a
confirmed link.

- **Confidence:** high
- **Vote:** 0-3 / 1-2 across 14 distinct refuted claims; none survived
- **Sources:** [GitHub Actions: Workflows and actions](https://docs.github.com/en/actions/concepts/workflows-and-actions), [Workflow artifacts](https://docs.github.com/en/actions/concepts/workflows-and-actions/workflow-artifacts), [githubnext Agentic Workflows](https://githubnext.com/projects/agentic-workflows/)
- **Evidence:** Direct tally from the refuted-claims list: every claim naming
  a GitHub Actions or agentic-workflow concept failed adversarial
  verification, while every claim that survived (the 11 confirmed claims,
  merged below into findings 2-6) is drawn exclusively from linear-logic,
  sequent-calculus, or category-theory sources with no GitHub content at
  all. The refutation demonstrates that these particular proposed mappings
  do not hold up under scrutiny — it does not prove no valid interpretation
  could exist, only that none was established by this research.

### Finding 2 — Bi-intuitionism collapses non-linearly; the linear case is the exception

**Claim:** The categorical distinction between "constructive" and
"dual/co-constructive" logic is well-behaved specifically in the linear
setting: for cartesian closed categories (models of ordinary
constructive/intuitionistic logic), adding co-exponentials to represent
co-implication (bi-intuitionism) collapses the category to a single partial
order, destroying proof-theoretic content — except this collapse is
explicitly avoided in bi-intuitionistic LINEAR logic. This is the one
confirmed result that directly explains why a "constructive vs. dual vs.
co-constructive" distinction would need to be framed in a linear
(resource-sensitive) logic rather than an ordinary one.

- **Confidence:** high
- **Vote:** 3-0
- **Sources:** [Trafford, "Structuring Co-constructive Logic for Proofs and Refutations," Logica Universalis (2016)](https://www.researchgate.net/publication/293194966_Structuring_Co-constructive_Logic_for_Proofs_and_Refutations)
- **Evidence:** Verbatim-quoted from Trafford (2016), tracing the collapse
  theorem to Crolard's peer-reviewed "Subtractive logic" (TCS 2001) and the
  linear-logic exception to Bellin's "Categorical proof theory of
  co-intuitionistic linear logic" (arXiv 2014); independently corroborated
  by unrelated secondary sources describing the same "degenerates to a
  preorder" result and linear-logic escape route.

### Finding 3 — Constructive linear logic embeds fully and conservatively into dual (classical) linear logic

**Claim:** The constructive-vs-dual distinction in linear logic programming
has a formal categorical-semantic realization: closed symmetric monoidal
categories (models of intuitionistic/constructive linear logic) embed
fully — preserving tensor and internal-hom structure — into *-autonomous
categories (models of classical/dual linear logic with involutive negation),
and this embedding is furthermore 2-categorically conservative for any
{0,⊤}-free MALL fragment over its intuitionistic IMALL counterpart. I.e.,
the "constructive" fragment is not merely definable inside the "dual"
fragment but sits inside it faithfully, without collapse or loss of
provability.

- **Confidence:** high
- **Vote:** 3-0 (both facets, same paper)
- **Sources:** [Shulman, "*-Autonomous Envelopes and Conservativity," TLLA/EPTCS (2020)](https://arxiv.org/pdf/2004.08487)
- **Evidence:** Both facets (full embedding; 2-categorical conservativity)
  come from the same peer-reviewed paper and are two statements of one
  result: Theorem 8.1 (conservativity) is derived from the explicit
  embedding construction (Theorem 2.1 plus the envelope/double-gluing
  argument). Merged here since they are facets of a single theorem rather
  than independent claims.

### Finding 4 — Multicategories (constructive) and polycategories (dual/classical)

**Claim:** Multicategories model the single-output ("constructive"/
intuitionistic) fragment of categorical proof theory, while
polycategories — introduced by Szabo specifically to extend the
multicategory/intuitionistic-sequent-calculus correspondence to full
classical (multi-input, multi-output) sequent calculus — model the
"dual"/classical fragment; a polycategory equipped with the relevant
universal objects (tensor, par, dual) corresponds precisely (a
2-equivalence) to a *-autonomous category, mirroring the
multicategory/monoidal-category correspondence on the constructive side.

- **Confidence:** medium
- **Vote:** 2-1 (historical/motivation half) and 3-0 (correspondence-theorem half)
- **Sources:** [Blanco, PhD thesis (arXiv 2305.15139)](https://arxiv.org/pdf/2305.15139)
- **Evidence:** Both parts verified against Blanco's thesis, corroborated
  independently for the correspondence theorem by the Cockett-Seely/Shulman
  literature and nLab. Confidence capped at medium because the
  framing/historical half (Szabo's motivation, multicategory=intuitionistic
  vs. polycategory=classical) only reached a 2-1 adversarial vote, not
  unanimous.

### Finding 5 — Coinductive logic programming as the concrete referent for "co-constructive"

**Claim:** "Co-constructive logic programming" has a concrete existing
formal referent: coinductive logic programming (CoLP), which is dual to
ordinary (inductive/constructive) logic programming in two
independently-verified senses — (a) algebraically, a ground Horn-clause
program is literally a coalgebra for the PfPf endofunctor on Set, the
categorical dual of the standard inductive/algebraic least-Herbrand-model
reading, and induction/coinduction generally correspond to least-fixed-point
(initiality+minimality) vs. greatest-fixed-point (maximality) semantics; and
(b) proof-theoretically, coinductive Horn-clause resolution has been recast
as a dedicated system of coinductive uniform proofs (CUP), replacing prior
ad hoc cycle-detection with a uniform framework extending
Miller-Nadathur's logic-programming hierarchy.

- **Confidence:** high
- **Vote:** 3-0 on each of three underlying claims
- **Sources:** [Komendantskaya, Power, Schmidt et al. (arXiv 1312.6568)](https://arxiv.org/pdf/1312.6568), [Gupta et al., "Infinite Computation, Co-induction and Computational Logic"](https://www.researchgate.net/publication/227053497_Infinite_Computation_Co-induction_and_Computational_Logic), [Basold, Komendantskaya, Li, "Coinduction in Uniform Proofs," ESOP (2019)](https://link.springer.com/chapter/10.1007/978-3-030-17184-1_28)
- **Evidence:** Merges two claims asserting the same algebra/coalgebra-LFP/GFP
  duality from independent primary sources, plus the CUP proof-theory
  result. Caveat: the initiality/minimality-vs-maximality quote was
  corroborated partly via search-snippet cross-checking rather than a
  from-scratch full PDF read, a slightly weaker verification path than the
  other two sources in this group.

### Finding 6 — Forum and the connective restriction in goal-directed linear logic programming

**Claim:** Sequent-calculus proof search supplies the design rationale for
restricting which linear connectives a goal-directed logic-programming
language may use unrestricted (excluding ∨/⊕, ∃, ⊗, ! because they break
uniform proofs), while Forum is presented as recovering all of linear
logic — including these excluded, "dual" connectives — by restricting to a
different unrestricted base {∀, ⊸, ⇒, &, ⊤, ℘, ⊥} and defining every other
connective (including the classical/dual ones) via De Morgan-style duality
from that base.

- **Confidence:** medium
- **Vote:** 3-0 (all three underlying claims)
- **Sources:** [Miller, WoLLIC lecture slides](https://www.lix.polytechnique.fr/~dale/papers/wollic03.pdf)
- **Evidence:** All three claims trace to a single primary source that is a
  lecture-slide deck rather than peer-reviewed proceedings (flagged by the
  verifier), though the connective-restriction claim is independently
  corroborated by two additional foundational peer-reviewed papers by the
  same author (Hodas & Miller, "Logic Programming in a Fragment of
  Intuitionistic Linear Logic"; Miller, "A Uniform Proof-Theoretic
  Investigation of Linear Logic Programming") and the Forum-completeness
  claim traces to Miller's peer-reviewed 1996 JLC/TCS "Forum" paper. Held at
  medium rather than high because the direct citation base for this
  synthesis is the single slide deck, not those corroborating papers
  themselves.

## Caveats

The research question is itself underspecified: "a strict subset or a
strict class or a strict category" of GitHub workflow syntax is never
operationalized in any surviving claim, so it's impossible to say which
fragment of Actions YAML (if any) the confirmed logical machinery might
apply to. The core gap is structural, not incidental: all 11 confirmed
claims are pure logic/category-theory results with zero GitHub content, and
all 14 refuted claims are exactly the ones that tried to name a GitHub-side
counterpart — meaning the theory-to-workflow bridge is entirely
unestablished by this research, not merely weakly evidenced. Several
findings rest on a single primary source (the Miller WoLLIC slide deck for
Finding 6; the Trafford paper alone for the collapse/exception result in
Finding 2, though its central theorem is independently traceable to Crolard
2001 and Bellin 2014). The polycategory/multicategory finding is capped at
medium confidence because its historical-motivation half only achieved a
2-1 adversarial vote. Two "refuted" sources (githubnext agentic-workflows)
describe a different, adjacent product (an experimental natural-language-
to-YAML compiler with its own CLI) rather than GitHub Actions YAML proper,
so their refutation says nothing about Actions itself either way. None of
the confirmed mathematical results (linear logic duality, *-autonomous
categories, polycategories, coalgebraic logic programming) are
time-sensitive or contested; they are stable, decades-old-to-2023
categorical/proof-theoretic literature, so currency is not a concern for
the confirmed half — the risk is entirely in the (unestablished)
application to GitHub syntax.

## Open questions

- Does any strict, well-defined subset of GitHub Actions/workflow YAML
  actually satisfy the uniform-proof restrictions identified in Finding 6
  (i.e., can workflow steps be read as goal-directed derivations that avoid
  unrestricted ∨/⊕, ∃, ⊗, ! in a way that would make a logic-programming
  reading sound), or does workflow syntax structurally require exactly the
  connectives that break goal-directedness?
- Are GitHub Actions artifacts actually linear resources in the technical
  sense assumed by every refuted claim? Artifacts are re-downloadable an
  arbitrary number of times within their retention window, which
  structurally resembles the exponential/reusable (!) modality rather than
  a single-use linear resource — this mismatch may be the specific,
  unexamined reason the artifact-based claims failed verification, and
  would need to be resolved before any linear-logic reading of artifacts
  could succeed.
- Do GitHub Actions jobs — which can have multiple upstream `needs`
  dependencies (multi-input) and produce multiple downstream outputs
  (multi-job fan-out) — structurally fit the multicategory
  (single-output/constructive) or polycategory
  (multi-input/multi-output/dual-classical) shape identified in Finding 4,
  and would that classification differ for reusable workflows vs. ordinary
  jobs?
- Does anything in GitHub Actions' operational semantics (e.g.,
  scheduled/cron-triggered workflows, long-running services, or
  self-retriggering workflows) instantiate the coinductive/greatest-fixed-
  point side of the induction/coinduction duality found in Finding 5, as
  opposed to the finite, terminating (least-fixed-point) semantics that
  ordinary one-shot workflow runs would suggest?
