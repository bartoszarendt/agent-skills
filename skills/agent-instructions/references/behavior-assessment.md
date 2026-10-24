# Behavior assessment

Use this when a guidance change is consequential enough to evaluate in runs,
or when judging whether a skill or rule helps at all. A narrow correction needs
only the walkthrough in the main file.

Decide first which question the runs answer:

- **Regression:** does the changed guidance still produce the expected
  decisions? Realistic cases fit, including cases about finding, interpreting,
  or acting on evidence the agent can reach. A case that every variant passes
  still guards against regression and can show a difference in cost.
- **Improvement:** does the change, or the skill, give more accurate results,
  or acceptable results at lower cost, than the unchanged guidance? This needs
  the comparison and repetition below, scaled to how consequential the claim is.

## What a result can establish

Keep four questions apart for each case:

- **Available:** the guidance was installed and discoverable where the agent ran.
- **Loaded:** the agent read it, or the reference the case needed.
- **Applied:** the decision it governs followed it.
- **Effective:** applying it gave a more accurate result, or an acceptable one
  at lower cost, than the unchanged guidance.

A usage record can show the first two at most. Missing usage records mean the
use is unmeasured, not that the guidance is unused.

## Choose cases

- Ordinary requests where the guidance should apply, worded as a user would
  write them, with nothing that points at what the case tests. A request that
  names the uncertainty prompts every variant to handle it.
- Nearby requests the guidance should not affect.
- A request that conflicts with a default the guidance sets. Precedence and
  authorization decide the correct outcome: following the user's explicit,
  authorized instruction is correct even where it departs from the default.
- An authorization or evidence limit.
- For an accuracy claim, cases the unchanged guidance could plausibly get
  wrong: a case it already handles correctly shows no gain in accuracy. When
  the deciding fact is the user's, provide someone to ask who answers only what
  is asked. For an efficiency claim, cases both versions handle acceptably,
  compared on cost.
- Where you can, start with one deciding fact or step per case, so a result
  points at its cause; combine them when the behavior under test is the
  combination.

## Set up the runs

- Control the configuration. Install or inject the guidance under test, and
  keep other instructions, skills, and tools the same in every variant, or
  record where they differ.
- Write the expected outcome before seeing any result, from what the user needs
  rather than in the guidance's own terms. A pass criterion that reuses the
  guidance's vocabulary can only confirm it.
- Check any automated scoring first: a known-good result passes, while the
  starting state and a plausible wrong result fail.
- Score the delivered result and the consequential actions. Score the order of
  steps only where that order protects a real contract.

## Measure an improvement

- Run each case on the unchanged guidance as well as the changed one. When the
  change interrupts the agent or adds steps and the claim concerns what it
  says, a variant that interrupts as often with generic content separates the
  effect of stopping from the effect of the content.
- Repeat each case, and decide before running how many runs and what
  difference will count. Do not extend a run because its result is close.
- A case that every variant passes, or every variant fails, shows no
  difference in accuracy between them; it can still show one in cost.

## Read the results

- Describe each run by what was observed: correct, with the guidance
  observably applied; correct without it applied; the needed fact or step
  obtained but the result still wrong; the agent pursued the wrong fact; the
  guidance loaded but not applied where the case needed it; or the guidance not
  loaded where the case needed it. A single run shows what happened, not why;
  attribute a result to the guidance only from a pattern across runs and
  variants.
- For a regression check, one run per case can be enough when the decision is
  clear; repeat a case whose result is close or varies between runs.
- Report the cost beside the effect, such as added turns, questions,
  interruptions, or tokens.
- State what the runs cannot show, such as cases written by someone who knew
  the guidance, or effects too small for the number of runs.
