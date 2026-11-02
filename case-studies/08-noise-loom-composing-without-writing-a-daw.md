# Case Study 08: Noise Loom, Making Rhythmic Experimentation Tactile

**Status:** Offline creative tool with a completed odd-meter reliability milestone; intentionally parked as of October 31, 2026.

## The problem

I wanted to direct unusual rhythmic foundations for AI-assisted music generation without first becoming a percussion programmer or learning to sequence every event in a full digital audio workstation.

The creative goal was specific: hear an idea, change its grouping and emphasis, arrange sections, and export a useful audio seed. The user interaction needed to be exploratory and tactile, not an exercise in translating musical curiosity into implementation detail.

## From a generator to an instrument

**Noise Loom** became an offline, browser-based sketch instrument. Its current catalog contains 228 rhythm sketches derived from 57 foundations, each with four deliberately different electronic interpretations. It supports additive and odd-meter explorations, arrangement sections, section-specific editing, project saving, undo/redo, and WAV export.

The important product choices were about preserving the creator's intent:

- A rhythm variation must change actual accents and timing, not merely its display name or tempo.
- A section edit must modify the selected part, not unexpectedly rewrite the opening pattern.
- When a multi-bar groove starts at a new marker, its phase must start where the human intended.
- A saved project must preserve all edits even in a long, complex arrangement.
- Visual activity and labels must correspond to musical events rather than imply behaviors the audio engine cannot produce.

## Real failures changed the acceptance criteria

A late reliability audit identified an out-of-phase restart for multi-bar grooves and a project-import limit that lost clip toggles after section 100. The agent-assisted fixes were checked with browser regressions and round-trip tests.

The documentation also records limits honestly. Browser audio renders may differ slightly between runs, and an external music model's response to an odd-meter audio seed is not guaranteed to preserve the requested meter. I did not treat an interesting generated result as proof of deterministic timing control.

## My contribution

I defined the creative problem, judged the musical usefulness of the interaction, challenged designs that disguised identical rhythms as meaningful variations, directed interface revisions, and required test cases based on real use. AI agents implemented the application, tests, and audio-rendering logic.

This is an example of product direction informed by hands-on creative practice, not a claim of independent expertise in low-level digital signal processing.

## Outcome and limits

The tool reached a useful, test-backed state and was deliberately parked rather than expanded indefinitely. That pause is a scope decision, not evidence that the product failed.

**What this demonstrates:** human-centered creative tooling, iterative prototyping, requirements grounded in domain practice, test design for stateful editing, honest model-capability evaluation, and disciplined stopping criteria.

The central lesson: a good AI-assisted creative tool should preserve what the artist meant to change, not merely generate something superficially impressive.
