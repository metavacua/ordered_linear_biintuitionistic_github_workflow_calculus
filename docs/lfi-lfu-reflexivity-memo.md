# Research memo: Logics of Formal Inconsistency, Logics of Formal Undeterminedness, and the reflexivity-failure question

**Run date:** 2026-08-20
**Method:** single-agent, real-source research (WebSearch/WebFetch), not
adversarially multi-verified in the same way as the deep-research report in
this directory — treat confidence markers accordingly. Reproduced here
close to verbatim, since its hedging is precise and load-bearing.

## Logics of Formal Inconsistency (LFI)

Founded on Newton da Costa's paraconsistent tradition and formalized by
Walter Carnielli, Marcelo Coniglio, and João Marcos, LFIs are paraconsistent
logics that internalize consistency *at the object-language level* via a
unary consistency operator, `○A` ("A is consistent") — see Carnielli,
Coniglio & Marcos, ["Logics of Formal Inconsistency"](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=7746fe65efb386f6226c9116145b1495b7b79d15);
Carnielli & Coniglio, *Paraconsistent Logic: Consistency, Contradiction and
Negation* (Springer, 2016). The core move: negation is made non-explosive
(a bare contradiction `A, ¬A` does not entail arbitrary `B`), but the system
is only *gently* explosive — adjoining `○A` to a contradictory pair `A, ¬A`
*does* recover full classical explosion. Inconsistency is thereby localized
and made formally expressible, rather than either forbidden outright
(classical logic) or left completely unconstrained.

## Logics of Formal Undeterminedness (LFU)

Introduced by Marcos as the paracomplete mirror image: propositions split
into determined and undetermined ones, and a theory may contain `A` with
neither `A` nor `¬A` derivable. A dual connective (often written `★` or
`∘`) marks a proposition as determined, recovering the principle of
excluded middle in a controlled way for exactly the propositions so marked.

