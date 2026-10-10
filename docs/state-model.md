# State model

The fixtures describe expected transitions across finance workflows. They are validation examples, not a replacement for backend domain rules.

## Core distinctions

1. `suggested` is decision support, not a committed accounting fact.
2. `approved` authorizes a possible next step but does not prove that an external operation committed.
3. `unavailable` means the provider result is unknown; it must not be presented as a negative result.
4. A retry must not duplicate an already committed financial effect.
5. Reversals, cancellations, and corrections remain explicit transitions rather than destructive rewrites.
6. Live bank and e-document actions require the relevant plan, organization authority, business eligibility, provider readiness, and user approval.

## Minimal record structure

Each JSONL row provides a stable `case_id`, domain, initial state, event, provider result, approval state, expected state, financial-effect classification, retry policy, audit requirement, machine-readable reason code, and a short Turkish rationale.

These fields make the expected transition and its audit obligation reviewable without presenting a model recommendation as financial truth.
