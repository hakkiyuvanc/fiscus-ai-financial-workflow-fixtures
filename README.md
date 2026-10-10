---
language:
- tr
- en
license: cc-by-4.0
pretty_name: FISCUS AI Financial Workflow State Fixtures
task_categories:
- text-classification
tags:
- finance
- accounting
- fintech
- synthetic
- audit-trail
- human-in-the-loop
- turkish
size_categories:
- n<1K
configs:
- config_name: default
  data_files:
  - split: test
    path: data/financial_workflow_state_fixtures.jsonl
---

# FISCUS AI Financial Workflow State Fixtures

This small, fully synthetic reference dataset demonstrates how finance-critical workflow events can be classified without confusing an AI suggestion, a user approval, an external-provider response, and a committed accounting effect.

The fixtures are intended for:

- validating deterministic workflow guards;
- testing human-in-the-loop finance assistants;
- reviewing retry and idempotency behavior;
- checking that user-facing status matches the source-of-truth state;
- verifying that audit events remain reconstructible.

It is **not** a training benchmark, a collection of real transactions, accounting advice, tax advice, or a substitute for provider and regulatory validation.

## Data origin

All rows are hand-authored synthetic scenarios. They contain no customer records, bank data, invoice identifiers, taxpayer identifiers, personal data, model outputs from production, or confidential provider responses.

## Schema

| Field | Meaning |
|---|---|
| `case_id` | Stable synthetic fixture identifier |
| `domain` | Finance workflow surface |
| `initial_status` | Source-of-truth state before the event |
| `event` | Observed or requested transition event |
| `external_result` | Provider/system outcome when applicable |
| `approval_state` | Human or policy approval state |
| `expected_status` | Expected state after guard evaluation |
| `financial_effect` | Whether a committed financial effect exists |
| `retry_policy` | Safe retry behavior |
| `audit_required` | Whether the transition must create an audit event |
| `reason_code` | Stable machine-readable rationale |
| `rationale_tr` | Short Turkish explanation |

## Core semantics

The fixtures deliberately preserve these distinctions:

1. `suggested` is decision support, not an accounting fact.
2. `approved` does not imply that an external operation was committed.
3. `unavailable` means the result is unknown; it must not be presented as a negative result.
4. A retry must not duplicate an already committed financial effect.
5. Reversals, cancellations, and corrections remain explicit state transitions rather than destructive rewrites.
6. Live bank and e-document actions require the relevant plan, organization authority, business eligibility, provider readiness, and user approval.

## Example

```json
{
  "case_id": "bank_reconciliation_001",
  "domain": "bank_reconciliation",
  "initial_status": "suggested",
  "event": "user_approves_match",
  "external_result": "not_required",
  "approval_state": "approved",
  "expected_status": "approved",
  "financial_effect": "none_until_commit",
  "retry_policy": "not_applicable",
  "audit_required": true,
  "reason_code": "APPROVAL_IS_NOT_COMMIT",
  "rationale_tr": "Kullanıcı onayı eşleştirmeyi yetkilendirir; kalıcı muhasebe etkisi ayrı commit adımından sonra oluşur."
}
```

## Responsible use and limitations

- Treat the rows as illustrative test fixtures, not universal accounting rules.
- Add jurisdiction, organization, role, amount, tax, document-type, and provider-specific guards before production use.
- Do not infer regulatory eligibility from a missing or unavailable provider response.
- Do not use these fixtures to auto-post ledger entries without explicit domain validation and authorization.
- A passing fixture suite does not prove legal, tax, accounting, security, or production readiness.

## Project context

The state model reflects the controlled-automation principles used by [FISCUS AI](https://fiscusai.org/), an AI-supported financial operating system for Turkish SMEs. Product availability and live integrations remain conditional on plan, organization authority, business eligibility, provider readiness, and user approval.

## License

The dataset card and synthetic fixtures are released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

