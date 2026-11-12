# Inbox lab

A small support inbox makes the model/code boundary visible.

## What the reader sees

Twelve messages arrive in an unassigned tray. Each card shows:

- the message;
- topic scores;
- independent property judgments;
- urgency levels;
- the queue selected by the current policy.

The reader changes the policy and watches cards move without calling the model again.

## Questions

### Topic

Pick one ownership topic:

- billing;
- account access;
- shipping;
- product problem;
- general question.

### Independent properties

- Does the customer ask for money back?
- Is the customer unable to use the product or account?
- Does the message mention a deadline?
- Does the customer sound frustrated?

These are judgments. “Should a person handle this?” is deliberately absent.

### Urgency

- routine;
- important;
- urgent;
- critical.

Each level will have a standalone description.

## Starting policy

```text
unable to use account and billing topic → urgent billing
unable to use product                    → urgent product
refund requested                         → billing
high frustration                         → human review
otherwise                                → topic queue
```

The reader can change the order and thresholds. The lab explains that changing policy does not change what the model observed.

## Cases

The set must include:

- an obvious billing request;
- an obvious shipping request;
- one message with billing and account-access content;
- a frustrated message with no urgent operational problem;
- an urgent deadline stated calmly;
- a message that fits none of the ownership topics;
- an ambiguous message;
- a case where a model answer is wrong.

## Evidence

Two people will label the questions independently before model outputs are examined. Disagreements remain visible. Tuning cases and held-out cases stay separate.

The lab reports both judgment errors and final routing errors. A correct topic can still produce a bad route if the policy is wrong.
