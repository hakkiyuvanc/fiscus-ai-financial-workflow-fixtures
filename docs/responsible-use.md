# Responsible use

All 25 rows are hand-authored synthetic scenarios. They contain no customer records, bank data, invoice identifiers, taxpayer identifiers, personal data, production model output, provider secrets, or live accounting records.

## Limitations

- Treat the rows as illustrative test fixtures, not universal accounting rules.
- Add jurisdiction, organization, role, amount, tax, document-type, and provider-specific guards before production use.
- Do not infer regulatory eligibility from a missing or unavailable provider response.
- Do not use the fixtures to auto-post ledger entries without explicit domain validation and authorization.
- A passing fixture suite does not prove legal, tax, accounting, security, or production readiness.

The material is not accounting, tax, legal, or investment advice. It is a compact public artifact for testing controlled and auditable financial automation.