**The technically precise statement of the duality — worth stating exactly
rather than loosely:** it is *not* that "LFI and LFU are dual logics" in
some blanket sense, nor that PEM and non-contradiction are dual *formulas*.
It is that the two *inference rules*, excluded middle (PEM) and explosion
(EXP), are dual to one another, and LFI/LFU are the systems built around
independently controlling each. Combined systems (LFIU) control both
simultaneously. See Carnielli, Coniglio & Marcos on recovery operators and
duality: ["Recovery operators, paraconsistency and duality"](https://www.cle.unicamp.br/prof/coniglio/Recovery.pdf).

**Provenance note, carried forward honestly:** the exact primary citation
for Marcos's original LFU paper (title, year) was not directly fetched in
this research pass — search results describe it as "introduced by Marcos in
2005" without a directly-verified primary source. Track down the exact
paper (plausibly a dedicated LFU paper, or discussed within Marcos's broader
"paranormal logics" work) before citing a specific year/title as
established.

## The reflexivity-failure question

**The literature gives a clear, negative-leaning answer, and it matters to
say so plainly rather than force a correspondence.**

Reflexivity failure can mean several different things:

- (a) the sequent calculus identity axiom `A ⊢ A` failing to hold
  unrestrictedly (loss of the reflexivity of entailment);
- (b) an accessibility relation or preorder failing to be reflexive in some
  Kripke- or algebraic-style semantics;
- (c) self-reference and Löb's theorem / the diagonal lemma;
- (d) a category-theoretic identity natural transformation failing at some
  object.

Direct search found no established LFI/LFU literature built around any of
these. On the contrary, one search result states plainly:

> "The identity/reflexivity axiom typically remains valid even in most
> paraconsistent systems."

LFIs and LFUs restrict *explosion* and *excluded middle*, not the
reflexivity of entailment itself; `A ⊢ A` is standardly preserved even as
non-contradiction or excluded middle are locally suspended. On the
self-reference angle (c), there is real, adjacent work on paraconsistent/
partial logics *tolerating* self-reference and Löb-style obstacles without
collapsing (background: the [diagonal lemma](https://en.wikipedia.org/wiki/Diagonal_lemma)
and the Stanford Encyclopedia of Philosophy's ["Self-Reference and Paradox"](https://plato.stanford.edu/entries/self-reference/)),
but this is about paraconsistency being a *tool for handling* self-reference
gracefully, not a claim that LFIs/LFUs are themselves *defined by* a
reflexivity failure.

**This means: a formal correspondence between LFI/LFU and "failure of
reflexivity" is not an established result to cite — it would be a
genuinely novel synthesis specific to this repository's own project, and
should be framed and pursued as such, not asserted as settled.**

## An adjacent, honestly-caveated thread: bi-intuitionistic logic's own history of errors

The repository's name invokes *bi-intuitionistic* logic (the union of
intuitionistic logic and its dual, co-intuitionistic logic), introduced by
Cecylia Rauszer with a Hilbert calculus, algebraic, and Kripke semantics,
restricting sequents to a single formula on the left *or* the right. Worth
knowing going in: Rauszer's original sequent calculus and completeness
proofs were later found to contain real errors — Goré and Shillito (2020)
documented mistakes in her account of the deduction theorem and in her
completeness proofs, and her "cut-free" calculus has since been shown to
actually fail cut-elimination. The field has spent real effort rebuilding
solid foundations since:
["A proof-theoretic study of bi-intuitionistic propositional sequent calculus"](https://cs.ioc.ee/~tarmo/papers/pinto-uustalu-jlc18.pdf);
[Gore & Postniece, "Combining Derivations and Refutations for Cut-free..."](https://users.cecs.anu.edu.au/~linda/GorePostniece_GBiInt.pdf).

This isn't a reason to avoid the bi-intuitionistic framing — it's a reason
to build on the *corrected*, post-2020 literature rather than Rauszer's
original papers directly, and a concrete illustration that "the identity/
reflexivity direction looks trivial until someone actually checks it" is a
real, recurring failure mode in this exact area of proof theory, not a
hypothetical concern.

## A genuine research direction for this repository, stated as a project-specific novel synthesis rather than an established fact

GitHub Actions' honest-result pattern (a step marked
`continue-on-error: true` whose real outcome is only recoverable via an
explicit, separate assertion reading `steps.X.outcome`, never
`steps.X.conclusion`) is a live engineering instance of exactly the
reflexivity-failure question the literature leaves open — the job's own
self-report (`conclusion`) is *not* trustworthy as a reflexive witness of
its own state; a second, independent judgment is required to recover it.
Whether this is fruitfully formalized as an LFI-style consistency operator
(`○(job succeeded)` recoverable only via the explicit assertion step), an
LFU-style determinedness operator, or a bespoke reflexivity-failure
connective is exactly the open design question this repository exists to
work out — not something to import from the literature as already solved.

## Sources

- Carnielli, Coniglio & Marcos, ["Logics of Formal Inconsistency"](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=7746fe65efb386f6226c9116145b1495b7b79d15)
- Carnielli & Coniglio, *Paraconsistent Logic: Consistency, Contradiction and Negation*, Springer, 2016
- Carnielli & Coniglio, ["Recovery operators, paraconsistency and duality"](https://www.cle.unicamp.br/prof/coniglio/Recovery.pdf)
- ["On formal aspects of the epistemic approach to paraconsistency"](https://www.cle.unicamp.br/prof/coniglio/LETJ.pdf)
- Diagonal lemma / self-reference: [Wikipedia](https://en.wikipedia.org/wiki/Diagonal_lemma), [Stanford Encyclopedia of Philosophy, "Self-Reference and Paradox"](https://plato.stanford.edu/entries/self-reference/)
- Bi-intuitionistic logic history and corrections: Goré & Shillito (2020) on errors in Rauszer's original completeness proofs and deduction theorem; ["A proof-theoretic study of bi-intuitionistic propositional sequent calculus"](https://cs.ioc.ee/~tarmo/papers/pinto-uustalu-jlc18.pdf); [Gore & Postniece, "Combining Derivations and Refutations for Cut-free..."](https://users.cecs.anu.edu.au/~linda/GorePostniece_GBiInt.pdf)
- Stanford Encyclopedia of Philosophy, ["Paraconsistent Logic"](https://plato.stanford.edu/entries/logic-paraconsistent/)
