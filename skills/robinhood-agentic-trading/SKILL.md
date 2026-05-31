---
name: robinhood-agentic-trading
description: Plan and review Robinhood Agentic Trading actions through an Agent OS finance policy boundary. Use when the user asks about Robinhood agentic trading, long-equity order review, trading readiness, or governed brokerage connector setup. This skill is instruction-only and must not place trades.
user-invocable: true
disable-model-invocation: false
allowed-tools: []
---

# Robinhood Agentic Trading

Use this skill only as a safe control-plane guide for Robinhood Agentic Trading through Agent OS policy. It does not grant live trading authority.

## Safety Boundary

- Do not place orders.
- Do not cancel orders.
- Do not fetch private account values, balances, positions, order identifiers, or transaction identifiers.
- Do not ask the user for Robinhood passwords, MFA codes, OAuth tokens, session cookies, account numbers, or other private provider data.
- Do not use unofficial Robinhood APIs, scraping, browser automation, or commands that bypass Agent OS policy.
- Do not claim Robinhood partnership, broker-dealer status, RIA status, investment advice, or guaranteed returns.
- Options, margin, short selling, crypto, futures, and event contracts are roadmap-only unless a later Agent OS policy explicitly supports them.

## Required Policy Conditions

Before any live connector action can be discussed as eligible, all of these must already be true in Agent OS:

1. The owner has enabled the Robinhood trading connector policy.
2. A schema-only MCP probe has confirmed the official tool names and parameter shapes.
3. The finance policy allows the requested symbol and intent.
4. The request is long-equity only.
5. A review step has already been completed before order placement.
6. Owner approval has already been recorded for any live order placement or cancellation.
7. Single-order, daily-notional, and open-order caps are in force.
8. Redacted receipt policy is enabled.

## Official MCP Endpoint

Use only the official Robinhood Agentic Trading MCP endpoint when an Agent OS connector policy has already approved schema inspection or future connector use:

```text
https://agent.robinhood.com/mcp/trading
```

## Safe Workflow

For trading-related requests:

1. Classify the request as research, readiness, review, order placement, or cancellation.
2. If the request is research, route to a research-only artifact and mark candidate actions as non-executable.
3. If the request is review, verify connector enablement, symbol policy, long-equity intent, notional caps, and receipt policy.
4. If the request is placement or cancellation, require prior review and explicit owner approval before treating it as eligible.
5. If any condition is missing, stop and return the missing policy or approval requirement.

## Safe Response Pattern

Use language like:

```text
This can be prepared as an Agent OS trading review, but no live order can be placed until the owner-approved connector policy, review record, approval record, caps, and receipt policy are all present.
```

Never tell an agent to bypass Agent OS, call a provider directly, or execute a trade from text alone.
