# When AI Wasn't the Hard Part

## Building toward a 95%-accurate governed email-intake workflow

**Olamide Aborowa, MBA, PMP, PSM**

Updated September 2026

## The business problem

Many companies rely on a dedicated email address for a specific operational issue. An employee scans each message, determines what the customer needs, checks whether enough information is available, and often pastes a nearly identical first response.

The writing is repetitive. Understanding the customer is not.

Customers omit facts, describe the wrong part of the problem, write emotionally, reference earlier interactions, attach partial evidence, or use language that does not match internal terminology. A useful system must handle that variation without inventing facts or surrendering operational control.

The product question became:

> Can this reduce time spent answering repetitive emails without creating new problems?

The practical ambition is for an operator to review approximately 20 consequential or uncertain cases instead of manually writing 100 repetitive responses—while maintaining accuracy high enough to earn lasting operational trust.

## The original assumption

The first concept was straightforward:

```text
Email arrives → AI understands it → AI writes the answer
```

That approach produced fluent responses, but fluency was not the same as reliability. The model could make unsupported claims, vary approved language, infer business decisions, or respond confidently to a use case the system did not actually support.

The problem was not simply choosing a better model. It was deciding what authority the model should have.

## The central design decision

The workflow now separates understanding from control:

- **LLM:** interpret inconsistent language, extract evidence-backed facts, summarize intent, and identify missing information.
- **Code:** validate structure, enforce business rules, determine routing, and select approved response wording.
- **Operator:** investigate external systems and retain authority over consequential decisions.

The LLM became a capable analyst inside a governed process rather than an autonomous representative of the company.

## Choosing the smallest useful operational slice

Parking management became the first proving ground. The initial slice does not attempt to decide whether a parking violation is valid. It handles intake before that investigation can occur.

For a supported first-contact violation inquiry:

- If a plausible violation number is supplied, the operator can research the company system.
- If the message is a follow-up or references a prior decision, the operator should review the history.
- If the case lacks enough information to investigate, code prepares an approved information-request response.
- If the message is unsupported or extraction is uncertain, the system routes it to human review.

This is intentionally granular. Its value comes from performing one repetitive operational task consistently and safely.

## Why approved wording matters

Even a correct model-generated response can vary from one run to another. In governed operations, that variability can create training problems, inconsistent customer experiences, and unnecessary risk.

The current workflow uses the model for judgment and code for wording. The response template is approved in advance, and deterministic logic requests only facts that remain missing. If a customer has already supplied usable evidence, the system does not ask for it again.

Consistency is treated as a product feature—not a limitation.

## Architecture evolution

The project evolved from:

```text
LLM → Customer response
```

to:

```text
Email intake
  → constrained extraction
  → evidence validation
  → deterministic routing
  → approved template or operator brief
  → human-controlled workflow
```

The surrounding system now includes strict schemas, validation rules, workflow state, queue management, audit history, operator controls, and repeatable evaluation.

Most of the engineering work occurs around the model because that is where operational trust is created.

## What testing revealed

Early versions routed nearly every message to the same outcome and sometimes classified identical emails differently. Legal or emotional wording could dominate the underlying operational need. Information that customers had already supplied could be requested again.

The governed redesign produced materially better separation between:

- First-contact cases eligible for approved information gathering
- Cases ready for operator research
- Unsupported or uncertain cases requiring human judgment

Early synthetic and exploratory tests helped expose failure modes, but they are not presented as current performance or as an operations-owned accuracy claim.

The evaluation process has since moved to a fixed 100-email regression set with permanent case numbers, saved email content, and an operations-owned answer key. This prevents the test population from changing as the inbox changes. The system can replay named regression sets, test new inbox batches separately, and show progress while a batch runs.

The first verified comparison, completed September 1, 2026, produced 86.0% route accuracy, 91.2% auto-ready precision, and 88.6% eligible automation coverage. Six cases were incorrectly made auto-ready, and eight eligible cases were unnecessarily retained for human review. This controlled baseline is not a production-performance claim; it identifies exactly where the system-correction phase must begin.

## The most important lesson

LLMs are easier to use for extraction than to govern as writers.

The project improved when the question changed from:

> Can the AI write a good response?

to:

> Can the workflow prove that this is the right kind of response, using approved language, for a supported situation?

That distinction turns AI from an unpredictable author into a bounded component of an operational system.

## Broader product direction

Parking is the proving ground, not the destination.

The reusable pattern can support other dedicated intake channels—insurance claims, maintenance requests, billing inquiries, warranty claims, human-resources requests, and similar workflows. Each new application must define its supported scope, required facts, approved templates, escalation conditions, and human authority before implementation begins.

The product is being built one highly reliable operational slice at a time.

## Current priorities

1. Reduce false auto-ready outcomes toward zero.
2. Raise auto-ready precision above 95%.
3. Raise route accuracy above 95%.
4. Improve automation coverage without reducing precision.
5. Measure repeatability across multiple runs.
6. Improve local inference latency, throughput, and operator experience.
7. Add new industry workflows only after the current slice is demonstrably trustworthy.

## Conclusion

The strongest operational AI systems do not ask the model to replace the decision-maker. They use the model to prepare and organize information while code and people retain authority.

My Office Intern is an experiment in making that balance measurable, reusable, and trustworthy.
