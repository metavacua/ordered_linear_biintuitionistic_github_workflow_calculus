# Ordered Linear Bi-Intuitionistic GitHub Workflow Calculus

A research and development repository for the formal interpretation of GitHub
workflow syntax and mechanics as a linear constructive and linear
co-constructive logical programming language.

## Status: open research question, not an established result

This repository's founding thesis was tested, on 2026-08-20, by a 109-agent
adversarial deep-research run (full report:
[`docs/deep-research-report.md`](docs/deep-research-report.md)). The honest
result has to be stated up front, because it reframes everything else here:

> **Every one of the 14 claims that attempted to map a GitHub Actions
> concept — artifacts, jobs, `needs:`, actions composition, `safe-outputs`
> — onto linear-logic structure was refuted under adversarial
> verification (0–3 or 1–2 votes). Zero survived.** What *did* survive
> (11 confirmed findings, all high-to-medium confidence) is the pure,
> GitHub-free theoretical substrate such a bridge would need: linear
> logic's sequent-calculus proof theory, the categorical semantics of
> constructive vs. dual linear logic, multicategory/polycategory duality,
> and coinductive logic programming as the established referent for
> "co-constructive" logic programming.

So: the logical machinery this repository wants to apply is real, is
decades-to-recent peer-reviewed literature, and is well-verified in the
abstract. The application of that machinery to GitHub's actual workflow
syntax is **not** established anywhere in the literature searched. This
repository exists to do that work honestly — either to build a mapping that
survives the same adversarial standard the founding claims just failed, or
to characterize precisely *why* no such mapping exists, which is itself a
real, useful result.

Two points are load-bearing for the whole project and are worth stating
immediately. The second is a finding directly from that research run; the
first started as a research-run finding but needed a further scope
correction, which is stated in its corrected form below. Both already
correct assumptions this project's own earlier conversational scaffolding
made in passing (see
[`docs/working-notes-2026-08-20.md`](docs/working-notes-2026-08-20.md) for
the corrected discussion):

1. **Artifact linearity is a per-edge, per-workflow-graph property — not a
   category-wide verdict on "GitHub Actions artifacts" as a platform
   primitive.** The research run's original framing ("artifacts are
   almost certainly not linear resources," because an artifact is
   re-downloadable an arbitrary number of times within its retention
   window) conflated two different scopes. Re-downloadability is a
   capability of the *ambient platform* — GitHub Actions as a system is
   expressive enough to let any artifact be fetched by any number of
   consumers. That is a fact about the host system's ceiling, not a fact
   about how a *specific* artifact is actually used in a *specific*
   workflow's dependency graph. This is the same distinction the Chomsky
   hierarchy makes precise: a language's membership in a narrower class
   (say, regular) is not refuted by the fact that a more expressive host
   system (a Turing-complete language) is also capable of expressing or
   simulating it. A strictly-included class's intrinsic properties survive
   being embedded in a more powerful ambient system; they are not
   retroactively erased by that system's greater ceiling.

   The correct question is therefore per-edge and decidable by inspecting
   real call sites: for a given uploaded artifact, how many distinct
   `actions/download-artifact` invocations (across however many jobs)
   actually consume it in this specific workflow? In the pipeline that
   originally motivated this repository, both answers are observable
   today, side by side, in the same committed workflow file — counted
   directly from its real `actions/download-artifact` call sites, not
   inferred from its design documents: `dependency-graph-batch-N` is
   uploaded once per batch (by the `dependency-graph` job) and downloaded
   by exactly one job, `indexing`, via a wildcard
   `pattern: dependency-graph-batch-*` — a genuinely linear edge,
   single-use by construction. `target-capability-batch-N`, uploaded once
   per batch by the `target-capability` job, is downloaded by *two*
   distinct jobs — `build-attempt` (by exact name) and `indexing` (via a
   wildcard `pattern: target-capability-batch-*`) — a genuinely
   non-linear, exponential edge. Both are real, and they coexist in one
   graph, right now. "Are GitHub Actions artifacts linear?" is
   consequently the wrong-shaped question; "is this edge, in this graph,
   linear?" is the one with a decidable, mechanically checkable answer.

2. **The word "linear" in this repository's name is load-bearing, not
   decorative.** A verified (3-0) result traces a real theorem: adding
   co-exponentials to an ordinary cartesian closed category — i.e.,
   building bi-intuitionistic logic non-linearly — collapses the category
   to a single degenerate partial order, destroying all proof-theoretic
   content (Crolard 2001; Trafford 2016). This collapse is specifically
   avoided in **bi-intuitionistic *linear* logic** (Bellin 2014). That is
   the actual, cited reason a "constructive vs. dual vs. co-constructive"
   distinction has to be framed in a resource-sensitive (linear) logic at
   all, rather than an ordinary one — it is not a stylistic preference.

