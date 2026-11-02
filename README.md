# AI Product & Model Behavior Portfolio

I investigate where AI-assisted systems fail in real use, then turn those discoveries into product rules, operational workflows, and working tools. My work now spans model behavior and evaluation, AI-native product direction, multi-agent coordination, and creative tooling. I direct AI research and coding agents while retaining responsibility for requirements, tradeoffs, user testing, and acceptance.

The newer projects are not just thought experiments: they include working desktop tools, local agent infrastructure, browser-based creative software, and a deployed-but-not-yet-live-publishing audience service. Their status and limits are documented rather than collapsed into blanket claims of production readiness.

My process is empirical and iterative:

1. Notice behavior that feels wrong in actual use.
2. Define the intended product semantics in plain language.
3. Form a testable hypothesis.
4. Use multiple frontier AI systems, primarily GPT, Claude, and Gemini, for research, implementation, review, and cross-checking.
5. Evaluate the real behavior, not just whether the code compiled or the tests passed.
6. Keep digging when the product still behaves wrong.
7. Turn the discovered rule into tests, documentation, and durable product constraints.

## What I contribute

- AI-assisted product ownership from initial observation through usability testing and release decisions
- Multi-agent delegation, work partitioning, independent QA, and verification-driven delivery
- Design of local operator tools, live workflows, and cross-system integrations
- Product and behavior problem discovery
- Requirements extracted from messy real-world observations
- Human-AI workflow design
- Recommender and model-behavior reasoning
- Evaluation criteria and regression-test design
- Cross-model context management, role separation, and handoff design
- Cross-disciplinary transfer of useful controls and practices into new environments
- Provenance, authority, and collaboration rules
- Iterative direction of AI research and coding agents
- Judgment about when a technically plausible solution still fails the user

## What I do not claim

I am not presenting myself as a conventional software engineer.

I use GPT, Claude, and Gemini extensively, often in parallel across the same projects, for technical research, implementation, code review, test writing, and drafting. A meaningful part of the work is keeping project state coherent across models with different strengths, context, and behavior. The case studies in this portfolio distinguish product direction and judgment from AI-assisted implementation rather than pretending the AI was not part of the work.

See [AI Collaboration Disclosure](AI_COLLABORATION_DISCLOSURE.md).

## Selected product and operational case studies

1. **[Building Nightwire Around the Host's Actual Workflow](case-studies/05-building-nightwire-as-a-real-host-workflow.md)**  
   A two-screen live music-hosting application evolved through real show needs, multi-provider media integration, hardware controls, stable/beta separation, and ongoing real-device acceptance.

2. **[Hydra: When Agent Activity Is Not Progress](case-studies/06-hydra-when-agent-activity-is-not-progress.md)**  
   Coordinating GPT/Codex, Claude, and AGY exposed the difference between running processes, useful progress, and verified completion. A local orchestration and observability system grew from those distinctions.

3. **[A Playlist Is Not a Play History](case-studies/07-live-playlist-what-actually-played.md)**  
   A public audience service distinguishes an intended queue from a truthful record of completed plays. Deployed prototype; live publishing integration remains under evaluation.

4. **[Noise Loom: Making Rhythmic Experimentation Tactile](case-studies/08-noise-loom-composing-without-writing-a-daw.md)**  
   An offline music sketch tool grew into a section-aware odd-meter arrangement instrument; real editing and saved-project failures became regression tests. The project was intentionally parked after a reliability milestone.

## Model behavior, context, and collaboration case studies

5. **[When More Metadata Made the Recommender Worse](case-studies/01-when-more-metadata-made-the-recommender-worse.md)**  
   Structural metadata-density bias and slate composition, uncovered after two seemingly correct scoring fixes failed to solve the real recommendation problem.

6. **[Stop Making the Human Be the API](case-studies/02-stop-making-the-human-be-the-api.md)**  
   Continuum simplified into an MCP context engine so humans did not have to become the bridge between models and projects.

7. **[Two Humans, Two AIs, One Canonical Creative Project](case-studies/03-two-humans-two-ais-one-canonical-project.md)**  
   Shared repository truth, provenance, context handoff, authority, and human creative agency across distinct AI conversations.

8. **[The Status Wasn't the State](case-studies/04-the-status-wasnt-the-state.md)**  
   Reconciled event booking, play history, radio rotation, and backend status into a useful local workflow that was handed to native platform maintainers.

## Earlier systems work

**[From Banking Controls to Retail Fraud Prevention](earlier-systems-work/01-from-banking-controls-to-retail-fraud-prevention.md)**  
A 2020 example, before generative AI entered my workflow, of identifying an accountability and training gap after a real fraud incident, transferring relevant controls from banking into luxury retail, and turning them into practical frontline training and procedure.

I include this separately because it helps establish that the underlying pattern in the AI case studies - finding a broken assumption, following the seam across disciplines, and turning the result into an explicit usable system - predates the models.

## Portfolio descriptor

**AI Product & Model Behavior Designer** (portfolio descriptor), with demonstrated work in **AI-native product direction and multi-agent workflow design**

This is a portfolio descriptor, not a claim of a previous formal job title. The work sits at the intersection of product reasoning, model behavior, evaluation, human-AI interaction, multi-model workflows, cross-disciplinary systems thinking, and AI-assisted systems design.
## Evidence and status

These are first-person, AI-assisted case studies supported by project repositories, tests, operating notes, and real-use observations. Several underlying repositories are private; public descriptions deliberately omit internal configuration and credentials. A repo, a passing test, a deployed page, and a production-accepted workflow are not interchangeable evidence. Individual case studies call out open acceptance work and what AI agents implemented.

This portfolio is not a claim of formal software engineering, ML research, or prior employment under these role titles.
