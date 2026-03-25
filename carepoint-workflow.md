# CAREpoint Workflow

This document summarizes the practical workflow of General Devices CAREpoint based on official product and training materials. Exact steps may vary by hospital because alerts, forms, and routing can be configured locally.

## Core workflow

1. EMS initiates contact with the emergency department through radio, phone, or integrated communication channels.
2. ED staff receive and answer the call in CAREpoint.
3. Staff gather patient details while the call is active.
4. CAREpoint supports intake forms, alerts, and incoming clinical data such as ECG-related information.
5. Notifications and escalations are sent to downstream teams when needed.
6. Incoming patients can be tracked before arrival with identifiers such as ETA, complaint, and bed-related information where configured.
7. The receiving team prepares for handoff and arrival.
8. Recordings, reports, and case information are available later for QA, review, and follow-up.

## Functional areas

### Incoming communication

- EMS radio and phone traffic enters through the CAREpoint workstation.
- Calls may be answered manually or by configured workflow behavior.
- Multiple communication resources can be managed or conferenced when needed.

### Intake and documentation

- CAREpoint can capture structured incoming patient information.
- Sites may use configurable intake forms for alert categories such as trauma, STEMI, stroke, sepsis, OB, or MCI.
- Some environments use CAREpoint as a communication intake layer rather than the full legal chart.

### Team activation

- Relevant teams may be alerted based on call content and workflow rules.
- Common downstream groups include trauma, cath lab, neuro, and other ED response teams.

### Remote access

- CAREpoint 3 materials describe mobile and remote access options for viewing or handling communication away from the fixed ED workstation.

### Review and reporting

- CAREpoint materials describe recording and later review of communications and related case data.
- This supports quality review, administrative review, and operational reporting.

## Questions to track

- Which CAREpoint version is in use locally
- Which alerts are active in the local configuration
- Whether the local site uses CAREpoint for full intake, alerting only, or ECG plus communications
- Which downstream teams receive automated notifications
- What QA reports are available to end users versus admins

## Sources to confirm against

- General Devices CAREpoint user and training documents
- General Devices CAREpoint 3 feature and requirements materials
- Local departmental workflow and policy documents
