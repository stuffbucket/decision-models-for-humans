# Chat filter lab

A live chat feed shows why model judgments and application policy should be separate.

## What the reader sees

Each message has recorded judgments:

- message kind: conversation, question, hype, backseat advice, spam or other;
- probability of personal abuse;
- probability of a spoiler.

A policy panel maps those judgments to:

- show;
- highlight;
- dim;
- blur;
- hide.

Changing a mapping updates the feed immediately. The model is not called again.

## Two policies from the same answers

**Streamer mode**

- highlight questions;
- show conversation and hype;
- hide spam, abuse and backseat advice;
- blur spoilers.

**Replay viewer mode**

- highlight useful explanations;
- show backseat advice;
- hide spam and abuse;
- show spoilers because the game is already complete.

The example makes the distinction concrete: the model describes messages, while the user decides how those descriptions affect the screen.

## Cases

The feed includes ordinary conversation, an honest question, playful teasing, direct abuse, disguised spam, solicited advice, unsolicited advice, a likely spoiler and a phrase that only looks like a spoiler without earlier context.

That last case demonstrates missing state. The model cannot know what the viewer has already seen unless the application supplies it.

## Evidence

The lab reports per-property results and the effect of each policy. “Correct model answer” and “acceptable visible outcome” remain separate measurements.

The first version will adapt the pattern in TypeSafe's Twitch chat filter cookbook while using original cases and clearly attributed design ideas.
