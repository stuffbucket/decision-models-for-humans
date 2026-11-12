# Patterns

These patterns describe jobs, not products. A model may support one pattern directly or require the application to compose it from simpler questions.

## Route

**Job:** send an item to one of several destinations.

```text
message → billing 0.83, account 0.12, shipping 0.05 → billing queue
```

Use a pick-one question when exactly one destination must own the item. Add a separate “does any destination fit?” judgment or a review rule when none may fit.

Examples: support queues, model selection, tool selection, document type, email folder.

## Tag

**Job:** mark every property that applies.

```text
review → battery 0.91, delivery 0.84, screen 0.08 → battery + delivery
```

Use independent yes/no judgments or a multi-label question. A pick-one question is wrong when two properties can both be true.

Examples: review aspects, policy flags, skills mentioned, symptoms described.

## Gate

**Job:** decide whether code may move to an expensive or risky step.

```text
Does the request contain a complete shipping address? 0.94
0.94 ≥ tested threshold → continue
```

The model judges the condition. Code owns the threshold and the action. Give failures and unsettled cases separate outcomes.

Examples: call a larger model, ask for missing information, permit a tool, send to review.

## Score

**Job:** place an item on an ordered scale.

```text
routine 0.05, important 0.25, urgent 0.60, critical 0.10
```

Describe each level as a standalone situation. “More urgent than the previous level” forces the reader and model to reconstruct the scale.

Examples: severity, urgency, quality rubric, relevance, tone.

## Rank

**Job:** order known candidates by how well each matches a need.

```text
query + 20 search candidates → relevance judgment per candidate → sorted shortlist
```

Ordinary retrieval should find candidates. The decision model judges those candidates. It should not be expected to recall items that were never supplied.

Examples: search results, matching records, listings, passages for retrieval-augmented generation.

## Select, then copy

**Job:** recover a value without asking a model to generate it.

```text
text → date candidates found by code → model selects candidate → code normalizes it
```

This keeps exact strings in code and gives the model the narrow job of resolving intent.

Examples: dates, names, product IDs, menu items, spans found by a parser.

## Verify

**Job:** compare an assertion with supplied evidence.

```text
claim + source passage → supported? 0.18 → review
```

The evidence must be present. A model cannot verify against a source it was not given.

Examples: citation checks, extracted field checks, answer-versus-source checks, duplicate records.

## Judge once, change policy later

**Job:** preserve judgments so a user or application can change what they mean operationally.

A chat filter can judge each message as conversation, question, hype, spam, spoiler or abuse. One policy may highlight questions and blur spoilers. Another may show spoilers and hide backseat advice. The messages do not need to be judged again.

This pattern makes the boundary visible:

- model output describes the item;
- policy maps descriptions to actions.

## Escalate the unsettled middle

**Job:** automate clear cases while retaining a safe outcome for ambiguous ones.

```text
probability ≥ upper threshold → yes path
probability ≤ lower threshold → no path
otherwise → review
```

Starting values such as 0.7 and 0.3 can make a prototype concrete. Production thresholds come from labeled cases, error costs and capacity for review.

## Ask several independent questions together

If several questions inspect the same state, many APIs can evaluate them in one request. This avoids sending and reading the same state repeatedly.

Do not make one question depend on another answer in the same request unless the API explicitly supports dependencies. Code can ignore speculative answers that turn out not to apply, or issue a second request when one answer determines the next state.
