# Case Study 01: When More Metadata Made the Recommender Worse

## Executive summary

K-Radar is a personal television and film discovery system. During normal use, its highest-confidence recommendation bucket became overwhelmingly dominated by anime even though the visible taste profile was broad across science fiction, drama, action, comedy, and other content families.

The first two explanations were plausible and real: inferred media format was adding recommendation weight, and the literal `anime` genre label was acting as another positive signal. Removing both improved the model but did not solve the product behavior.

The deeper problem was structural. Anime titles in the broader catalogue carried denser genre metadata than television and movies. Because every matched genre contributed independently, a densely tagged title had more opportunities to intersect the user's preferences and therefore became "louder" simply because it was described in greater detail.

That led to the product principle:

> More genre tags should describe a title more precisely, not make it louder.

The scorer was changed so inferred genre matches share a fixed candidate-side evidence budget rather than each receiving full independent weight. A later pass then separated **honest candidate scoring** from **useful active-slate composition**, because even a fair score can produce an unhelpful feed when one media kind has much more qualifying supply.

This case study is less about anime than about a recurring AI-product problem: apparently reasonable features can become hidden proxy signals, and fixing the first proxy does not mean the underlying behavior is corrected.

## Context

K-Radar maintains a user taste model from explicit reactions and inferred evidence, then generates Discover recommendations with classifications such as Strong, Adjacent, and Wildcard.

The product was already showing a relatively broad inferred taste profile. In one observed state, the strongest visible content families included science fiction, drama, action, and comedy, while Anime was present but not dominant.

Discover told a different story.

**Observed Strong bucket: 44 anime recommendations out of 48.**

The important product question was not "How do we make fewer anime recommendations?" It was:

**Why does the ranking behave as though the user has an overwhelming medium preference when the visible evidence says otherwise?**

That framing prevented the obvious but bad solution: imposing an arbitrary anime quota.

## Pass 1: the format hypothesis

The first hypothesis was that inferred media format was acting as an extra positive accelerator.

A simplified candidate comparison looked like this:

- TV candidate: science fiction + drama + action
- Anime candidate: science fiction + drama + action + inferred anime format

If both matched the same content preferences, the anime candidate could still receive another positive dimension simply for being anime-shaped.

### Product rule

Inferred media format should remain useful for metadata, filtering, and explicit user steering, but it should not independently increase recommendation score or confidence.

Explicit direct preferences were preserved. If the user deliberately says they prefer or dislike Anime, that choice should matter.

### Result

The fix was technically correct.

The product behavior barely changed.

After repackaging, the Strong bucket was still approximately **44 anime out of 48**.

That was the important moment in the investigation. Passing tests did not end the task because the actual user-facing behavior was still wrong.

## Pass 2: the wrapper-genre hypothesis

A read-only diagnostic showed why the first fix had not moved the distribution.

No `format:*` reason codes remained in the Strong recommendations. Instead, the dominant reason was the literal inferred `genre::anime` signal.

That label was being treated as though it were an ordinary content genre, alongside science fiction, drama, comedy, mystery, and similar dimensions.

But "anime" is primarily a medium/category wrapper. It says much less about story content than "political thriller", "science fiction", or "character drama".

### Product rule

Inferred `genre::anime` should not count as positive content evidence by default.

Again, explicit user steering remained intact. If the user directly prefers or dislikes Anime, that is a deliberate choice and should continue to influence results.

### Result

The skew improved, but remained substantial:

**approximately 39 anime out of 48 Strong recommendations.**

The second hypothesis had also been real, and also incomplete.

## Pass 3: structural metadata-density bias

The next diagnostic compared metadata density across the catalogue.

The broader corpus showed a structural difference:

- Anime titles carried more approved broad genre facts on average.
- TV titles carried fewer.
- Movies were thinner still.
- The current Strong anime recommendations were especially dense.

The scorer treated every matched inferred genre as another independent positive contribution.

That meant a title with four legitimate genre labels had four opportunities to intersect the user's preferences, while an equally relevant title represented by two labels had only two.

Nothing had to be mislabeled for the system to become biased.

The metadata itself was uneven.

### The core insight

**Descriptive density had accidentally become recommendation volume.**

That is a generalizable product failure. Any recommendation, search, or ranking system that consumes heterogeneous metadata can reward the objects that are documented most richly rather than the objects that are actually the best fit.

### Product rule

> More genre tags should describe a title more precisely, not make it louder.

