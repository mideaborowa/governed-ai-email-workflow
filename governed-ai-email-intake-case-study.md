# When AI Wasn't the Hard Part

## Building a governed AI operations system for repetitive email intake

**Olamide Aborowa, MBA, PMP, PSM**

Updated September 2026

This is an operations-led build. It began with a recurring workplace problem,
not with a search for somewhere to use AI: employees spend substantial time
reading inconsistent requests and repeatedly sending the same first response.

## The business problem

Many companies rely on a dedicated email address for a specific operational issue. An employee scans each message, determines what the customer needs, checks whether enough information is available, and often pastes a nearly identical first response.

The writing is repetitive. Understanding the customer is not.

Customers omit facts, describe the wrong part of the problem, write emotionally, reference earlier interactions, attach partial evidence, or use language that does not match internal terminology. A useful system must handle that variation without inventing facts or surrendering operational control.

The operational question became:

> Can this reduce time spent answering repetitive emails without creating new problems?

The practical ambition is for an operator to review approximately 20 consequential or uncertain cases instead of manually writing 100 repetitive responses, while maintaining accuracy high enough to earn lasting operational trust.

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
- If the case lacks enough information to investigate, code prepares an Approved Information Request. The system labels this outcome Template Auto Ready.
- If the message is unsupported or extraction is uncertain, the system routes it to Human Review.

This is intentionally granular. Its value comes from performing one repetitive operational task consistently and safely.

## Why approved wording matters

Even a correct model-generated response can vary from one run to another. In governed operations, that variability can create training problems, inconsistent customer experiences, and unnecessary risk.

The current workflow uses the model for judgment and code for wording. The response template is approved in advance, and deterministic logic requests only facts that remain missing. If a customer has already supplied usable evidence, the system does not ask for it again.

Consistency is treated as an operational requirement, not a limitation.

## Architecture evolution

The system architecture evolved from:

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

The September 2026 evaluation of workflow version 1.3 produced 96.0% route accuracy, 100.0% auto-ready precision, and 94.2% eligible automation coverage on the fixed 100-email regression set. There were no false auto-ready outcomes. The four remaining errors were conservative human-review escalations. This is a controlled regression result, not a production-performance claim.

Testing then expanded to a combined 300-case evaluation: the fixed 100-email
regression set plus a separate 200-case holdout set. Workflow version 1.14
achieved 97.3% route accuracy, 97.2% auto-ready precision, and 98.3% eligible
automation coverage. It also produced five false auto-ready outcomes and three
unnecessary Human Review routes.

That result was valuable precisely because it was imperfect. The broader set
revealed a new failure layer that the smaller regression milestone did not. The
five false-auto cases were treated as safety failures and used to refine the
next workflow version. Version 1.15 has not yet received a full 300-case rerun,
so the result is reported as a dated evaluation milestone, not as current
production performance.

## The most important lesson

LLMs are easier to use for extraction than to govern as writers.

The system improved when the question changed from:

> Can the AI write a good response?

to:

> Can the workflow prove that this is the right kind of response, using approved language, for a supported situation?

That distinction turns AI from an unpredictable author into a bounded component of an operational system.

## Why this work is worth sharing

The significance is not a claim that email automation is new. It is the attempt
to make a narrow form of automation dependable enough for real operational
trust.

My professional background is in operations rather than corporate technology.
That led me to treat accuracy, consistency, exception handling, operator control,
and measurable evidence as product requirements from the beginning. The result
is not merely a concept or a generated demonstration: it is a working prototype
with repeatable evaluation, documented failure modes, and explicit limits on AI
authority.

The project also demonstrates what becomes possible when people closest to an
operational problem can use modern AI and software tools to test their own
solutions. Domain judgment still matters. Tools expand who can turn that
judgment into a working, measurable system.

## Broader direction

Parking is the proving ground, not the destination.

The reusable pattern can support other dedicated intake channels, including insurance claims, maintenance requests, billing inquiries, warranty claims, human-resources requests, and similar workflows. Each new application must define its supported scope, required facts, approved templates, escalation conditions, and human authority before implementation begins.

The system is being developed one highly reliable operational slice at a time.

## Current priorities

1. Preserve zero false auto-ready outcomes.
2. Confirm performance across repeated and fresh email collections.
3. Improve automation coverage without reducing precision.
4. Reduce unnecessary human review without weakening safety.
5. Measure repeatability across multiple runs.
6. Improve local inference latency, throughput, and operator experience.
7. Add new industry workflows only after the current slice is demonstrably trustworthy.

## Conclusion

The strongest operational AI systems do not ask the model to replace the decision-maker. They use the model to prepare and organize information while code and people retain authority.

My Office Intern is a working prototype that makes this balance measurable, reusable, and trustworthy.

Thoughtful conversations about governed operational AI, potential pilots,
collaboration, or relevant professional opportunities are welcome through
[LinkedIn](https://www.linkedin.com/in/mideaborowa/).
