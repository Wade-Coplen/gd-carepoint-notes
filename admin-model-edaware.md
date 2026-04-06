# Cleaner Admin Model for EDAware

This document proposes a cleaner administrative model for EDAware, focused on four high-friction areas:

- alerts
- templates
- call routing
- role permissions

The design goal is to reduce configuration sprawl, make site setup safer, and let hospitals adapt workflows without turning everyday administration into a fragile expert-only task.

## Core opinion

The current category is often over-configurable in the wrong places and under-structured in the right ones.

A cleaner admin model should:

- separate configuration domains clearly
- make relationships visible
- allow local variation without duplicating everything
- support role-based administration
- include simulation and auditability before changes go live

## Recommended admin architecture

Treat the admin console as four coordinated modules sitting on a shared policy layer.

### 1. Alert Administration

This module controls what kinds of events exist and what they trigger.

#### Main objects

##### `AlertType`

Examples:

- Trauma Alert
- STEMI Alert
- Stroke Alert
- Sepsis Alert
- OB Alert
- MCI Alert

Suggested fields:

- `id`
- `name`
- `status`
- `severity`
- `defaultPriority`
- `allowedInitiators`
- `requiredTemplateId`
- `routingPolicyId`
- `notificationPolicyId`
- `escalationPolicyId`

##### `AlertTriggerRule`

Defines when an alert can be launched or suggested.

Suggested fields:

- `id`
- `alertTypeId`
- `triggerSource`
- `conditions`
- `confirmationRequired`

##### `EscalationPolicy`

Defines what happens if an alert is not acknowledged or completed in time.

Suggested fields:

- `id`
- `alertTypeId`
- `steps`
- `timeouts`
- `fallbackTargets`

#### Cleaner design rules

- Alert types should be reusable system objects, not embedded inside forms or routing rules.
- Routing and notification should be linked to the alert, not redefined from scratch each time.
- Each alert should have a preview page showing template, recipients, timing, and fallback behavior in one place.

### 2. Template Administration

This module controls structured intake and workflow forms.

#### Main objects

##### `Template`

Examples:

- EMS Pre-Arrival Intake
- STEMI Intake
- Stroke Intake
- Trauma Intake
- Interfacility Transfer Intake

Suggested fields:

- `id`
- `name`
- `version`
- `status`
- `category`
- `appliesToAlertTypes`
- `sections`
- `fieldRules`

##### `TemplateField`

Suggested fields:

- `id`
- `templateId`
- `label`
- `type`
- `required`
- `defaultValue`
- `validationRule`
- `visibilityRule`

##### `TemplateVersion`

Supports safe updates without breaking live workflows.

Suggested fields:

- `id`
- `templateId`
- `versionNumber`
- `publishedBy`
- `publishedAt`
- `changeSummary`

#### Cleaner design rules

- Templates should be versioned explicitly.
- Draft, test, and published states should be distinct.
- Templates should inherit from shared base patterns where possible so sites do not duplicate entire forms for small local changes.
- Required fields should be controlled by policy rules, not hidden in freeform configuration.

### 3. Call Routing Administration

This module controls where calls, alerts, and related events go.

#### Main objects

##### `RoutingPolicy`

Defines how incoming calls or events are assigned.

Suggested fields:

- `id`
- `name`
- `channelType`
- `siteScope`
- `scheduleId`
- `defaultDestination`
- `fallbackDestination`
- `overflowBehavior`

##### `RoutingRule`

Defines conditional routing logic.

Suggested fields:

- `id`
- `routingPolicyId`
- `priority`
- `matchConditions`
- `destination`
- `afterHoursDestination`
- `failoverDestination`

##### `Destination`

Represents a team, role, person, queue, device, or remote endpoint.

Suggested fields:

- `id`
- `name`
- `destinationType`
- `contactMethod`
- `availabilityPolicy`

#### Cleaner design rules

- Routing rules should be readable in plain language.
- Every route should answer three questions: where does it go first, what happens after hours, and what happens if nobody answers.
- Routing should be testable with a simulator before publishing.
- Manual override should always be available to approved roles during live operations.

### 4. Role Permission Administration

This module controls who can view, configure, launch, edit, approve, and review.

#### Main objects

##### `Role`

Examples:

- ED Clerk
- Charge Nurse
- Physician
- EMS Coordinator
- QA Reviewer
- Site Admin
- System Admin

Suggested fields:

- `id`
- `name`
- `scope`
- `basePermissionSetId`

##### `Permission`

Suggested examples:

- `alert.launch`
- `alert.cancel`
- `alert.overrideRouting`
- `template.editDraft`
- `template.publish`
- `routing.edit`
- `routing.simulate`
- `recording.view`
- `recording.export`
- `admin.manageUsers`

##### `PermissionPolicy`

Defines combinations of permissions and environment scope.

Suggested fields:

- `id`
- `roleId`
- `permissions`
- `siteRestrictions`
- `auditLevel`

#### Cleaner design rules

- Use role-based defaults with limited local overrides.
- Separate operational permissions from configuration permissions.
- Publishing workflow changes should require higher privilege than using them.
- Sensitive actions such as exporting recordings or editing retention settings should require explicit elevated permission.

## Shared governance layer

These four modules should not be built as isolated admin pages. They should sit on top of shared governance services.

### Shared capabilities

- audit log for every configuration change
- draft versus published state
- approval workflow for high-risk changes
- test or simulation mode
- environment scoping by site, region, or enterprise
- rollback to prior version

## Recommended admin UI shape

Instead of one dense configuration page, use a task-oriented admin console:

### Navigation

- Alerts
- Templates
- Routing
- Roles and Permissions
- Sites
- Audit Log
- Simulations

### Per-page layout

Each admin page should include:

- summary list
- detail view
- dependency map
- change history
- test or preview action

## Example dependency model

An admin should be able to open a single alert type and see:

- which template it uses
- which routing policy it uses
- which teams receive notifications
- which roles can launch it
- how escalation behaves

That one-screen relationship view is one of the biggest usability upgrades over fragmented legacy administration.

## EDAware-specific recommendations

For EDAware, I would strongly recommend:

### Keep local site configuration, but constrain it

Hospitals need local variation. They do not need unlimited freedom to create contradictory workflows.

Use:

- enterprise defaults
- site overrides
- hard-locked safety rules

### Separate builders from operators

The person answering EMS traffic should not be editing routing logic during normal operation unless they have an explicit elevated role.

### Add change simulation before publish

Before a routing or alert policy goes live, the admin should be able to test:

- weekday daytime scenario
- overnight scenario
- no-answer scenario
- remote-access scenario

### Treat permissions as clinical-safety controls

Permissions are not just IT settings. In this type of platform, they affect who can trigger teams, view sensitive recordings, and alter operational behavior.

## Honest opinion

If this area is not modeled well, the product will feel powerful in demos and painful in production.

The winning move is not "more flexibility." The winning move is structured flexibility:

- reusable objects
- visible dependencies
- safe publishing
- constrained overrides
- strong auditability

That would be a real upgrade over the configuration complexity often associated with older hospital communication platforms.
