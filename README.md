# AI Product & Model Behavior Portfolio

I investigate where AI-assisted systems fail in real use, especially when the failure is not a single bug but a mismatch between model behavior, data, product constraints, and human workflow.

My process is empirical and iterative:

1. Notice behavior that feels wrong in actual use.
2. Define the intended product semantics in plain language.
3. Form a testable hypothesis.
4. Use multiple frontier AI systems, primarily GPT, Claude, and Gemini, for research, implementation, review, and cross-checking.
5. Evaluate the real behavior, not just whether the code compiled or the tests passed.
6. Keep digging when the product still behaves wrong.
7. Turn the discovered rule into tests, documentation, and durable product constraints.

## What I contribute

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

## Case studies

1. **[When More Metadata Made the Recommender Worse](case-studies/01-when-more-metadata-made-the-recommender-worse.md)**  
   A recommendation system repeatedly over-selected anime. Two plausible fixes were correct but insufficient. The deeper failure was structural metadata-density bias, followed by a separate slate-composition problem.

2. **[Stop Making the Human Be the API](case-studies/02-stop-making-the-human-be-the-api.md)**  
   Continuum evolved from an overbuilt application into a lightweight MCP context server designed around one product rule: the agent should handle context bookkeeping instead of making the human continually re-explain the project.

3. **[Two Humans, Two AIs, One Canonical Creative Project](case-studies/03-two-humans-two-ais-one-canonical-project.md)**  
   A collaboration design for two human creators using separate AI conversations against one shared repository, with explicit provenance, context handoff, branch authority, and creative-agency safeguards.

## Earlier systems work

**[From Banking Controls to Retail Fraud Prevention](earlier-systems-work/01-from-banking-controls-to-retail-fraud-prevention.md)**  
A 2020 example, before generative AI entered my workflow, of identifying an accountability and training gap after a real fraud incident, transferring relevant controls from banking into luxury retail, and turning them into practical frontline training and procedure.

I include this separately because it helps establish that the underlying pattern in the AI case studies - finding a broken assumption, following the seam across disciplines, and turning the result into an explicit usable system - predates the models.

## Portfolio descriptor

**AI Product & Model Behavior Designer**

This is a portfolio descriptor, not a claim of a previous formal job title. The work sits at the intersection of product reasoning, model behavior, evaluation, human-AI interaction, multi-model workflows, cross-disciplinary systems thinking, and AI-assisted systems design.