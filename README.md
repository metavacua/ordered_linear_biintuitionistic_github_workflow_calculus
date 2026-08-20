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

Two findings from that same research run are load-bearing for the whole
project and are worth stating immediately, because they already correct
assumptions this project's own earlier conversational scaffolding made
in passing (see [`docs/working-notes-2026-08-20.md`](docs/working-notes-2026-08-20.md)
for the corrected discussion):

1. **GitHub Actions artifacts are almost certainly not linear resources.**
   An artifact is re-downloadable an arbitrary number of times within its
   retention window. Structurally, that is the *exponential* (`!`,
   "of course", freely reusable) modality of linear logic, not a
   single-use linear resource consumed exactly once. Any future claim in
   this repository that treats an artifact, or a fact derived from one, as
   a linear resource needs to confront this mismatch directly rather than
   assume it away.

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
- Given finding 1 above (artifacts ≈ exponential, not linear), is there
  *any* genuinely single-use, linear-resource-shaped concept in GitHub
  Actions' actual mechanics — and if not, does that sink the "linear"
  framing for GitHub Actions specifically, independent of whether it holds
  for the abstract calculus?
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
