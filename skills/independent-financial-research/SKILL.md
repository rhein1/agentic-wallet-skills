---
name: independent-financial-research
description: Create safe, independent financial research plans and artifacts that can inform Agent OS review without executing trades, purchases, or provider actions. Use when the user asks for finance research, bull/bear cases, risk summaries, cited market analysis, or candidate trading/card actions.
user-invocable: true
disable-model-invocation: false
allowed-tools: []
---

# Independent Financial Research

Use this skill to produce research-only finance artifacts. Research may propose candidate actions for later review, but it cannot execute orders, purchases, wallet transfers, x402 payments, or provider dispatch directly.

## Safety Boundary

- Do not provide personalized investment, tax, legal, or financial advice.
- Do not promise returns, guaranteed performance, or guaranteed execution outcomes.
- Do not place trades, cancel orders, fetch card details, make purchases, move wallet funds, or call providers.
- Do not ask for provider passwords, MFA codes, OAuth tokens, account numbers, card values, balances, positions, order identifiers, transaction identifiers, private wallet data, or private provider data.
- Do not vendor or execute third-party research-provider code.
- Do not claim partnership with Fincept, Robinhood, Coinbase, or any other provider unless an explicit verified partnership artifact exists.

## Research Output Contract

Every research artifact should include:

1. Topic and scope.
2. Symbols or assets, if relevant.
3. Source list with citations.
4. Timestamp or freshness note for market-sensitive data.
5. Bull case.
6. Bear case.
7. Key risks and unknowns.
8. Non-advice disclaimer.
9. Candidate actions, if any, marked `executable_directly:false`.
10. Next control-plane step, such as Agent OS review or owner approval.

## Candidate Actions

Candidate actions are suggestions for a later governed workflow. They must always be marked:

```json
{
  "executable_directly": false,
  "requires_review": true,
  "requires_owner_approval": true
}
```

Research output cannot override Agent OS connector policy, approval gates, caps, or receipt requirements.

## Provider Notes

Fincept and similar research providers are external/user-managed candidates until licensing and distribution review is complete. Do not vendor their code, run their runtime, or imply official partnership.

## Safe Response Pattern

Use language like:

```text
This is research only, not financial advice. Any candidate action is non-executable and must go through Agent OS policy review, connector readiness, owner approval, and receipt controls before any live action can occur.
```

If citations or a non-advice disclaimer are missing, treat the artifact as incomplete.
