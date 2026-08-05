---
name: grilling
description: Conduct rigorous discovery until a proposed creation or development effort is understood. Use when the user wants to create, build, develop, design, add, or substantially change a project, especially when decisions or requirements remain unresolved.
---

# Grilling

## Input and output contract

- **Input:** The user's initial creation or development intent, the active conversation, and discoverable project context.
- **Output:** Shared understanding with the user of what is being created or changed, including the resolved decisions and any explicitly deferred open questions.
- **End state:** The grilling ends at shared understanding. It never forces documentation and never begins implementation.

## Method

1. Preserve the user's initial context as part of the conversation.
2. Before asking a question, inspect the working project/codebase whenever the answer can be discovered there. Do not ask the user for facts available in the project.
3. Walk through the decision tree one dependency at a time.
4. Ask exactly one focused question per response.
5. With every question, provide your recommended answer and a concise reason for that recommendation.
6. Use the user's response to select the next unresolved branch. Resolve ambiguities, dependencies, constraints, edge cases, and relevant alternatives without turning the conversation into project-management paperwork.
7. Continue until you and the user share the same understanding. Do not impose acceptance criteria, task breakdowns, implementation plans, or acceptance-criteria sections.
8. When shared understanding is reached, stop. Report the understanding and any open decisions to the calling worker or workflow.

## Boundaries

- Conduct the grilling only. Do not write the session document yourself and do not begin implementation.
- Do not delegate or re-route; the caller decides how the shared understanding is used.
