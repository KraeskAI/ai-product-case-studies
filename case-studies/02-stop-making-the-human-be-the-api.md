# Case Study 02: Stop Making the Human Be the API

## Executive summary

Continuum began from a recurring problem in AI-assisted work: every new agent session demanded another manual reconstruction of project state.

The tax became especially obvious while moving real project work among GPT, Claude, and Gemini. Each system could be highly capable inside its own session, yet the human still had to carry decisions, file context, preferences, and unfinished work across model boundaries.

What was already decided? What had been tried? Which files mattered? What had changed since the last session? What preferences applied to this user? What role was this particular agent supposed to play?

The early system grew into a conventional application with a web API, dashboard, realtime plumbing, and strict handoff formats. That architecture could store information, but it still risked making the human responsible for moving context between the AI and the system.

The current design deliberately strips the product back to a lightweight local MCP memory server.

The central product principle is:

> The agent handles the bookkeeping. The human does the work they actually came to do.

## The problem

A stateless agent can be excellent inside one session and still impose a large tax across sessions.

The user repeatedly becomes the integration layer:

- paste the old plan;
- explain the current state;
- remember which decision superseded which;
- tell the next agent which files matter;
- repeat personal working preferences;
- summarize what another model already discovered;
- reconcile different model assumptions about the same project.

This is not merely a memory problem.

It is a **workflow-design problem** caused by making the human act as the API between otherwise capable systems.

## Product evolution

Continuum's earlier architecture accumulated:

- a web API;
- a dashboard;
- realtime SignalR plumbing;
- a strict SUBMIT block workflow;
- more application surface than the core context problem actually required.

The current V2 intentionally removes those surfaces from the core.

The active product is a local Go MCP server with SQLite storage, semantic search, a CLI for inspection, and a deliberately small tool surface.

The architecture separates the engine from the interface so a future consumer UI can be added without rebuilding the underlying model.

## Three kinds of context

A key product decision was to stop treating "memory" as one undifferentiated pile.

### 1. Project data

Shared, objective project state:

- tasks;
- sessions;
- decisions;
- file references;
- relationships and supersession.

This belongs to the project, not to one model.

### 2. User profile

Cross-project information about how the human prefers to work:

- communication preferences;
- recurring frustrations;
- confirmed working patterns;
- corrections.

Agents may propose updates, but the human approves or rejects them conversationally.

### 3. Agent role

Per-agent, per-project context:

- what this agent is responsible for;
- what it should not do;
- project-specific working agreements;
- role and persona history where relevant.

Two agents working on the same project can therefore share project truth without being forced into the same role or personality.

That separation also reflects practical multi-model work. GPT, Claude, and Gemini do not need to behave identically in order to share a trustworthy project state. The durable layer should preserve what is true about the project while allowing each model to bring a different working style or role.

## Automatic retrieval, not another filing system

The design target is not "a database the user can query."

At session start the agent should already receive a compact relevant snapshot.

If more detail is needed, the agent retrieves it.

The user should not need to remember to save something, retrieve something, or manually paste a handoff every time.

This principle also constrains project creation. The agent may notice that a new durable project exists, but asks before creating one rather than silently producing administrative clutter.

## Correctness over completeness

A large memory that mixes current and stale information is worse than a smaller trustworthy one.

Continuum therefore treats supersession and staleness as first-class problems rather than simply accumulating prose forever.

The broader design lesson is that persistent AI context needs:

- source identity;
- current versus historical state;
- explicit reversals;
- auditability;
- conflict handling;
- a compact retrieval policy.

"Remember everything" is not a product specification.

## What I did

My role in Continuum has been product direction and iterative architecture:

- identified the repeated human-as-bridge failure while juggling real work across GPT, Claude, and Gemini;
- pushed the system away from workflows that required manual context submission;
- separated project truth, user profile, and per-agent role;
- required transparent, inspectable state rather than invisible memory magic;
- preserved conversational approval for profile changes;
- pushed V2 toward a small MCP engine after the earlier application became too elaborate;
- treated the first version as evidence rather than sunk-cost architecture;
- used real multi-model work to expose context, handoff, staleness, role, and identity problems.

## What AI agents did

GPT-, Claude-, and Gemini-based coding and research workflows have contributed implementation, reviews, tests, migrations, technical research, and documentation at different points in the project.

That is intentional.

Continuum is itself partly an experiment in whether a nontraditional technical product owner can coordinate capable but behaviorally different AI systems to turn observed workflow failures into a functioning product without making the human the permanent context shuttle between them.

## What this demonstrates

- First-principles product simplification
- Human-AI workflow design
- Multi-model context and handoff design
- Persistent-context architecture
- Provenance and supersession reasoning
- Agent-role separation
- Approval and trust boundaries
- Willingness to discard architecture when it does not serve the core interaction
- Direction of AI implementation agents across a long-running system

## Broader lesson

The most expensive part of many AI workflows is not model intelligence.

It is the context tax imposed on the human.

The useful system is the one that makes that tax disappear without making the underlying state opaque or untrustworthy.