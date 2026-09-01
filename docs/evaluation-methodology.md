# Evaluation Methodology

## Purpose

Evaluation is treated as part of the product architecture. The goal is not simply to measure whether a model produced plausible text; it is to determine whether the complete governed workflow behaves safely, consistently, and usefully.

## Unit of evaluation

Each case contains an anonymized customer email and an expected set of operational labels:

- Inquiry type
- Prior-contact status
- Research-ready identifier status
- Evidence supplied
- Missing information
- Expected operational handling
- Expected automatic-template eligibility

The expected labels should ultimately be approved by an owner of the real operational process.

## Primary metrics

### Exact-case accuracy

The percentage of cases in which every evaluated extraction field and the final route match the expected labels.

This is intentionally strict. A case with a correct route but an incorrect evidence field is not counted as an exact match.

### Route accuracy

The percentage of cases routed to the expected operational handling:

- Template Auto Ready
- Human Review

The interface may distinguish between review cases with or without an AI-prepared operator brief. That distinction can be useful to the operator, but it is not a separate pass-or-fail routing label in the current evaluation.

### Extraction-field accuracy

Accuracy across the individual structured fields used by deterministic routing.

### Auto-ready precision

Of all cases declared eligible for an automatic approved template, the percentage that were genuinely eligible.

This is one of the most important safety metrics because a false automatic response can create a customer-facing error.

### Eligible automation coverage

Of all cases that were genuinely eligible for the approved template, the percentage the system successfully automated.

### False auto-ready count

The number of cases that received an automatic-ready outcome when they should have remained under human control.

The target is zero.

### Repeatability

The percentage of repeated identical inputs that produce the same structured extraction and routing outcome across multiple runs.

### Latency

Average and percentile processing time per email. Accuracy is the first constraint, but operational value also depends on usable throughput.

## Validation ladder

Evaluation progresses through increasingly realistic stages:

1. Deterministic unit tests for routing and template rules
2. Small labeled engineering fixtures
3. Repeated model runs for consistency
4. Larger anonymized operational datasets
5. Adversarial and ambiguous inputs
6. Operations-owner label review
7. Shadow-mode deployment with no automatic sending
8. Narrow production pilot with monitoring and rollback controls

## Current regression evaluation

The current evaluation uses a fixed 100-email regression set. Each case has a permanent case number, saved email content, and an expected handling decision owned by operations. This allows the same cases to be rerun even when the Gmail inbox changes.

The first verified comparison was completed on September 1, 2026:

| Metric | Result |
|---|---:|
| Fixed cases | 100 |
| Correct routes | 86 |
| Route accuracy | 86.0% |
| Auto-ready precision | 91.2% |
| Eligible automation coverage | 88.6% |
| False auto-ready outcomes | 6 |
| Unnecessary human reviews | 8 |

The rerun contained all 100 fixed cases with no missing, additional, or changed emails. Each mismatch was reviewed against the operations-owned answer key. These results establish a controlled correction baseline; they are not a production-performance claim.

New inbox batches are tested separately and can be preserved as future named sets. Earlier exploratory tests informed the current design but are not presented as current performance.

## Release standard

A workflow should not advance merely because its average score is high. Release requires:

- No known unsafe auto-ready case in the approved benchmark
- Operations-approved expected labels
- Stable results across repeated runs
- Documented unsupported-case behavior
- Auditable routing reasons
- A clear rollback path
- Human control over external investigation and consequential decisions
