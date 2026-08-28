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
- Expected workflow route
- Expected automatic-template eligibility

The expected labels should ultimately be approved by an owner of the real operational process.

## Primary metrics

### Exact-case accuracy

The percentage of cases in which every evaluated extraction field and the final route match the expected labels.

This is intentionally strict. A case with a correct route but an incorrect evidence field is not counted as an exact match.

### Route accuracy

The percentage of cases routed to the expected operational outcome:

- Template Auto Ready
- Human Review Assisted
- Human Review Needed

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

## Current evidence

The current preliminary 20-case engineering benchmark reports:

| Metric | Result |
|---|---:|
| Exact-case accuracy | 95.0% |
| Route accuracy | 100.0% |
| Extraction-field accuracy | 99.17% |
| Auto-ready precision | 100.0% |
| Eligible automation coverage | 100.0% |
| False auto-ready outcomes | 0 |

These numbers are promising engineering evidence. They are not yet a statistically supported production claim because the fixture is small and its labels are pending independent operational approval.

## Release standard

A workflow should not advance merely because its average score is high. Release requires:

- No known unsafe auto-ready case in the approved benchmark
- Operations-approved expected labels
- Stable results across repeated runs
- Documented unsupported-case behavior
- Auditable routing reasons
- A clear rollback path
- Human control over external investigation and consequential decisions
