# The mental model

## Start with a moment, not a model

A person glances at a message and notices that it is angry. They see a photograph and notice a cracked screen. They read two records and notice that they describe the same customer.

These are judgments. They use context and ordinary experience, but the answer is small: yes or no, one option, a level, or a few applicable tags.

A decision model makes bounded judgments over information supplied by an application.

```text
state + question + allowed answers → scored answers
```

- **State** is what the model can inspect: text, structured data and, for some models, images.
- **Question** names one judgment.
- **Allowed answers** define the boundary.
- **Scores or probabilities** let code compare answers and handle uncertainty.

## The human test

Ask whether a person shown only the same state and question could answer quickly by intuition.

Good fits:

- Which team should receive this message?
- Does this paragraph support the claim?
- How upset does the customer sound?
- Which menu item does this phrase name?

Poor fits:

- What should the company do? The answer depends on policy that belongs in code.
- What is the account balance? Use an exact lookup.
- What happened last quarter? The needed facts are missing.
- Write a tactful reply. The output is open-ended text.

When the human test fails, improve the state, narrow the question, or use another tool.

## System 1 is an analogy

Kahneman used “System 1” for fast, automatic human cognition and “System 2” for slower, deliberate thought. The analogy points toward the right class of task: quick judgments rather than open-ended reasoning.

It is not a claim that a model thinks as a person does. A decision model can be confidently wrong, can miss context a person would need, and can behave unevenly across topics. Its behavior must be measured on the actual job.

## Do not ask the model to own policy

“Should this ticket be escalated?” mixes observation with company policy.

Split it into judgments:

- Is the customer unable to use the product?
- Does the message describe a financial loss?
- Does the customer sound frustrated?
- Is a deadline mentioned?

Then keep the decision in code:

```text
unable_to_use and financial_loss → urgent human queue
financial_loss                    → billing queue
frustrated                        → normal human queue
otherwise                         → automated triage
```

This exposes missing cases and lets the organization change policy without retraining or rewording the model questions.

## One judgment per question

A question such as “Is this fraudulent or dangerous?” joins two properties. Ask them separately. Both may be true, neither may be true, and each may require a different response.

Concrete questions work better than abstract labels:

- “Does the message ask to change bank details?” rather than “Is this fraud?”
- “Is a SQL query assembled by joining untrusted text?” rather than “Is this code insecure?”
- “Does the answer claim a fact absent from the source?” rather than “Is this a bad answer?”

## The model sees only what the application supplies

Useful state contains what a person would inspect:

- the full relevant thread, with speakers named;
- readable product names rather than internal IDs;
- the policy excerpt needed for a verification question;
- the candidate records being compared;
- facts the application already knows.

Irrelevant state is not harmless. It can change the answer. Missing state turns uncertainty into noise.

## The null case matters

A pick-one question always has a winner, even when no option fits. Applications need an explicit way to detect “none of these.” Depending on the model, that may be:

- a separate yes/no question asking whether any option fits;
- a multi-label question that may return an empty set;
- a carefully defined “other” option;
- a review threshold established on labeled cases.

A low top score is not automatically a reliable null detector. Test it.

## Probabilities describe groups, not promises

A probability of 0.8 is not a guarantee about one case. Calibration is a property measured across many comparable cases: among answers assigned about 0.8, roughly 80 percent should be correct.

Providers use the words *probability* and *confidence* differently. Before using either as a gate:

1. define what correct means;
2. collect representative labeled cases;
3. inspect errors at different thresholds;
4. give the middle region an explicit outcome, usually review;
5. repeat after changing the model, question, options or state.

The top answer is often a reasonable starting point. Unattended automation requires evidence from the intended job.
