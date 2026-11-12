# Evidence

A polished demonstration can make a model understandable. It cannot establish that the model is good enough for a job.

## Four different claims

### The interface works

A request was accepted and returned the documented shape.

Evidence: exact request, exact response, model identifier, API or runtime version and date.

### The implementation matches a reference

Two runtimes produced equivalent results on a fixed corpus.

Evidence: pinned artifacts, corpus, tolerances, raw differences, environment and reproducible commands.

This is what GLiNER Runner's ONNX parity receipts establish. They show that its Node runtime reproduces its PyTorch reference within the stated tolerance. They do not establish that either answer is correct for a user's task.

### The model performs on a benchmark

A model was scored against labeled cases under a defined metric.

Evidence: dataset provenance, held-out split, exact task construction, metric, per-task results, failures and enough detail to rerun the evaluation.

A benchmark published by the model maker is useful evidence with a conflict-of-interest caveat. A leaderboard number without task construction and raw outputs is weak evidence.

### The application is safe and useful

The complete workflow behaves acceptably on the population and conditions where it will be used.

Evidence: representative application data, human labeling guidance, error costs, thresholds, review capacity, drift monitoring and a fallback path.

No generic benchmark can settle this claim.

## Every lab records

- the user-visible job;
- the exact state, questions, options and criteria;
- provider, model ID, immutable revision when available, runtime and date;
- raw answers, not only the selected answer;
- expected answers and who supplied them;
- which cases were used to tune wording or thresholds;
- a separate held-out set;
- the policy that maps judgments to actions;
- errors by kind, including null and ambiguous cases;
- latency and cost measurement conditions;
- known limitations and failed examples;
- a replay format that does not require credentials.

## A demonstration should label its status

- **Illustration:** invented values used to explain an interface.
- **Recorded run:** real output from a named model on a named input.
- **Checked example:** a recorded run with a stated expected answer.
- **Evaluation:** a defined set of checked examples with an aggregate result.
- **Application evidence:** an evaluation on representative data with an operational policy.

“Potential output” is an illustration, not a recorded run. Real scores are a recorded run, not automatically a checked example.

## Accuracy is not one thing

The metric must match the job.

- Pick one: accuracy, per-class recall, confusion matrix.
- Several labels: exact match, per-label precision and recall, subset accuracy.
- Yes/no gate: precision and recall at each proposed threshold, calibration, review rate.
- Ordered score: mean absolute error and the full predicted distribution.
- Ranking: ranking metrics and inspection of the top results.
- Workflow: wrong-action rate, missed escalation rate, review volume, latency and cost.

A single average can hide a class that never works.

## Question changes are model changes

Changing any of these can change the output distribution:

- question wording;
- option names or descriptions;
- task name;
- state fields or truncation;
- model version;
- runtime preprocessing;
- answer constraints;
- threshold or policy.

Keep the exact payload and rerun held-out cases after a change. Do not tune wording until a few visible examples return the desired numbers and call that validation.

## Confidence is not correctness

Some APIs return a top probability, some return a separate confidence statistic, and some use “confidence” as a general label. Record the provider's definition. If it is not defined, treat it as an opaque model output until measured.

Thresholds should follow the cost of errors. Blocking a harmless message, missing a dangerous action and sending an ordinary ticket to review have different costs. Report each outcome rather than hiding them in one score.
