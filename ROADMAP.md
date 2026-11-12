# Roadmap

## 1. Foundation

- Plain-language mental model.
- Model and interface map.
- Evidence vocabulary.
- Lab specifications.
- Checked primary-source index.

## 2. First interactive lab

Build the chat filter first. It demonstrates the central idea with the least machinery: judge once, change policy later.

- Static replay data.
- Visible state, questions, distributions, policy and outcome.
- Accessible policy controls.
- Provider-native payload inspection.
- Mobile layout and light/dark themes.
- No analytics or remote storage in the first version.

## 3. Inbox and review queue

- Multi-question inbox flow.
- Human labels and disagreement records.
- Threshold and review-rate exploration.
- Recorded outputs from GLiNER Runner and at least one hosted decisions API.

## 4. Reproducible evaluation

- Versioned case format.
- Provider adapters.
- Frozen held-out sets.
- Raw response receipts.
- Evaluation command and report.
- Clear separation between parity, benchmark and application evidence.

## 5. More jobs

Add examples only when they reveal a different pattern:

- select a menu item and fill known options;
- verify an answer against its cited passage;
- rerank search candidates;
- suggest an agent skill;
- gate a proposed tool action;
- classify a long category hierarchy.

## 6. Revisit existing GLiNER Runner demonstrations

- Turn “be the model” into a prediction-and-reveal exercise with reference labels and model failures.
- Keep 20 Questions as a secondary ranking/search demonstration, or replace it with catalog search.
- Link every playful demonstration to an ordinary application using the same pattern.
- Publish the data and evaluation status beside each result.
