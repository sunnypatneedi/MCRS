# MCRS FHIR Mappings

This document outlines how the MCRS data model concepts map to standard HL7 FHIR resources. The goal is to leverage existing FHIR structures while extending them where necessary to accommodate MCRS-specific details.

## Core Mapping Strategy

We will define FHIR Profiles based on standard resources, adding extensions for MCRS-specific fields.

*   **Extension Prefix:** MCRS-specific extensions will use a defined URL prefix (e.g., `http://mcrs-spec.org/fhir/StructureDefinition/`).

## Resource Mappings

1.  **`MedicationChangeRequest` (MCR) -> `MedicationRequest`**
    *   **Base:** The proposed change itself often maps to a `MedicationRequest` resource.
    *   **Status Mapping:** `MedicationRequest.status` (active, on-hold, cancelled, completed, entered-in-error, draft, unknown) needs careful mapping to MCRS states (`PENDING`, `APPROVED`, `REJECTED`, etc.). An `x-mcrs-state` extension might be required for direct mapping.
    *   **Dosage:** `MedicationRequest.dosageInstruction` maps to `proposed_dosage` and `instructions`.
    *   **Medication:** `MedicationRequest.medicationReference` or `medicationCodeableConcept` maps to `medication_name`, `rxnorm_code`, `atc_code`.
    *   **Patient:** `MedicationRequest.subject` maps to `patient_id`.
    *   **Requester:** `MedicationRequest.requester` maps to `proposer.user_id`.
    *   **Extensions:**
        *   `x-mcrs-id`: To store `mcr_id`.
        *   `x-mcrs-criticality`: To store `criticality_level`.
        *   `x-mcrs-current-dosage`: To store `current_dosage`.
        *   `x-mcrs-state`: Direct mapping of MCRS state enum.

2.  **MCR Workflow & History -> `Provenance`**
    *   **Base:** Each significant event in the MCR lifecycle (creation, verification, state change, resolution) can be recorded as a `Provenance` resource linked to the `MedicationRequest` (or a dedicated MCR representation).
    *   **Target:** `Provenance.target` points to the relevant MCR/MedicationRequest.
    *   **Agent:** `Provenance.agent` represents the user performing the action (`proposer`, `verifier`, `arbiter`).
        *   `agent.who`: Maps to `user_id`.
        *   `agent.type`: Can represent the MCRS role (Proposer, Verifier).
        *   `agent.onBehalfOf`: If applicable.
    *   **Activity:** `Provenance.activity` can describe the action (e.g., "Propose", "Verify-Approve", "Verify-Reject", "Escalate", "Override").
    *   **Timestamp:** `Provenance.recorded` maps to event timestamps.
    *   **Extensions:**
        *   `x-mcrs-verifier-status`: If recording a verification event, stores the status (`APPROVED`, `REJECTED`).
        *   `x-mcrs-verifier-notes`: Stores verifier notes.

3.  **Notifications -> `CommunicationRequest` / `Communication`**
    *   **Base:** `CommunicationRequest` can be used to trigger notifications to verifiers or other stakeholders.
    *   **Status:** Tracks the status of the notification request.
    *   **Recipient:** `CommunicationRequest.recipient` points to the intended user/role.
    *   **Payload:** `CommunicationRequest.payload.contentString` or `contentReference` can link to or contain details about the MCR requiring attention.
    *   **BasedOn:** Can link back to the originating MCR/MedicationRequest or Task.
    *   **`Communication`:** Can represent the actual notification sent/received event.

4.  **Verification Tasks -> `Task`**
    *   **Base:** A `Task` resource can represent the work item assigned to a verifier.
    *   **Status:** `Task.status` (draft, requested, received, accepted, rejected, ready, cancelled, in-progress, on-hold, failed, completed, entered-in-error) maps to the verification progress.
    *   **Focus:** `Task.focus` points to the MCR/MedicationRequest being verified.
    *   **For:** `Task.for` points to the `patient_id`.
    *   **Owner:** `Task.owner` maps to the assigned `verifier.user_id`.
    *   **Input/Output:** Can potentially carry verification details or results.

## FHIR Profiles

Formal FHIR Profiles (StructureDefinitions) need to be created for:

*   `MCRSMedicationRequest`
*   `MCRSProvenance`
*   `MCRSCommunicationRequest`
*   `MCRSTask`

These profiles will define the required extensions and potentially constrain value sets (e.g., for `x-mcrs-state`).

*(Note: This is a preliminary mapping. Detailed profiling work is required based on implementation needs and FHIR best practices.)*
