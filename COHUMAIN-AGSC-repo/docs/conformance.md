# Conformance Tiers

A graduated, **cumulative** adoption path. An organisation declares the tier it conforms to; the evidence column in each control spec defines what proves it.

## Tier 1, Foundational  (8 controls)
The minimum bar for *any* production agent. Core safety + security that prevent the highest-severity, fastest-moving failures.

`SAF-01` | `SAF-02` | `SAF-03` | `ALN-01` | `ALN-02` | `SEC-02` | `SEC-03` | `SEC-04`

## Tier 2, Managed  (18 cumulative)
Adds governance, alignment and proactive security with defined evidence. Appropriate for material or customer-facing systems.

*All Tier 1, plus:* `SAF-04` | `SAF-05` | `ALN-05` | `GOV-01` | `GOV-02` | `GOV-05` | `SEC-01` | `SEC-05` | `SEC-06` | `SEC-07`

## Tier 3, Assured  (25 total)
The full catalog, continuous conformance, third-party attestation. EU AI Act high-risk readiness.

*All Tier 2, plus:* `ALN-03` | `ALN-04` | `GOV-03` | `GOV-04` | `GOV-06` | `GOV-07` | `GOV-08`

---

| Tier | Controls | Cumulative | Typical use |
|------|----------|------------|-------------|
| Foundational | 8 | 8 | Any production agent |
| Managed | +10 | 18 | Material / customer-facing |
| Assured | +7 | 25 | High-risk / regulated |

---

## Evidence grade (proposed)

*Proposed by an implementer (xChk, November 2026) as an RFC; not yet adopted by the maintainers.*

The standard says conformance is verifiable, not assertional. Today every evidence item is a document the
deployer produces about itself (minutes, dashboards, configuration exports, "approval records"), and nothing in
the control text distinguishes a record that was signed by the person who decided from a line the agent printed.
`ALN-02` and `SEC-02` (Tier 1) require approval records for high-impact actions, and `SAF-05` (Tier 2) requires
them for regulated outputs; a tamper-evident receipt and an unsigned log entry both satisfy the words.

The proposal is one attribute on each evidence item, an **evidence grade**, declared by the organisation beside
the tier:

| Grade | Meaning | Example |
|---|---|---|
| **E0 asserted** | a statement in a document | a policy that says a kill switch exists |
| **E1 logged** | a record written by the system, mutable by the system that wrote it | an application log line per action |
| **E2 signed by the actor** | a record the acting system signed at the time; tamper-evident after the fact | a hash-chained, signed action trace |
| **E3 signed by the accountable human, independently verifiable** | the person who answered signed the record, and a third party can check it without trusting the deployer or the vendor | a passkey-signed approval record with a public verification path |

Suggested floors, so that the grade changes what an assessor accepts rather than only labelling it:

A floor applies from the tier at which its control enters the catalog, and holds at every tier above it.

| Evidence item | Controls | Tier 1 | Tier 2 | Tier 3 |
|---|---|---|---|---|
| Approval records: a person's decision on a high-impact action (`ALN-02`, `SEC-02`) or on a regulated output before it enters a decision (`SAF-05`) | `ALN-02`, `SEC-02` (T1); `SAF-05` (T2) | **E3** | **E3** | E3 |
| Per-action traces | `SAF-01`, `SEC-04` | E2 | E2 | E2, with omission detectable |
| Emergency-stop activation log | `SAF-02` | E2 | E2 | E2 |
| Boundary-violation log | `ALN-01` | E1 | E2 | E2 |
| Everything else | | E0 | E0 | E1 |

Why E3 for the approval items from the tier each enters at: the human gate is the control the catalog's own
"risk it closes" text leans on hardest (an irreversible action taken before any person could review it; a
regulated decision taken on an unreviewed output), and it is the one whose evidence most often turns out, after
an incident, to be a record the agent could have written. `SAF-05`'s approvals concern outputs rather than
actions, which is why the row names both, so that an approval of an output does not fall under "everything else".

What this would change in the repository, if adopted: an `evidence_grade` field per evidence item in
`controls/controls.json` and the CSV, the two tables above in this file, and one sentence in each affected
control's Evidence list naming the floor. No control is added, removed or re-scoped.
