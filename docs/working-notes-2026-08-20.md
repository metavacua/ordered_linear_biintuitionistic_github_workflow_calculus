# Working notes, 2026-08-20 — informal conversational scaffolding

**Read the README and the two research documents first.** This document is
the informal, conversational origin material that motivated this
repository — worked examples, a GitHub-Actions-expression translation
exercise, a failure-mode taxonomy grounded in real CI data, and a
constructive/co-constructive property enumeration. It is **not**
peer-reviewed material, was **not** adversarially verified the way
`deep-research-report.md` was, and in at least one place is now known,
retrospectively, to overclaim something the deep-research run subsequently
refuted. Corrections are inserted inline, marked clearly, rather than
silently smoothed over — that's the whole discipline this repository is
supposed to practice on itself.

The originating context: a separate, unrelated engineering session
building a GitHub Actions CI pipeline (a Rust cross-target build-analysis
system) produced, as a side conversation, an extended discussion of whether
that pipeline's own mechanics (`needs:`, `${{ }}` expressions,
`continue-on-error`, artifact upload/download, `background`/`wait` steps)
could be read through a constructive/linear-logic lens. That conversation is
reproduced and organized below.

## 1. The GitHub Actions expression-language translation exercise

The prompt was to restate a preceding discussion of constructive witnesses,
singular succedents, and linear resources directly in GitHub Actions'
`${{ }}` expression syntax. The translation drew one honest boundary
throughout: `${{ }}` expressions only operate over already-materialized
scalars, strings, and small JSON blobs exposed as job/step `outputs` — they
cannot parse a compiler diagnostic or trace a span to a dependency's
registry path. That work has to happen in a general-purpose language (in
the originating pipeline, Python), which then re-exposes exactly one named
result as an output. The expression layer gates, compares, and passes along
conclusions that general-purpose code already produced; it does not derive
them.

**Singular succedent** — a job's own one conclusion, addressed as exactly
one value:

```yaml
${{ needs.build-attempt.outputs.batch-had-failure }}
${{ needs.discovery.outputs.batch-indices }}
```

`needs.<job>.outputs.<name>` names one thing, never an open disjunction —
the syntactic form of "one definite formula on the right of the turnstile."

**The turnstile itself** — `if:` as the literal syntactic realization of a
sequent's ⊢: a job only fires (derives its conclusion) if its stated
antecedent holds:

```yaml
if: ${{ needs.discovery.result == 'success' }}
```

**Weakening as a named structural rule** — `always()`/`!cancelled()` as the
weakening rule (discard a premise and proceed anyway), spelled out as
functions rather than left implicit:

```yaml
if: ${{ !cancelled() }}   # a downstream job runs regardless of any upstream job's conclusion
if: always()              # an upload step runs even if the step before it failed
```

**Joint failure as a raw conjunction — the classical, witness-free fact:**

```yaml
${{ needs.job-a.result == 'failure' && needs.job-b.result == 'failure' }}
```

This tells you nothing about *why*. It's the classical fact with no
constructive pair (in the Brouwer-Heyting-Kolmogorov sense) behind it yet.

**Extracting the witness — pushed to a general-purpose language, then
re-exposed as one output**, since `${{ }}` cannot trace a span itself:

```yaml
# inside a Python step:
#   culprit = trace_shared_dependency(error_sites_a, error_sites_b)  # "" if none found
- id: trace
  run: echo "shared-dependency-culprit=$CULPRIT" >> "$GITHUB_OUTPUT"
```

```yaml
${{ needs.indexing.outputs.shared-dependency-culprit != '' }}
```

That boolean is the constructed witness, re-admitted to the expression
layer as a singular succedent once it has been built — the `!= ''` check is
the only thing `${{ }}` contributes; the actual construction happened
upstream, in code.

**Shared linear resource, expressed as list membership** — `contains()` is
a real function (`contains(search, item)`), used here for "did A's and B's
derivations consume the same resource":

```yaml
${{ contains(fromJSON(needs.indexing.outputs.dependency-culprits-by-target)[matrix.target_a], 'socket2') &&
    contains(fromJSON(needs.indexing.outputs.dependency-culprits-by-target)[matrix.target_b], 'socket2') }}
```

> **Retrospective correction, 2026-08-20 (post deep-research):** the
> language used at this point in the original conversation — "the same
> linear resource consumed twice" — was not qualified carefully enough. The
> deep-research run's open questions flag exactly this: whether anything in
> GitHub Actions actually behaves as a *linear* (single-use) resource is
> unconfirmed, and artifacts specifically — re-downloadable arbitrarily
> within their retention window — structurally resemble the *exponential*
> (`!`, freely reusable) modality instead. The `contains()` pattern above is
> still a reasonable *membership check*; calling what it detects a "linear
> resource" specifically was an overclaim the later research walked back.
> "Shared antecedent fact" is the accurate, hedged description; "shared
> linear resource" is the claim this repository would need to actually
> establish, not assume.

