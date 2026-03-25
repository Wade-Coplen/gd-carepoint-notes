# HIPAA and Architecture Notes

This is an early planning note, not legal advice.

## Assumptions

If the platform stores call recordings, patient identifiers, alert context, or related clinical data, treat that information as ePHI.

## Core design expectations

### Security controls

- encryption in transit
- encryption at rest
- least-privilege access
- role-based permissions
- centralized authentication
- audit logging for access and changes

### Data lifecycle

- defined retention rules
- documented deletion process
- legal hold and review process where applicable
- backup and recovery plan

### Operational controls

- vendor and hosting review
- business associate agreement readiness
- incident response plan
- monitoring and alerting for suspicious access

## Architecture direction

### Suggested platform shape

- web application for hospital users
- mobile access layer for approved users
- secure media ingest service for voice and attachments
- event-routing service for alerts and notifications
- audit and reporting subsystem
- encrypted object storage or database-backed archive for recordings and metadata

### Storage model

Keep the media object and metadata concerns separated:

- media objects in secure encrypted storage
- searchable metadata in an application database
- immutable audit trail for access and disposition events

### Deployment model

Potential models:

- cloud-hosted with HIPAA-capable vendors and signed BAAs
- hybrid deployment where sensitive interfaces remain local but recordings and app logic are centrally managed

## Regulatory caution

Avoid moving too quickly into features that may create additional medical-device regulatory exposure, such as automated clinical interpretation or treatment recommendation logic.
