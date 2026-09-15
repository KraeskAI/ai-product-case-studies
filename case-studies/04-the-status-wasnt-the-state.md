# Case Study 04: The Status Wasn't the State

## Executive summary

A community music platform exposed submission records with labels such as `pending`, `accepted`, `deleted`, and `on air`.

The labels looked like a state model. In practice, they were mostly bookkeeping markers.

A track could still show `pending` after it had already played in a Listening Party. `Deleted` often meant the submission lifecycle had been cleaned up, not that the track had been rejected. `On air` meant something different again: the track had entered the platform's persistent radio rotation.

The result was a recurring cognitive tax for artists trying to answer basic questions:

- What have I already submitted?
- Which upcoming Listening Parties still need a track?
- Has this song already played?
- Which songs are on the radio?
- Which inboxes are open right now?
- Am I about to submit the same thing twice?

I modeled those as separate product concepts, directed an AI coding workflow to build a single-file local tracker, then iterated against real platform behavior until the prototype became useful enough to hand to the uploader maintainers as a source of product ideas.

The maintainers began adapting the useful pieces directly into the native uploader, where they have access to the live schedule, inbox state, and submission records that the standalone prototype could only infer from copied data.

The important artifact is not the HTML page.

It is the workflow model that survived contact with real use and transferred cleanly into the system that actually owns the data.

## The problem

The platform's raw submission view was technically complete and practically difficult to use.

Each row contained identifiers, account handles, track names, event names, genres, backend status labels, and timestamps. The data answered individual database questions, but it did not answer the human question:

> What do I need to do next?

That became especially painful across a weekly rotation of Listening Parties and After Parties. Listening Party inboxes could open days before an event and close when full. After Party inboxes often opened shortly before the event. Hosts sometimes left backend records in `pending` or `accepted` long after the track had already played.

The user had to mentally reconcile schedule, submission history, radio acceptance, inbox availability, and host bookkeeping every time they wanted to submit music.

## The key product insight

The first useful move was to stop treating the platform's status field as the truth.

The workflow actually contained several independent facts:

### Event booking

Which track is committed to which LP or AP occurrence?

### Play history

Has that occurrence already happened?

### Radio state

Has this track been accepted into the platform's ongoing radio rotation?

### Backend bookkeeping

What does the platform currently label the record: `pending`, `accepted`, `deleted`, or `on air`?

Those facts can correlate, but they are not interchangeable.

Once separated, the tracker could answer the questions the artist actually cared about instead of reproducing the source table with nicer colors.

## Prototype evolution

The first prototype was deliberately small: one local HTML file with no server, account, installation, analytics, or network dependency.

A user pasted copied platform data into it. The browser maintained a durable local ledger.

The tracker then grew around observed workflow failures rather than a speculative feature list:

- merge new pastes into the existing ledger instead of replacing history;
- deduplicate stable submission IDs;
- preserve status changes without duplicating the underlying submission;
- make radio acceptance durable once observed;
- separate upcoming commitments from historical track detail;
- collapse old track history behind compact per-track controls instead of letting archival data dominate the dashboard;
- convert visible dates and times to the user's local system timezone;
- show every upcoming Listening Party, not only the ones already submitted to;
- distinguish `Submitted`, `Not submitted`, and `Closed`/not accepting;
- parse the platform's separate Submission Status and Listening Party Schedule text when pasted;
- treat the live Submission Status page as authoritative for whether an inbox is actually accepting tracks;
- keep the schedule responsible for who runs when, rather than incorrectly inferring availability from the schedule's visible `SUBMIT` text.

The prototype became a small reconciliation engine rather than a prettier spreadsheet.

## Real-world edge cases changed the design

Several rules only became visible through actual use.

### LP and AP timing are different

Listening Party inboxes may open roughly a week before the event. After Party inboxes usually open shortly before or during the event they follow.

That meant the same timestamp could not be interpreted the same way for both submission types.

### Host bookkeeping can lag reality

A submission may remain `pending` or `accepted` after it has already played.

The tracker therefore uses event occurrence and known workflow rules rather than assuming the raw status label describes real-world state.

### The platform exposes more than one submission table

