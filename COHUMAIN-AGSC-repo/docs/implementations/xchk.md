# Implementation note: xChk against AGSC v1.0.0

**Who:** xChk (https://xchk.io), a runtime authorization and accountability layer for AI agents: a gate in the
agent's execution path, a passkey ceremony on a named person's phone for the actions that need one, and a
sealed, anchored receipt per action that a third party can verify offline without the vendor or the deployer.

**What this is:** a self-assessment by the implementer, dated 6–7 November 2026, of one *component* against the
25 controls. AGSC is written for the organisation deploying an agent; a component meets some controls alone,
supplies the technical half of others, and has no business claiming the rest. Each row below says which.
It is not a conformance claim. The standard has no conformance program, and this note does not pretend to one.

The full assessment, with the evidence and benchmark behind every row, is public:
https://in.xchk.io/agsc-assessment.html

## Summary

| | MEETS | PARTIAL | N/A |
|---|---|---|---|
| Tier 1 Foundational (8) | 7 | 0 | 1 |
| Tier 2 adds (10) | 4 | 4 | 2 |
| Tier 3 adds (7) | 2 | 1 | 4 |
| **All 25** | **13** | **5** | **7** |

**MEETS** = the component alone produces the control's named evidence, and that evidence is machine-verifiable.
**PARTIAL** = the technical half is the component's; the organisational half (minutes, runbooks, reviews) is
the deployer's. **N/A** = a model-lifecycle or content control outside what the component does, by design.

## Per control

| Control | Tier | Verdict | Evidence, in one line |
|---|---|---|---|
| SAF-01 | T1 | MEETS | Per-action sealed trace with actor, action, target and the agent's stated rationale; seven standing deviation watches wired to the owner's phone; a generated monthly review pack with a sign-off block |
| SAF-02 | T1 | MEETS (application layer) | One-call emergency stop at plate, host, org or registry scope; every action refused before any grant is read; registry-signed stop statement verified on the host; measured 20/20 halted, 9 ms median, 221 ms p95 against the 5 s SLA |
| SAF-03 | T1 | N/A | Content safety on generative output is a different product |
| SAF-04 | T2 | N/A | Factual accuracy is the model layer's |
| SAF-05 | T2 | PARTIAL | Human gate before a regulated act, with a signed, offline-verifiable approval record; output bias and drift monitoring is the model layer's |
| ALN-01 | T1 | MEETS | Declarative per-agent policy, deny-by-default, enforced outside the model's context; "cannot be overridden by prompt content" is measured by a published bypass benchmark (0 silent passes) run before every release |
| ALN-02 | T1 | MEETS | Approval happens before the act, on the accountable person's phone, under a passkey |
| ALN-03 | T3 | MEETS (agentic surface) | The public receipt carries why it asked and who decided; a consumer-facing explanation is the deployer's |
| ALN-04 | T3 | PARTIAL | The sealed action trace and per-run trust record are the explanation artefact for agents |
| ALN-05 | T2 | MEETS (action half) | Every act attributed to the agent and the accountable human, signed and anchored; survives export |
| GOV-01 | T2 | PARTIAL | Untrusted runtime content screened and labelled at the tool boundary; training lineage is the deployer's |
| GOV-02 | T2 | MEETS | Signed, manifest-hashed gate releases; every slot reports its version; a change register per period |
| GOV-03 | T3 | N/A | Supplier contracts |
| GOV-04 | T3 | N/A | Training governance |
| GOV-05 | T2 | N/A | Evaluating the deployer's model |
| GOV-06 | T3 | N/A | Model drift |
| GOV-07 | T3 | MEETS (agentic artefacts) | One identity per agent, gate version per install, harness and model per run; "what was live" answerable per run and per period |
| GOV-08 | T3 | N/A | Carbon governance |
| SEC-01 | T2 | PARTIAL | One identity per agent and ceilinged cross-org acts; the interaction map and delegation protocol are open work |
| SEC-02 | T1 | MEETS | Unique agent identity; task-scoped runs that can only narrow; human-in-the-loop for high-impact acts; entitlement review generated from the ledger |
| SEC-03 | T1 | MEETS | The authorization decision is made outside the model's context, so injected text cannot widen it; screens measured on spikee (94 %, 0 false positives) with the misses named |
| SEC-04 | T1 | MEETS | One record per call; absence of telemetry is itself a finding; incident package generated from the ledger |
| SEC-05 | T2 | MEETS (own system) | STRIDE self-assessment and a benchmark spec as the threat-to-control matrix |
| SEC-06 | T2 | MEETS | Adversarial suite and security scan gate every deploy; external suites reproduced |
| SEC-07 | T2 | PARTIAL | The component holds no agent memory; approvals answer one action only; the agent's memory store is the harness's and the deployer's |

## What the assessment surfaced about the catalog

The core argument holds up in practice: for an agent, "what may it do" and "what can a compromised one be made
to do" are one problem, and the eight AI-native controls are the right eight to call new.

The one thing the implementer missed is an **evidence grade**. Every evidence item in v1.0.0 is a document the
deployer writes about itself; three Foundational-tier controls accept "approval records" without saying who
approved, how the record is bound to the act, or whether anyone outside the deployer can check it. The proposal
is in `docs/conformance.md` under "Evidence grade (proposed)".