**Vacuous succedent (doesn't depend on the antecedent at all)** — only
checkable by comparing the *same* output across every matrix leg, which
needs an aggregating job downstream (a single matrix leg can't see its
siblings):

```yaml
${{ join(fromJSON(needs.indexing.outputs.crate-type-canary-hashes-by-batch)) }}
```

— then, in general-purpose code, checking `len(set(hashes)) == 1`. An
identical value regardless of which target produced it is the operational
definition of "the antecedent contributed nothing." There is no single
`${{ }}` expression for "these were all equal across an arbitrary-length
list" — `contains`/`join` get the serialized list into view; the actual
uniqueness check needs real code, same as everything else that needed
parsing rather than gating.

**Independent (disjoint proof systems)** — the cleanest case, needing no
shared-resource machinery at all, because it's just two `needs:` edges into
two structurally different jobs with no expression ever comparing them:

```yaml
needs.build-attempt.result                     # a compiler-diagnostic verdict
needs.dependency-graph.outputs.deny-verdict     # a curated policy-scan verdict
```

Nothing ever writes `${{ needs.build-attempt... == needs.dependency-graph... }}`
for these two, because there's no proof-theoretic reason they should share
a resource — the *absence* of a comparison expression is itself the
syntactic mark of independence.

## 2. Mechanical and metamathematical properties this boundary implies

Five properties fall out of the expression-language/general-purpose-code
boundary described above, each with a real consequence for how a
diagnostic space gets partitioned:

1. **Decidability class.** The `${{ }}` grammar is closed, non-recursive,
   and quantifier-free — a fixed set of combinators (`==`, `&&`, `||`, `!`,
   `contains`, `startsWith`, `join`, `fromJSON`/`toJSON`, the status
   functions), no loop, no recursion, no user-defined function. Every
   expression evaluates in bounded work: no backtracking, no open-ended
   search, no possibility of non-termination. A general-purpose scripting
   layer has none of these restrictions. This is the precise sense in which
   the expression layer is a decidable, quantifier-free fragment and the
   scripting layer is the unrestricted computational one.
2. **Proof-irrelevance at the output boundary.** An expression can only see
   the *value* a job wrote to an output — never how it was derived. Two
   computations reaching the same boolean by entirely different reasoning
   are indistinguishable downstream. Consequence: a witness not explicitly
   re-exposed as its own named output is permanently unrecoverable to the
   gating layer, even though the code that found it still exists somewhere
   in a log.
3. **Referential transparency vs. earned determinism.** Expressions are
   pure — no side effects, a function only of already-fixed context state.
   Anything expressible purely in the expression layer is reproducible by
   construction, with zero verification burden. General-purpose code is not
   pure by default (registry fetches, subprocess calls, timing); its
   determinism has to be earned through explicit testing (rerun the same
   unmutated state twice, confirm byte-identical output) before a
   difference can be trusted as real rather than noise.
4. **Lexical, statically-checkable scoping.** An expression can reference
   `needs.X` only if `X` is literally declared in that job's own `needs:`
   list — checkable at parse time, before any runner executes anything.
   This is the same discipline as a sequent's context Γ: nothing outside
   the explicitly declared antecedent is available to the judgment.
5. **Monotone, immutable output store.** An output write cannot be
   retracted later in the same job or by any downstream job. A diagnostic
   classification computed once is a fixed, auditable fact for the rest of
   a run.

**The design rule this licenses:** push the minimum possible logic into the
unrestricted scripting layer — just enough to construct and name one
witness — and push everything else (comparison, gating, boolean
combination of already-named witnesses) into the expression layer, because
the expression layer's guarantees (termination, purity, static
checkability) are structurally free, while the scripting layer's
guarantees have to be earned via real verification every time.

## 3. A dependent / independent / vacuous failure-mode taxonomy, grounded in real CI data

Given a mechanically-established relationship between two things under
test — e.g., target A's feature set being a subset of target B's — there
are four possible pass/fail combinations for the same input tested against
both. Two of the four are worth real care:

- **Both fail.** This is not safe to treat as one data point. It needs a
  second, finer check: do the two failures cite the *same* error site/code?
  If yes, real corroboration. If the sites differ despite both being
  failures, that's two distinct problems sharing a pass/fail boolean, not
  one shared cause.
- **A passes, B fails, where A is a strict subset of B along the checked
  axis** ("failure out of proper order"). This is not directly explainable
  by the subset relationship — anything buildable under the *more*
  restrictive constraints should build under the less restrictive ones too
  — so when it happens anyway, it has one of three distinct causes, and
  conflating them is exactly how a real result becomes a misleading one:
  (a) the subset relationship itself was checked along an incomplete set of
  axes and doesn't actually hold globally; (b) a genuine, high-value
  environment/toolchain gap; (c) ordinary noise, needing a rerun to rule out
  before trusting it.