## Methodology note: what "14/14 refuted" actually demonstrates

The adversarial-verification method used in the deep-research run — three
independent skeptics per claim, kill on 2/3 refutes — is a
*literature-conformance* check: a claim survives only if a verifier can
find prior, citable, peer-reviewed support for it. That method is
well-suited to catching overclaims dressed as established fact. It is
structurally **unable** to confirm a claim that is true but genuinely
novel, because "genuinely novel" means no prior citable source yet states
it — there is nothing for a literature-conformance verifier to find. Run
that method against any first-correct instance of a new result and it
returns the same verdict a false claim would get: refuted, for want of a
citation.

This means "every one of the 14 claims mapping GitHub Actions concepts
onto linear-logic structure failed adversarial verification" is evidence
about a mismatch between *method* and *claim type* for at least some of
those claims — not evidence that no such mapping exists anywhere. The 14
attempts were, in every case the report describes, **top-down**: start
from an established linear-logic concept (an introduction/elimination
pair, a resource channel, combinatory structure, a resource-bounded
effect model) and ask whether some named GitHub Actions feature
instantiates it. The refutation evidence behind the 0-3/1-2 votes is not
uniform, though, and shouldn't be flattened into one story: some
refutations plausibly reduce to sheer absence of prior citable support
(the literature-conformance failure mode this section is about); at
least one — the artifacts claim — was refuted by a *substantive*
mechanical argument (re-downloadability implies the exponential, not
linear, modality) that the report's own open questions flagged as
possibly "the specific, unexamined reason the artifact-based claims
failed verification." Finding 1 above shows that argument itself was
scoped incorrectly — category-wide instead of per-edge — a third failure
mode distinct from both citation-absence and outright falsity: a real
mechanical observation, generalized past where it actually holds. All
three failure modes share the property that a top-down,
literature-checking method cannot by itself tell them apart; only tracing
the claim back to the real mechanics decides which one occurred.

The **converse** direction is the one this repository now treats as the
more productive path: start from GitHub Actions' own real, mechanically
observed structure — actual call sites, actual `needs:` edges, the actual
number of consumers a given artifact has in a given graph, the actual gap
between `steps.X.conclusion` and `steps.X.outcome` — and derive whatever
logical structure that evidence actually supports, rather than checking a
pre-selected logical concept against it. The corrected, per-edge
artifact-linearity result above is the first output of that method: it
did not start from "is there a linear resource here?" (the top-down
question the original 14 attempts asked and failed) — it started from
counting real `download-artifact` call sites in a real workflow, and only
afterward named the result using linear-logic vocabulary. The existing
linear logic, LFI/LFU, and bi-intuitionistic literature remains essential
to this repository — not as a verification oracle for authenticating
originality, but as the precise vocabulary this bottom-up derivation
borrows once it has already found something real to name.

## What "constructive," "dual," and "co-constructive" mean here

These are used precisely, not loosely, throughout this repository's
documents:

- **Constructive** — a positive claim is trustworthy only if the design
  produces an explicit, named, checkable *witness* — not the mere absence
  of a refutation (a tool accepting a flag without complaint; a function
  that type-checks and returns a well-formed value on every input while
  never actually firing under real conditions).
