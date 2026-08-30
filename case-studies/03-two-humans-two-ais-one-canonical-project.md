# Case Study 03: Two Humans, Two AIs, One Canonical Creative Project

## Executive summary

A creative collaboration becomes unusually complicated when two humans each use private AI conversations against one shared project.

The obvious solution - put everyone in one giant shared chat - creates its own problems. Private conversations contain unrelated material, personal context, exploratory dead ends, and model-specific working relationships. Making all of that shared state is neither necessary nor desirable.

The collaboration design used for The Midnight Engine treats the repository, not the private chat, as the durable shared boundary.

The system then adds explicit rules for:

- source authority;
- human versus AI provenance;
- branch authority;
- context discovery;
- context handoff;
- creative agency;
- review and merge responsibility;
- differences between browser and IDE tooling.

The interesting product problem is not music. It is how multiple humans and multiple AI agents can collaborate without silently collapsing private context, authorship, authority, or responsibility.

## The problem

Two collaborators can each have a capable AI assistant and still fail to share the right state.

One agent may know:

- the track's narrative purpose;
- an album-level constraint;
- a prior decision;
- a collaborator's raw seed;
- why a neighboring song already owns a particular idea.

The other human does not automatically know any of that.

A private AI silently reading the repository is therefore not enough.

The collaborator needs the context required to exercise human judgment.

## Repository as durable shared context

The shared repository is treated as canonical project state.

Private ChatGPT conversations are explicitly not considered shared authority unless the relevant decision or source material has been committed.

This creates a clean boundary:

- private conversations remain private;
- durable project state is inspectable;
- both agents can recover the same canonical evidence;
- historical conversation memory cannot silently outrank current project files.

## Source authority and provenance

The workflow distinguishes:

- human-authored material;
- collaborator-authored seed material;
- AI-generated drafts;
- human-selected AI material;
- human-revised or replaced material;
- ambiguous provenance.

Generated text is not silently promoted into human authorship.

Raw collaborator seed material is preserved rather than "cleaned up" in place.

This matters in any AI-assisted creative or knowledge workflow where authorship, intent, or historical sequence has value.

## Agent context is not collaborator context

One of the most important rules emerged from actual collaboration:

> Silently reading a file is not the same thing as handing that context to the human collaborator.

Before asking the collaborator to write, revise, choose, or critique, the agent must surface the compact context they actually need:

- what governs the current work;
- what the track is trying to accomplish;
- what it is not supposed to accomplish yet;
- neighboring boundaries;
- existing human source material;
- unresolved choices that genuinely belong to the humans.

This creates a useful distinction:

1. **Agent context** - what the model privately needs in order to reason correctly.
2. **Collaborator context** - what the human must actually know in order to make an informed creative decision.

Both are required.

That principle generalizes far beyond music.

## Branch authority without technical enforcement

The second collaborator works through a dedicated long-lived branch.

Rules include:

- `main` is canonical;
- all collaborator-originated writes explicitly target the collaborator branch;
- completed work is proposed by pull request;
- the collaborator and their AI do not merge their own work;
- ambiguous or diverged branch state stops the write rather than forcing history.

Because the repository plan does not provide technical branch protection for this private repository, the AI instructions treat the procedural rule as a hard constraint and explicitly avoid relying on the default branch.

This is not perfect security. It is a practical authority model designed around the available tooling.

## Creative-agency safeguards

The repository also constrains a common AI failure mode: over-helping.

The AI is told not to:

- invent replacement lyric lines during critique unless asked;
- rewrite one layer to solve a problem in another;
- optimize a local section at the expense of global progression;
- mistake every generative accident for intentional meaning;
- turn one successful fix into a universal creative rule;
- bury a human collaborator in invisible project architecture.

The objective is not maximum AI intervention.

It is better human judgment.

## Tooling differences stay visible

The project can be accessed in richer IDE environments or through browser GitHub tools.

The workflow explicitly refuses to pretend those environments are equivalent.

If a browser session cannot access a local context server or execute repository skills automatically, the agent must recover what it can from canonical repository evidence and state the limitation rather than fabricating tool use.

That rule protects trust more effectively than cosmetically pretending every environment has the same capabilities.

## What I did

My contribution was to identify the collaboration failures and keep converting them into explicit product rules:

- private conversation should not equal shared project state;
- repository evidence should outrank remembered summaries;
- reading context privately is not enough;
- collaborators need usable handoff, not repository archaeology;
- human seed provenance must survive AI processing;
- AI critique should not silently become AI authorship;
- branch authority must remain explicit even when GitHub cannot enforce it technically;
- tool limitations must stay visible.

## What AI agents did

AI agents helped draft and refine the repository instructions, inspect state, perform GitHub operations, route source material, and test the workflow in practice.

The collaboration rules themselves were iterated from real failures and friction rather than written as a hypothetical policy exercise.

## What this demonstrates

- Multi-human / multi-agent workflow design
- Context-boundary design
- Provenance and authorship protection
- Human agency in AI-assisted creative work
- Trustworthy tool behavior
- Procedural safety under imperfect platform controls
- Translating lived collaboration friction into durable model instructions

## Broader lesson

The future of collaborative AI is not only "more people in the same chat."

Useful collaboration needs explicit answers to:

- What is private?
- What is shared?
- What is canonical?
- Who can change it?
- What does the AI know that the human does not?
- What must be surfaced before the human is asked to decide?
- Who authored this?
- Who has final authority?

Without those answers, adding more agents can increase confusion faster than it increases capability.