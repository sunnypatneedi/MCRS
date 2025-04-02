# MCRS Consensus Workflows

This document describes the standard workflows for proposing, verifying, and resolving Medication Change Requests (MCRs) using the MCRS specification.

## Standard Workflow (Non-Critical)

1.  **Proposal:** A `Proposer` creates an MCR object with `state` set to `PENDING`.
2.  **Verifier Assignment:** The system identifies and assigns required `Verifiers` based on institutional rules and medication type (may be pre-configured or dynamically assigned).
3.  **Notification:** Assigned `Verifiers` are notified (e.g., via a `CommunicationRequest`).
4.  **Verification:** Each `Verifier` reviews the MCR and updates their status in the `verifiers` array (`APPROVED`, `REJECTED`, `NEED_MORE_INFO`).
5.  **Consensus Check:** After each verification, the system checks if quorum is met.
    *   **Quorum Defined:** Configurable per institution (e.g., simple majority for non-critical).
6.  **Resolution:**
    *   **Approved:** If quorum for approval is met, MCR `state` changes to `APPROVED`. Notifications sent.
    *   **Rejected:** If quorum for rejection is met (or a mandatory verifier rejects), MCR `state` changes to `REJECTED`. Notifications sent.
    *   **Pending:** If quorum is not yet met, `state` remains `PENDING`.
7.  **Audit:** All actions and state changes are recorded in the `audit_log` and/or `Provenance` resources.

## Critical Medication Workflow

Similar to the standard workflow, but with stricter rules:

*   **Quorum:** Often requires unanimous approval from all mandatory verifiers (e.g., lead physician, specialist, pharmacist).
*   **Rejection:** Rejection by any single mandatory verifier may immediately move the MCR to `REJECTED` or trigger `CONFLICT` resolution.

## Conflict Detection & Resolution

Conflicts arise when:

*   Contradictory MCRs exist for the same medication/patient.
*   Verifier responses prevent reaching a clear Approved/Rejected consensus based on quorum rules.

**Workflow:**

1.  **Detection:** System identifies a conflict condition.
2.  **State Change:** MCR `state` is set to `CONFLICT`.
3.  **Notification:** Relevant parties (proposer, verifiers, arbiter) are notified.
4.  **Information Gathering:** System may prompt verifiers for more information or clarification.
5.  **Escalation:** If conflict persists, MCR is escalated (e.g., to a Medication Manager/Arbiter).
    *   `timestamps.escalated_at` is set.
6.  **Arbitration:** The designated `Arbiter` reviews the MCR, context, and verifier feedback.
7.  **Final Decision:** Arbiter makes a final decision, setting the state to `APPROVED` or `REJECTED` (potentially with an override flag).
8.  **Resolution:** `timestamps.resolved_at` is set. Final state broadcast and logged.

## Emergency Override

1.  **Trigger:** Authorized user initiates an override action.
2.  **State Change:** MCR may be created with `state` = `OVERRIDDEN` or an existing MCR state is changed.
3.  **Immediate Action:** The change is implemented, bypassing standard verification.
4.  **Notification:** All relevant parties notified immediately.
5.  **Audit:** Override action is logged with high priority.
6.  **Post-Event Review:** The override is typically reviewed retrospectively.

## Timeouts

*   Configurable time limits can be set for verifier responses.
*   If a timeout occurs, the system may:
    *   Escalate the MCR.
    *   Apply a default action (e.g., reject for critical, approve for non-critical - policy dependent).
    *   Mark the verifier status as `TIMED_OUT`.

*(Note: Visual diagrams corresponding to these workflows should be placed in `../diagrams/`)*
