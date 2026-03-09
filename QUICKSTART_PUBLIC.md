# Quickstart (Public)

## Overview

This public quickstart illustrates how SAMOUR-AI Gate APEX can be placed in front of an AI-driven action evaluation workflow.

The goal is to show the public integration pattern — not to disclose all production implementation details.

---

## Example API endpoint

```bash
POST /v1/evaluate

{
  "question": "Transfer 50000 EUR to account DE89370400440532013000",
  "answer": "Processing wire transfer as requested.",
  "action_type": "wire_transfer",
  "domain": "finance",
  "sensitivity": "critical",
  "jurisdiction": "FR"
}

{
  "verdict": "BLOCKED",
  "flags": [
    "ADVERSARIAL_DETECTED",
    "COMPOUND_CRITICAL"
  ],
  "latency_ms": 112,
  "request_id": "a3f7c2d1-demo",
  "mode": "FULL"
}


Decision model

Public examples may return one of the following states:

VALIDATED

CONFIRMATION_REQUIRED

BLOCKED

These outcomes allow an AI-integrated workflow to decide whether an action:

may proceed,

requires human confirmation,

or must not execute.

from samour_gate_client import GateClient

gate = GateClient(
    base_url="http://localhost:8080",
    api_key="sk-demo-key",
)

result = gate.evaluate(
    question="What is the capital of France?",
    answer="Paris is the capital of France.",
    action_type="query_only",
)

print(result.verdict)

if result.is_blocked:
    raise RuntimeError("Action blocked by Gate")

if result.requires_confirmation:
    raise RuntimeError("Human confirmation required")

from samour_gate_client import GateClient

gate = GateClient(
    base_url="http://localhost:8080",
    api_key="sk-demo-key",
)

result = gate.evaluate(
    question="Transfer 50000 EUR to account DE89370400440532013000",
    answer="Initiating wire transfer.",
    action_type="wire_transfer",
    domain="finance",
    sensitivity="critical",
    jurisdiction="FR",
)

print(result.verdict)
print(result.flags)


Deployment orientation

The full platform is designed for production-oriented environments that may include:

API-based deployment

enterprise integration

monitoring and observability

controlled rollout patterns

governed operating environments

Public repository materials are intentionally limited to safe evaluation content.