- **Dual / co-constructive** — a negative or universal claim ("nothing is
  missing," "X never happens") is trustworthy only if the design
  constructs the *remainder* between what's expected and what's found, and
  requires that remainder to be empty (or, for a progress claim, requires
  it to be non-empty) — the operational realization of co-Heyting
  subtraction, and, per finding 5 in the deep-research report, the same
  duality realized formally in coinductive logic programming
  (greatest-fixed-point semantics, dual to ordinary least-fixed-point /
  inductive logic programming).

## Research directions

### Logic of Formal Inconsistency (LFI) and Logic of Formal Undeterminedness (LFU)

LFIs (da Costa; formalized by Carnielli, Coniglio, Marcos) internalize
consistency at the object-language level via a consistency operator `○A`,
making explosion *local and controllable* rather than either forbidden
outright or unconstrained. LFUs (Marcos) are the paracomplete dual,
internalizing determinedness via a dual operator and controlling, in the
same localized way, where excluded middle is recovered. The technically
precise statement of the duality — worth stating exactly rather than
loosely — is that the *inference rules* excluded middle and explosion are
dual to each other; LFIs and LFUs are the systems built around
independently controlling each one. Full treatment, with citations and an
explicit accounting of what is and isn't established:
[`docs/lfi-lfu-reflexivity-memo.md`](docs/lfi-lfu-reflexivity-memo.md).

### Failures of reflexivity — an explicitly open, not-yet-established direction

The natural next question is whether LFI/LFU machinery corresponds to
failures of reflexivity — the sequent identity axiom `A ⊢ A`, an
accessibility relation failing to be reflexive, or a system's inability to
consistently self-report its own state. **Directed research found no
established literature connecting LFIs/LFUs to any of these** — on the
contrary, the identity/reflexivity axiom is standardly preserved even in
paraconsistent and paracomplete systems; LFIs/LFUs restrict explosion and
excluded middle, not reflexivity of entailment. This means: **a formal
LFI/LFU–reflexivity-failure correspondence would be a novel synthesis
original to this repository, not a result to cite as settled** — see the
memo for the one live, honestly-labeled engineering instance this
repository already has in hand (GitHub Actions' "honest-result" pattern,
where a job's own `conclusion` is not a trustworthy reflexive witness of
its real outcome, and a second, independent judgment reading `.outcome` is
required to recover it).

### Bi-intuitionistic foundations — build on the corrected literature

Cecylia Rauszer's original bi-intuitionistic sequent calculus and
completeness proofs are known to contain real errors, documented by Goré
and Shillito (2020) — mistakes in the deduction theorem and in the
completeness proofs, and Rauszer's claimed "cut-free" calculus does not
actually satisfy cut-elimination. This repository builds on the
*corrected*, post-2020 proof theory, not Rauszer's original papers
directly. It is also a useful, concrete illustration of this repository's
own governing standard: "the identity/reflexivity direction looks trivial
until someone actually checks it" is a real, recurring failure mode in
exactly this area of proof theory, not a hypothetical concern invented for
this project.

### Open questions carried forward from the deep-research run

- Does any strict, well-defined subset of GitHub Actions workflow YAML
  actually satisfy the uniform-proof restrictions that make goal-directed
  logic programming sound (avoiding unrestricted `∨`/`⊕`, `∃`, `⊗`, `!`),
  or does workflow syntax structurally require exactly the connectives
  that break goal-directedness?
- Finding 1 above already answers the narrower question this bullet
  originally asked (does *any* genuinely single-use, linear-resource-shaped
  edge exist in GitHub Actions' real mechanics) — yes, confirmed directly
  from the live workflow file: `dependency-graph-batch-N` has exactly one
  real consumer (`indexing`). The open question this sharpens into:
  is artifact-edge linearity **statically decidable from the workflow YAML
  alone** (counting `download-artifact` call sites syntactically), or does
  it require accounting for dynamic constructs — `matrix` expansion,
  `fromJSON`-indexed consumption, wildcard `pattern:` matches — that can
  make the real consumer count depend on values only known at run time? A
  static, syntax-only linearity checker would be directly useful (a lint
  flagging an artifact assumed single-use but actually fanned out to N
  consumers); whether one is possible in general, or only sound for a
  restricted syntactic subset, is unresolved.
- Do GitHub Actions jobs — multiple upstream `needs:` (multi-input),
  multiple downstream dependents (multi-output fan-out) — fit the
  multicategory (single-output/constructive) or polycategory
  (multi-input/multi-output/dual-classical) shape, and does the answer
  differ for reusable workflows (`workflow_call`) vs. ordinary jobs?
- Does anything in GitHub Actions' operational semantics (scheduled/cron
  triggers, `workflow_run` chains, a recursively self-retriggering
  pipeline) instantiate the coinductive/greatest-fixed-point side of the
  induction/coinduction duality, as opposed to the finite, terminating
  semantics an ordinary one-shot workflow run would suggest?

## Documents

- [`docs/deep-research-report.md`](docs/deep-research-report.md) — the full,
  unedited 109-agent adversarial research report this repository's founding
  thesis was tested against.
- [`docs/lfi-lfu-reflexivity-memo.md`](docs/lfi-lfu-reflexivity-memo.md) —
  the LFI/LFU research memo, with sources.
- [`docs/working-notes-2026-08-20.md`](docs/working-notes-2026-08-20.md) —
  informal working notes from the conversational session that motivated this
  repository: the GitHub Actions expression-language translation exercise,
  the dependent/independent/vacuous failure-mode taxonomy grounded in real
  CI examples, and the constructive/co-constructive design-property
  enumeration — explicitly labeled as informal scaffolding, not
  peer-reviewed material, and read *after* the corrections above, not
  before.

## License

This repository is dual-licensed:

- All documentation and prose (this README, everything under `docs/`) is
  licensed under **Creative Commons Attribution-ShareAlike 4.0
  International (CC BY-SA 4.0)** — see [`LICENSE-CC-BY-SA-4.0.txt`](LICENSE-CC-BY-SA-4.0.txt).
- Any code (workflow YAML, scripts, formal artifacts) added to this
  repository is licensed under the **GNU Affero General Public License
  v3.0 (AGPL-3.0)** — see [`LICENSE-AGPL-3.0.txt`](LICENSE-AGPL-3.0.txt).

See [`LICENSE.md`](LICENSE.md) for the full dual-licensing statement.

Copyright © 2026 Ian D.L.N. McLean.