One page used a leaner column layout. Another view contained extra fields.

A parser based on fixed column positions broke as soon as a different valid view was pasted. The importer was changed to identify meaningful values such as status semantically instead of assuming one rigid table shape.

### Useful metadata was hiding inside the identifier

The numeric suffix of the platform submission ID encoded a Unix timestamp.

Once recognized, that became a stronger clue for assigning a submission to the correct LP occurrence than some of the visible timestamps, which reflected later bookkeeping changes.

### Schedule does not equal availability

The copied schedule could visually contain a `SUBMIT` label even when the live page did not make that row actionable.

The design was corrected so schedule data determines timing while the separate Submission Status page determines whether the inbox is open.

These were not abstract edge cases. Each one came from the system disagreeing with an assumption during normal use.

## The usability test

The tracker became useful when it stopped being something to inspect and became something to act from.

Using the consolidated upcoming-LP view, I was able to move through every currently open Listening Party for the next week and submit tracks from an album campaign in order, quickly, without reconstructing from memory which host already had which track or which songs were already in radio rotation.

That was the product test that mattered: a previously mind-numbing coordination task became a short, reliable workflow.

## Handoff to the native product

Once the prototype demonstrated the interaction model, I sent it to the people maintaining the platform uploader with an explicit instruction to pull it apart and take whatever was useful rather than preserve my implementation.

That distinction mattered.

The standalone tracker had to infer truth from whatever a user manually copied out of the site. The native uploader already owns the live schedule, open/closed inbox state, and submission records.

Moving the useful ideas into the native system removes entire classes of inference and synchronization problems rather than polishing the workaround forever.

The uploader maintainer subsequently began integrating the useful concepts into the native interface.

That is the preferred outcome for this kind of prototype: prove the workflow, expose the semantics and edge cases, then let the system with authoritative data absorb the parts that belong there.

## What I did

My role was product discovery, systems modeling, UX direction, evaluation, and handoff:

- identified that the real problem was cognitive reconciliation, not lack of raw data;
- separated booking, play history, radio state, and backend bookkeeping into distinct concepts;
- translated messy platform behavior into explicit product rules;
- repeatedly tested the tracker against real submission workflows and corrected false assumptions;
- simplified the interface around immediate user questions rather than exposing the internal ledger;
- generalized a personal tool into a one-file community utility with local persistence and backup;
- recognized when the native platform was the correct long-term home for the workflow;
- handed the prototype to the maintainers as a source of ideas rather than defending the implementation;
- continued identifying UX gaps once the concepts began moving into the native uploader.

## What AI did

ChatGPT produced the implementation under iterative direction: HTML/CSS/JavaScript, parsing logic, local persistence, reconciliation rules, migration fixes, and successive UI changes.

I did not manually write the application code.

The work I am presenting is the product reasoning around what the system should mean, how conflicting evidence should be interpreted, which details should be visible to the user, how real-world failures changed the rules, and when the prototype should give way to a native implementation.

## What the platform maintainers did

The uploader maintainers own the native system and its implementation.

Once given the prototype and workflow model, they began adapting useful pieces into the uploader using access the standalone tool never had: authoritative schedules, inbox state, submission records, and native navigation.

Their implementation is theirs. The portfolio claim here is the discovery, prototype direction, workflow model, and transfer of those ideas into a real product context.

## What this demonstrates

- Product discovery from real operational friction
- State-model design from ambiguous backend semantics
- Human-centered information architecture
- Rapid AI-assisted prototyping
- Iterative evaluation against real behavior
- Parser and workflow robustness driven by observed edge cases
- Product simplification and progressive disclosure
- Local-first/privacy-conscious utility design
- Stakeholder handoff without implementation attachment
- Ability to turn a personal workaround into a transferable product concept

## Broader lesson

A backend status is not automatically a user state.

Systems often expose the labels that are convenient for their own workflow while forcing the user to reconstruct the meaning they actually care about.

A useful product model begins by asking what decision the human is trying to make, then separating the underlying facts until that decision becomes obvious.

And sometimes the best endpoint for a prototype is not a more polished prototype.

It is getting the right idea into the product that owns the truth.