# Case Study 06: Hydra, When Agent Activity Is Not Progress

**Status:** Local orchestration and activity-viewer system with implemented, evolving components; provider compatibility and unattended operation are not claimed as universally solved. Evidence reviewed through November 2026.

## The problem

Using several AI coding environments in parallel increased available capability but also introduced new coordination problems. Each provider exposed different session states, quotas, models, launch behavior, and logs. A running process could be mistaken for meaningful progress. A model could report that it had finished without tests or a verified artifact. Multiple workers could unknowingly edit the same checkout.

The user became the dispatcher, monitor, interpreter, and integration point. I wanted that bookkeeping moved into tools without surrendering decisions about scope, priority, access, or acceptance.

## The product model

**Hydra** began as an activity viewer and expanded toward a coordinated local agent operating environment.

Its most important design distinctions are semantic:

- **Process existence is not task completion.** Running, idle, ended, failed, and unknown need different evidence; silence does not prove that work succeeded.
- **A session is not a repository.** Several agents may work in one repo. A nearby timestamp or common path is insufficient to establish which process owns which session.
- **A quota percentage is not universal capacity.** Codex, Claude, and AGY expose different model buckets, reset windows, and usable allowances. Routing must account for those differences instead of pretending providers are interchangeable at the CLI level.
- **Delegation needs an acceptance contract.** An assignment includes scope, authority, ownership, evidence, and a definition of done. Completed implementation still requires independent verification and integration.
- **Coordination should reduce supervision, not create a second job.** Routine polling, redundant agent work, and constant status narration defeat the purpose of autonomy.

## Implemented and tested directions

The repository documents automatic Claude and Codex session discovery, explicit registered jobs, source-backed PID association, a recursive local-repository inventory, quota display, provider launch policies, and independent quality-assurance and Git finalization work. It also records ongoing development to make AGY a normal, useful worker rather than a permanently exceptional or read-only route.

Some diagnostic and integration issues remain open. The existence of a dispatcher, launch flags, or tests is not proof that every provider can perform every task reliably without supervision.

## Decisions I directed

I set the expected behavior and challenged approaches that looked cautious or technically elegant but defeated the actual objective:

- Coordinate providers across independent quota pools instead of overusing a single expensive agent.
- Preserve one responsible writer for a checkout while allowing parallel, nonconflicting work.
- Stop confusing model self-reports, telemetry, and independent acceptance.
- Make quota and activity displays readable enough to inform real decisions.
- Keep operator authority explicit: genuine platform restrictions are different from assistant-invented restrictions.
- Prefer durable project records and verified outcomes over endless narrated progress.

AI agents researched APIs, wrote most code, authored tests, and implemented successive changes. My work was the operating model, requirements, product constraints, failure analysis, and evaluation.

## Outcome and limits

Hydra is a substantial working local project, not a proven general-purpose orchestration platform. Its strongest evidence is the set of specific rules and technical checks that emerged from using AI agents in demanding real projects.

**What this demonstrates:** agentic workflow design, observability and state semantics, provider-agnostic product thinking, quota-aware task allocation, technical product direction, software quality systems, and operational judgment.

The central lesson: an AI workforce does not become manageable merely because its processes appear on a dashboard. The system must distinguish activity, authority, evidence, and accepted results.
