# MCRS Core Data Specification

This document details the core data model for the Medication Change Request (MCR) object.

## `MedicationChangeRequest` Object

The central object representing a proposed medication change.

### Fields

*   `mcr_id` (string, required): Unique identifier for the MCR.
*   `patient_id` (string, required): Unique patient identifier.
*   `medication_name` (string, required): Name of the medication.
*   `rxnorm_code` (string, optional): RxNorm code for the medication (Recommended).
*   `atc_code` (string, optional): ATC code for the medication (Optional).
*   `current_dosage` (string, optional): Dosage before the change.
*   `proposed_dosage` (string, required): Proposed new dosage.
*   `instructions` (string, required): Rationale or instructions for the change.
*   `criticality_level` (string, required, enum: `critical`, `semi-critical`, `non-critical`): Risk level.
*   `state` (string, required, enum: `PENDING`, `APPROVED`, `REJECTED`, `CONFLICT`, `OVERRIDDEN`): Current MCR status.
*   `proposer` (object, required): Information about the user proposing the change.
    *   `user_id` (string, required)
    *   `role` (string, required, enum: `physician`, `nurse`, `pharmacist`, etc. - extensible)
*   `verifiers` (array of objects, optional): List of assigned verifiers and their responses.
    *   `user_id` (string, required)
    *   `role` (string, required)
    *   `status` (string, enum: `APPROVED`, `REJECTED`, `NEED_MORE_INFO`, `PENDING` - indicates assigned but not yet responded)
    *   `timestamp` (string, format: date-time)
    *   `notes` (string, optional): Optional comments from the verifier.
*   `timestamps` (object, required): Key timestamps.
    *   `created_at` (string, required, format: date-time)
    *   `updated_at` (string, required, format: date-time)
    *   `escalated_at` (string, optional, format: date-time)
    *   `resolved_at` (string, optional, format: date-time)
*   `audit_log` (array of objects, optional): History of actions on the MCR.
    *   `action` (string, required): Description of the action (e.g., "Created", "Verifier Added", "State Changed to APPROVED").
    *   `performed_by` (string, required): User ID of the actor.
    *   `timestamp` (string, required, format: date-time)
    *   `notes` (string, optional): Additional context.
*   `extensions` (object, optional): Placeholder for custom vendor or implementation-specific fields.

## Other Core Objects

*(Placeholder: Define `User`, `AuditLog`, and `Notification` structures if they are separate top-level objects, though the current PRD embeds much of this within the MCR object itself)*

## Schema Definitions

Machine-readable schemas are provided in the `/schemas` directory:
*   [JSON Schema](../../schemas/mcrs-schema.json)
*   [Protobuf Definition](../../schemas/mcrs.proto)
