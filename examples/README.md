# Labs

Each lab will have two ways to use it:

1. **Replay:** recorded outputs load immediately. No account, API key or model download.
2. **Live:** an adapter sends the same cases to a selected provider or local runtime.

Replay data will include the exact request, raw response, model identity, date and evidence status. Live runs will not silently replace recorded evidence.

## First labs

| Lab | Judgment | Visible outcome | Evidence goal |
| --- | --- | --- | --- |
| [Inbox](inbox/README.md) | Topic, properties and urgency | Messages move between queues | Human-labeled topic and urgency cases |
| [Chat filter](chat-filter/README.md) | Message kind, abuse and spoiler | Show, dim, blur or hide | Per-class errors and policy outcomes |
| [Review queue](review-queue/README.md) | One yes/no property | Act, reject or review | Threshold, calibration and review-rate curves |

## Adapter boundary

A lab describes questions in its own plain data format. Provider adapters translate those questions without pretending their semantics are identical.

Recorded data keeps provider-native request and response payloads alongside a normalized view. If a provider cannot represent a lab's question faithfully, the adapter says so rather than changing the task.

## No leaderboard without a protocol

The labs may compare models only when they use:

- the same visible job;
- equivalent state and answers;
- a checked translation for each provider;
- a frozen evaluation set;
- a metric chosen before results are inspected;
- model and runtime versions;
- raw replayable outputs.

The first goal is understanding. Comparison follows only where the task is genuinely comparable.
