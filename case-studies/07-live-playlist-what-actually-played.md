# Case Study 07: A Playlist Is Not a Play History

**Status:** Experimental public audience page deployed; ordinary live publishing was not enabled at the reviewed milestone.

## The problem

A show playlist describes what its host intends to play, but not necessarily what the audience eventually hears. Tracks get reordered, held, skipped, replaced, or interrupted.

I worked on an AI-assisted prototype for a public listening-party page that separates three concepts: the current song, a provisional queue, and the record of completed performances.

## The product rule

**Only completed tracks belong in the durable show history.**

Being queued is not enough. A skipped or interrupted selection should never be presented as a completed play. This distinction makes the archive useful to artists and listeners instead of reproducing the host's planning notes.

## Product direction and iteration

I defined the host-versus-listener information boundaries and required the display to support different show identities rather than assuming one permanent host. I also pushed for compact artwork, restrained data retention, and clear separation between a functioning public page and a proven live broadcasting integration.

AI coding agents created the prototype, supporting service, automated checks, and initial deployment. The source documentation records functional tests and a public audience endpoint. It also documents that production publishing and acceptance had not been completed.

## My contribution

- Identified the mismatch between scheduled entries and actual listening history.
- Defined completion as the event that makes a record durable.
- Specified the audience experience, operating rules, and configurable show identity.
- Evaluated tradeoffs and avoided claiming that deployment alone establishes operational readiness.
- Coordinated agent-assisted implementation and review.

I am not claiming to have independently implemented the service code.

## What this demonstrates

Operational product modeling, event-driven behavior requirements, human-centered information design, community-tooling research, and clear acceptance criteria.

**The lesson:** a trustworthy public history must reflect what actually happened rather than what somebody intended to happen.
