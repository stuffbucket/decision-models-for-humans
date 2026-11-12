# Decision models for humans

Read this message:

> I was charged twice, and now I cannot open my account to see the invoices.

You can probably tell, without working through a set of rules, that it is about **billing** and **account access**. You can also tell that it is more urgent than a question about changing a mailing address.

A decision model gives software that kind of bounded judgment. The software supplies the message and the possible answers. The model scores those answers. Ordinary code decides what happens next.

Illustration — the values below are invented:

```text
message
  ↓
Pick every topic that applies
  billing       0.91
  account       0.84
  shipping      0.03
  product       0.02
  ↓
code sends it to the billing queue and adds the account-access tag
```

The model does not write the reply. It does not invent a queue. It scores answers the application supplied.

## Model judges; code decides

This distinction is the most useful way to understand a decision model.

Depending on the model, it can answer narrow questions about language, images or application state:

- Which topic fits this message?
- Does this message ask for a refund?
- How severe is the reported problem?
- Which of these records refers to the same person?
- Is this answer supported by the quoted passage?

Code keeps the policy:

```text
if payment is blocked → urgent queue
else if refund requested and customer is frustrated → human review
else if refund requested → billing queue
else → normal support queue
```

The model supplies the judgments on the left side of those rules. The rules remain visible, testable and changeable.

## Three shapes cover many jobs

Different providers use different names, but most text decision APIs include these shapes:

1. **Pick one** — billing, account, shipping or product.
2. **Yes or no** — does the message ask for a refund? The answer is a probability.
3. **Pick a level** — routine, important, urgent or critical.

Some models also support several answers at once, constrained combinations of answers, locations in images, or candidate selection over large lists.

## Jobs that fit

Decision models are useful when a person could look at the supplied information and make a quick, bounded call:

- sort messages into queues;
- tag every topic a review mentions;
- filter or highlight live chat;
- choose a tool or handler for a request;
- check whether a claim is supported by evidence;
- rank search results against a description;
- select a value from candidates found by ordinary code;
- score several visible qualities, then combine them in code;
- send uncertain or risky cases to a person.

They are usually the wrong tool for writing replies, summarizing documents, doing arithmetic, looking up missing facts, or answering questions whose possible answers are not known in advance.

## Start here

- [The mental model](docs/mental-model.md) — bounded judgment without the classifier vocabulary.
- [The recurring patterns](docs/patterns.md) — route, gate, score, rank, verify and escalate.
- [Models and runtimes](docs/models.md) — Jev, GLiNER2.5 Decide, Microsoft Decision-1, GPT-6 Luna Decisions, open Decision 1.0 models and the software that runs them.
- [Evidence](docs/evidence.md) — what a demonstration proves, what a benchmark proves and what neither proves.
- [Example design](docs/example-design.md) — the information every useful demonstration should expose.
- [Resources](RESOURCES.md) — a small, checked set of primary sources and broader directories.

## Labs

The first labs are designed around visible outcomes rather than model terminology:

- [Inbox](examples/inbox/README.md) — classify topic and urgency, then change the routing policy.
- [Chat filter](examples/chat-filter/README.md) — judge messages once, then switch between show, dim, blur and hide without calling the model again.
- [Review queue](examples/review-queue/README.md) — use labeled cases to choose thresholds and send unsettled cases to a person.

The labs are specifications first. Runnable versions will keep recorded, attributable model outputs so readers can inspect them without an API key or a large model download.

## Scope

This repository is model-neutral. It covers hosted and local decision models, including:

- TypeSafe Jev and its System One question shapes;
- Fastino GLiNER2.5 Decide models and [GLiNER Runner](https://github.com/stuffbucket/gliner-runner);
- Microsoft Decision-1;
- OpenAI GPT-6 Luna Decisions;
- open Decision 1.0 models such as Sol-2B;
- other models when their interface, provenance and evidence can be checked.

This is not an exhaustive awesome list. Existing lists already track the fast-moving catalog. This repository concentrates on understanding, building and testing.

## Contributing

A useful contribution makes a job easier to picture or a claim easier to verify. See [CONTRIBUTING.md](CONTRIBUTING.md).

Apache-2.0.