Three real examples, pulled from actual CI runs (a Rust cross-target build
pipeline, not this repository's own code — cited here only as worked,
concrete instances of the taxonomy):

- **Dependent, same mechanism, same target-property.** Two targets both
  reporting `std: false` in their real `rustc --print target-spec-json`
  output both produced the identical compiler diagnostic
  (`error[E0463]: can't find crate for 'core'`/`'std'`) when a build was
  attempted without any no-std adaptation. Single shared cause (the
  crate's own unconditional `std` dependency, not anything target-specific
  about either target individually); fixing the no-std conversion would
  resolve both simultaneously.
- **Dependent, same mechanism, but *not* via any target-lattice
  relationship at all.** Scanning real build output across a batch of
  twelve otherwise-unrelated targets — some WASM variants, some ARM
  Cortex-M microcontroller targets sharing no meaningful architectural
  similarity — eleven of them showed an identical second diagnostic,
  `error[E0583]: file not found for module 'sys'`, with its span pointing
  into a specific third-party networking dependency's registry source path.
  One target in the same batch (an Emscripten-based WASM variant) was
  exempt from *this specific* failure while still sharing the first,
  unrelated `std`-absence cause with the others. The real, traceable root
  cause was that one dependency lacked a platform backend for most, but not
  all, of the targets in the batch — a shared cause tied together by one
  package's own platform-support gap, not by any similarity among the
  targets themselves. Matching on error *code* alone would have missed
  this; only tracing the diagnostic's span back to the owning dependency's
  registry path revealed the real, shared mechanism.
- **Vacuous.** A separate build-configuration probe produced the identical
  error text — about the package's own crate-type declaration, not about
  any target property whatsoever — across every target checked, including
  two targets with completely different capability profiles. Seeing the
  same text repeat across targets here is not corroboration of anything
  real; it's the same non-target-specific fact reflected as many times as
  there are targets. The diagnostic procedure this implies: same code and
  message with *no correlation to any relevant capability field at all* is
  the operational signature of a vacuous, not a dependent, result.

## 4. A constructive / co-constructive critical review of the originating project's own CI and design documents

Applying the same two lenses back onto the originating pipeline's own
design documents (not this repository's) surfaced a real, historical
pattern worth recording here as a general methodological lesson, since it's
the actual origin of this repository's motivating question:

- **Where the discipline held:** a completeness check built as an explicit
  set-difference — `expected − actual`, required empty — rather than any
  attempt to *positively* prove "nothing was missed." The same algebraic
  move (subtraction), pointed in the opposite direction — requiring a
  remainder to be *non-empty* rather than empty — was separately used
  elsewhere in the same system to prove *progress* rather than
  *completeness*: one operator, two acceptance conditions, for two
  different proof obligations. A universal negative claim ("this process
  never performs a specific irreversible action") was likewise witnessed by
  constructing the literal match-set for that action and requiring it
  empty, rather than asserted without any corresponding check.
- **Where the discipline was violated, historically, and cost real time
  because of it:** a configuration flag was accepted by its tool without
  any error, and that silent acceptance was treated as if it were a
  positive witness that the flag had its intended effect — when in fact it
  had none, and the real, resolved configuration state (checked directly,
  later) still showed the untouched behavior the flag was supposed to
  suppress. Separately, and more subtly, a correctness-check function
  type-checked, ran without error, and returned a well-formed boolean on
  every real input for an extended period — while that boolean was
  unconditionally the "nothing to see here" value on *every* input, because
  of a data-shape mismatch between the function and its real input. It
  looked like a working, constructive check (tests passed) because its own
  test fixture had been shaped to match the same mismatched assumption,
  rather than shaped to match the tool's actual real-world output. A
  well-typed function that never actually fires under real conditions is a
  more dangerous failure than an assertion the design never bothered to
  make in the first place, precisely because it looks discharged.
- **A real, then-still-open gap surfaced by holding two similar-shaped
  claims to the same standard:** one universal negative claim in that
  project's design ("no CI job ever commits or pushes to the repository")
  had an explicit, mechanical, remainder-based check verifying it. A
  second, same-shaped universal negative claim in the same document ("a
  specific class of build attempt is never retried") had no such check
  anywhere — asserted, not witnessed, by the same standard the first claim
  was correctly held to.

The general lesson this repository takes from its own origin conversation:
**"accepted without error" is not a witness for "had the intended effect,"
and a function that type-checks is not a witness that it can ever produce
anything other than its default value.** Both are classical, not
constructive, moves dressed up as if they were the real thing. This
repository's own eventual formal work should hold itself to at least the
same standard it is proposing to formalize.
