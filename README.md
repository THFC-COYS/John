# Garrison

An MVP demo of an **agent control plane** for data center security — governing
AI agents (ops copilots, autoscalers, building-management controllers,
remediation bots) that hold privileged access to infrastructure, alongside
traditional outside-threat monitoring.

Built for a client pitch: the core idea is that AI agents inside a data
center are a new privileged-access population with none of the identity,
policy enforcement, or audit controls built for human operators.

## What's in this demo

Single-file, static, front-end-only simulation (`index.html`) — no backend,
no build step, just open it in a browser. It demonstrates:

- **Agent registry** — scoped, short-lived credentials per agent instead of
  shared service accounts.
- **Live activity feed** — every simulated agent action policy-checked with
  an Allowed / Held / Blocked verdict.
- **Rogue agent simulation** — a live "kill switch" demo: a building-management
  agent attempts an out-of-scope action, gets flagged, held, and
  auto-quarantined, with a real measured time-to-quarantine.
- **Two environment tabs** — Data Center (physical + cyber, the BMS/cooling
  scenario above) and Corporate IT (an accounts-payable agent attempting an
  unverified wire transfer above its authorization limit). Each tab has its
  own agent registry, activity feed, approvals, and audit ledger, and keeps
  its own state when you switch away and back.
- **Pending approvals** — human-in-the-loop dual control for high-risk actions
  (bulk credential revocation, data exports).
- **Sealed audit ledger** — an immutable-looking record of consequential
  actions, for the compliance story.

## Running it

Open `index.html` directly in a browser. No dependencies, no server required.

## Status

This is a sales/demo MVP, not production code. Turning this into a real
product means:

- A real policy engine sitting in front of agent tool calls (not simulated).
- Actual short-lived credential issuance for agents (e.g. workload identity
  federation, SPIFFE/SPIRE, or a cloud IAM equivalent scoped per task).
- Real telemetry ingestion instead of the seeded/mocked activity feed.
- An actual immutable audit store (append-only log / ledger) behind the
  "sealed ledger" UI.
