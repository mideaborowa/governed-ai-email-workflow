# Governance Model

## Principle

The system separates probabilistic understanding from operational authority.

The LLM may observe, extract, summarize, and classify. Deterministic code decides whether an approved response is eligible. Human operators investigate external systems and make consequential decisions.

## Responsibility boundaries

| Capability | LLM | Code | Operator |
|---|:---:|:---:|:---:|
| Interpret inconsistent customer language | Yes |  |  |
| Extract candidate facts and supporting excerpts | Yes | Validates |  |
| Determine whether required fields are missing | Proposes | Decides |  |
| Select customer-facing wording |  | Yes, from approved templates |  |
| Determine automation eligibility |  | Yes | Can override or stop |
| Investigate a company database |  |  | Yes |
| Approve, deny, waive, or resolve a dispute |  |  | Yes |

## Routing outcomes

### Template Auto Ready

The message belongs to the supported workflow, appears to be a first contact, lacks enough information for investigation, and passes deterministic safety checks. Code constructs the response using approved language and requests only missing information.

### Human Review Assisted

The message contains enough information for operator research, refers to prior correspondence, or benefits from an evidence-backed operator brief.

### Human Review Needed

The message is unsupported, unclear, malformed, or insufficiently reliable for the approved automated path.

## Fail-closed behavior

When extraction is invalid or the use case is outside the approved scope, the system does not improvise a customer response. It keeps the message under human control.

## Risk language

Emotional, legal, or reputational language is recorded as operational context. It does not automatically prove that the customer has supplied research information, and it does not independently authorize or prohibit an approved first-contact response.

The underlying workflow state remains the controlling factor.

## Expansion rule

Before adding a new capability, the team must answer:

1. Can the LLM be limited to observation, extraction, summarization, or classification?
2. Can deterministic logic make the operational decision instead?
3. Does a human need to investigate or approve the outcome?

If those boundaries are not clear, the capability is not ready to implement.
