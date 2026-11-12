# Example design

A useful example lets a reader see the whole path from information to visible behavior.

## Show these seven things

1. **The moment:** what a person or application is trying to do.
2. **The state:** exactly what the model can inspect.
3. **The judgment:** one plain question and its allowed answers.
4. **The distribution:** all relevant scores, not only the winner.
5. **The policy:** ordinary code or a small truth table.
6. **The outcome:** what changes on screen or in the workflow.
7. **The evidence:** whether values are invented, recorded, checked or evaluated.

If the model is replaced with a hidden magic box, the example teaches little. If the example ends at a JSON response, it shows no reason to care.

## Lead with the outcome

Weak opening:

> A classifier assigns input text to one or more labels.

Stronger opening:

> A new support message arrives. It appears in the billing queue, with account access marked as a second problem. An ambiguous message waits for review.

The second version gives the reader a scene they can recognize before introducing labels, tasks or thresholds.

## Let the reader change policy

One set of judgments can support several policies. A chat example should let the reader map categories to show, dim, blur or hide. An inbox example should let the reader move urgent account problems from the normal queue to a human queue.

When the screen changes without rerunning the model, the distinction between judgment and decision becomes concrete.

## Include the null and mixed cases

Easy examples make every model look good. Include:

- one obvious case;
- one case where two labels apply;
- one case where no label fits;
- one ambiguous case;
- one case the model gets wrong;
- one case where missing state prevents a responsible answer.

A wrong answer with a clear explanation teaches more than a gallery of perfect outputs.

## Make “be the model” measurable

A reader-facing prediction exercise can collect a human answer before revealing the model answer:

1. show the state and allowed answers;
2. ask the reader to choose;
3. reveal the model distribution;
4. reveal the reference label and its source;
5. explain disagreements;
6. aggregate anonymous local results only if the page clearly says what is stored.

Without a reference answer, a real model score proves only that the model emitted that score. It does not show that the model understood the case.

## Games are secondary demonstrations

A guessing game can demonstrate ranking or hierarchical search, but the implementation is hidden behind the game. If kept, expose:

- the current candidates;
- the model's probability distribution;
- the code's search rule;
- why a candidate was guessed next;
- the known answer set and held-out success rate.

A game should point to a corresponding ordinary job, such as searching a catalog from a vague description. The ordinary job belongs first.

## Keep technical layers available, not compulsory

The first view should show the moment, judgment, policy and outcome. Expandable details can show:

- provider-specific request JSON;
- command-line examples;
- timing and cost;
- model and artifact revisions;
- raw replay data;
- evaluation method.

A reader should understand the job without reading an API schema. A builder should still be able to inspect every value.
