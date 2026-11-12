# Review queue lab

A yes/no judgment becomes useful only after the application decides what to do with uncertainty.

## Job

Given a customer message, judge this statement:

> The customer explicitly asks for a refund.

The lab has checked positive and negative examples, including policy questions, complaints, exchanges and indirect requests.

## Three outcomes

```text
probability ≥ upper threshold → refund path
probability ≤ lower threshold → not-refund path
between thresholds           → human review
```

Two sliders change the thresholds. The page updates:

- automatic yes decisions;
- automatic no decisions;
- review volume;
- false positives;
- false negatives.

The reader can choose a policy that matches the cost of each mistake.

## What this teaches

- A probability is not the action.
- One threshold is not mandatory.
- Higher automation usually increases at least one kind of error.
- Calibration and ranking are different properties.
- A useful evaluation includes the cases that remain for people.

## Evidence

The lab keeps tuning and held-out examples separate and plots results only after the evaluation protocol is fixed. It reports the distribution of answers rather than one average accuracy number.
