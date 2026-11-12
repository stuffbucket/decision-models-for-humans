# Models and runtimes

Checked 12 November 2026. This area changes quickly. Follow the linked primary source before choosing a model or writing an integration.

## Interfaces are similar, not identical

A shared vocabulary has emerged around bounded questions:

- pick one option;
- estimate whether a statement is true;
- score against ordered levels;
- ask several independent questions about shared state.

Names and semantics differ. TypeSafe calls its yes/no probability a **Noul**. OpenAI calls the corresponding question a **predicate**. GLiNER2.5 Decide can represent yes/no as labels and can return several independent labels, but its native schema and probability behavior are different. Do not assume that two compatible-looking fields mean the same thing.

## TypeSafe Jev

[Jev](https://docs.typesafe.ai/introduction.md) is TypeSafe's hosted System One model. Its API accepts state plus typed questions and returns typed answers.

Question types documented by TypeSafe include:

- **Choice:** one supplied option;
- **Noul:** probability that a statement is true;
- **Score:** distribution over ordered levels;
- **Box:** location of an object in an image.

The official [agent skill](https://github.com/typesafe-ai/skills/blob/main/skills/typesafe-ai/SKILL.md) contains unusually useful integration guidance: let the model make judgments, keep decisions in code, apply the human test, ask atomic questions, provide the state a person would need, handle the null case and test against representative data.

Jev is hosted and its weights are not open. TypeSafe describes its probabilities as calibrated. Applications still need to measure behavior and thresholds on their own cases.

## Fastino GLiNER2.5 Decide

Fastino publishes three Apache-2.0 models relevant to this guide:

- [GLiNER2.5-Decide](https://huggingface.co/fastino/GLiNER2.5-Decide) — 340M, English;
- [GLiNER2.5-multi-Decide](https://huggingface.co/fastino/GLiNER2.5-multi-Decide) — 287M, multilingual;
- [GLiNER2.5-Decide-1B](https://huggingface.co/fastino/GLiNER2.5-Decide-1B) — about 1B, English.

They take text and a classification schema whose labels are supplied at request time. They support one label, several labels, described labels, several tasks in one request and constrained combinations. They do not generate text.

Fastino reports exact-match results on its `fast-decisions` benchmark: 60.2% for the 340M English model, 59.6% for the 1B model and 56.7% for the multilingual model. These are publisher-reported averages over a publisher-built benchmark. They are useful for orientation, not a substitute for application evaluation. The larger model does not win that average.

[GLiNER Runner](https://github.com/stuffbucket/gliner-runner) runs the three pinned revisions locally through a Python-free Node/ONNX runtime on CPU, or through a Python/PyTorch reference implementation. Its parity evidence tests runtime equivalence. It is not a general model-accuracy claim.

## Microsoft Decision-1

[Microsoft Decision-1](https://labs.ai.azure.com/innovations/microsoft-decision-1/) is a hosted Microsoft Foundry model built from Qwen3.5-9B and post-trained for single-pass decisions. Microsoft presents classification, routing, verification, scoring and workflow control as its main jobs.

Its System One-style endpoint accepts state and questions with supplied criteria. Microsoft reports internal evaluations and use by teams including Xbox Research, but its launch material does not publish enough raw results to independently reproduce the broad performance claims. Treat the figures as vendor-reported until a suitable external evaluation exists.

The model is hosted rather than open-weight.

## OpenAI GPT-6 Luna Decisions

OpenAI's [Decisions API](https://openai.com/index/decisions-api/) uses `gpt-6-luna` for bounded decisions over supplied input.

The documented shapes are:

- **predicate:** probability that a condition is true;
- **choice:** one supplied value plus a distribution;
- **score:** a distribution over ordered levels and a probability-weighted score.

The API can inspect text, structured JSON, conversation items and images. It supports many independent questions over shared input. Choice and score answers include a separate `confidence` field whose relationship to the answer probabilities must not be guessed.

This is a hosted OpenAI decision model. Other GPT-6 models and open models that happen to use “Decision” in their names are not interchangeable with this API.

## vLLM Semantic Router Decision 1.0

The open [Decision 1.0 collection](https://huggingface.co/collections/llm-semantic-router/decision-10-6ab12177bd0002394d8409f9) includes several sizes and base architectures. [Decision-1.0-Sol-2B](https://huggingface.co/vllm-sr/Decision-1.0-Sol-2B) is an Apache-2.0, Qwen3.5-2B-derived model supporting Choice, Noul and Score questions.

Its card reports a weighted score across 54 tasks and 3,766 decisions. The category weights were selected after results were available, so the aggregate should be read with that caveat. The card also says confidence does not guarantee correctness and identifies composition as a weak category.

Open weights make local testing, pinned revisions and independent evaluation possible. `trust_remote_code=True` is a supply-chain decision, not a harmless loading detail; inspect and pin model code before using it.

## Upstage Solar Decide

[Upstage documents Solar Decide](https://console.upstage.ai/docs/models/solar-decide) as a hosted model using a System One-style interface. It belongs in provider comparisons once its current documentation, model identity, probability semantics and evidence have been recorded directly.

“Solar Decide” and “Decision-1.0-Sol-2B” are different products from different organizations.

## Comparison checklist

Before adding a model comparison, record:

| Question | Why it matters |
| --- | --- |
| Hosted or open weight? | Determines privacy, reproducibility and operating model. |
| Exact model ID and revision? | Product aliases and `latest` targets change. |
| Supported state? | Text, JSON, images and conversation history are not interchangeable. |
| Question shapes? | Pick-one, independent yes/no, ordered score and multi-label have different semantics. |
| Null behavior? | A forced choice can look confident when nothing fits. |
| Probability definition? | “Confidence” may be a different statistic. |
| Context and option limits? | Determines which jobs fit without hidden truncation. |
| Price and hardware? | Hosted token price and local memory/latency answer different questions. |
| Public evidence? | Vendor benchmarks, independent benchmarks and application tests support different claims. |
| Data handling? | Local execution, retention, regions and compliance affect deployment. |

A single leaderboard rank cannot answer this checklist.