Each candidate receives a fixed inferred-genre evidence budget.

Conceptually:

- 1 scoring-relevant genre: that genre can contribute the full genre mass.
- 2 scoring-relevant genres: each receives half.
- 10 scoring-relevant genres: each receives one tenth.
- Matching 6 of those 10 produces 0.6 of the available genre mass, not six full independent boosts.

Important safeguards:

- Explicit direct user preferences are not diluted.
- The literal inferred `anime` wrapper remains excluded.
- Genres the user has no evidence about do not dilute genuine matches.
- Machine/why-tag evidence remains a separate channel.
- Explanation reason codes still identify the content dimensions that actually matched.

### Result

After genre-mass normalization, the observed Strong bucket moved again:

**approximately 36 anime out of 48.**

The scoring model was now behaving more fairly, but the product still felt crowded.

That exposed a different layer of the system.

## Pass 4: scoring versus slate composition

The application persisted an active Discover tray of up to 60 recommendations.

Up to 12 slots were reserved for Wildcards. The remaining 48 non-Wildcard slots were filled by flat rank order.

So even after the scoring corrections, one media kind could still consume most of those 48 slots if it had enough highly ranked supply.

This was no longer primarily a scoring bug.

It was a **slate-composition problem**.

There was also a UI inconsistency: the application could persist up to 60 active recommendations while the All tab silently rendered only 30.

### Product rule

**Score every candidate honestly, but compose a useful active slate.**

The correction preserved raw score and classification while changing selection of the persisted active tray:

- deterministic rather than random;
- supply-aware rather than fixed quotas;
- round-robin across available media kinds;
- unused capacity automatically redistributed when a kind runs out;
- no relabeling or score manipulation;
- Wildcard reservation preserved;
- the All tab shows the full active tray rather than an unrelated 30-card subset.

This distinction matters.

A ranking score answers "How strong is this candidate?"

A product feed answers "Which set of candidates is most useful to show together?"

Those are related questions, not identical ones.

## What I did

My contribution was the product investigation and iterative direction:

- noticed that the live recommendation mix contradicted the visible taste model;
- rejected "anime is just what the user likes" as an unsupported explanation;
- defined the constraint that explicit user steering must remain meaningful;
- rejected quotas and randomization as premature fixes;
- kept the investigation open after the first technically correct fix did not change the actual product;
- pushed the analysis from format, to taxonomy, to metadata density, to slate composition;
- articulated the governing product principles used to constrain each implementation;
- evaluated the live behavior after each pass;
- required each discovered rule to become deterministic regression coverage.

## What AI agents did

AI research and coding agents were used to:

- inspect the codebase and live read-only diagnostics;
- trace scoring paths and reason codes;
- implement the scoring changes;
- write deterministic unit and integration tests;
- measure catalogue metadata density;
- implement deterministic slate composition;
- document commits and after-action findings.

I do not present the implementation code as hand-written software-engineering work.

The case study demonstrates the part I did own: identifying the product failure, interrogating incomplete explanations, defining semantics, directing investigation, evaluating outcomes, and deciding when the system was still wrong.

## Evaluation design

The final regression coverage encoded the failure rather than only the implementation.

Examples included:

- one matched genre out of one versus one matched genre out of four;
- three matched genres out of three versus three out of six;
- dense and sparse candidates with equivalent positive matches;
- explicit direct preferences remaining undiluted;
- literal inferred Anime remaining neutral;
- machine/why-tag evidence staying independent;
- deterministic active-slate recomputation;
- supply-aware fallback when only one media kind exists;
- full active-tray rendering in the All view.

This matters because a product fix is much more durable when the test suite captures **why the old behavior was wrong**, not merely the lines of code that changed.

## What this demonstrates

- Behavioral debugging from real user experience
- Product semantics under ambiguous evidence
- Recognition of proxy and representation bias
- Iterative hypothesis testing
- Separation of model score from product presentation
- Human-intent preservation
- Eval and regression design
- AI-assisted technical direction without pretending to be the implementation engineer

## Broader lesson

The interesting failure was not that the model "liked anime too much."

The system had several individually reasonable signals that interacted badly:

1. inferred format,
2. a wrapper category represented as a genre,
3. uneven metadata density,
4. flat top-N slate selection.

Each fix exposed the next layer.

That is exactly why real AI products need people who will keep asking whether the product behavior matches the intended human meaning after the technically plausible explanation has already been implemented.