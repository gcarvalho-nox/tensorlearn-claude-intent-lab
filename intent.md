# Intent: Results-ready notification

Sources: approved PRD N-17 (`inputs/01-approved-prd.md`), discovery notes (`inputs/02-current-meeting.md`). The early request (`inputs/03-superseded-request.md`) is superseded by PRD N-17 and is used as history only; nothing in this intent is approved by it.

## Problem

- **I-1** The fictional clinic receives avoidable calls from patients checking whether their results are ready. (PRD, "Problem and outcome")

## Proposed outcome

- **I-2** Notify the patient when a result is ready for their review in the existing authenticated portal. (PRD)
- **I-3** "Ready" means a doctor has reviewed and released the result (see C-1). It does not mean the laboratory upload merely finished. (PRD constraints; discovery notes, product owner)
- **I-4** The notification says only that an update is available and directs the patient to the existing authenticated portal. (PRD)

### How success will be observed

- **S-1** Reduction in status-only results calls, counted separately from clinical questions and compared against a measured baseline. (PRD; discovery notes, support lead)
- **S-2** Delivery failures of notifications. (PRD)
- **S-3** No baseline or numeric target is approved yet; both will be agreed during discovery. This intent sets no target. (PRD)

## Affected users and systems

- **U-1** Patients: the only approved recipients of the notification. (PRD)
- **U-2** Doctors: their review and release of a result is the gate for any notification. (PRD)
- **U-3** Clinic support: receives the results-status calls; the support lead asks that status-only calls be counted separately from clinical questions. (discovery notes, support lead)
- **SYS-1** The existing authenticated patient portal and its existing result route, which engineering considers adequate. (PRD scope; discovery notes, engineering lead)
- **SYS-2** The notification delivery channel (still to be decided, see OPEN-1) and its operational/notification logs. (PRD; discovery notes, privacy owner)

## Out of scope

- **X-1** Portal redesign. (PRD scope)
- **X-2** A new or rebuilt patient dashboard: a separate project. (discovery notes, engineering lead)
- **X-3** Appointment scheduling. (PRD scope)
- **X-4** Clinical interpretation of results. (PRD scope)
- **X-5** Notifying third parties. The referring doctor is not approved either; that is held as an open question (OPEN-2), not part of this scope. (PRD; discovery notes, clinical owner)
- **X-6** Everything only in the superseded early request: sending results automatically on lab upload, putting the test result in a message, copying the referring doctor, rebuilding the dashboard and its call-reduction target. (superseded request status line)

## Constraints

- **C-1** A doctor must review and release the result before any notification is eligible; laboratory upload completion is a precondition but never enough on its own. (Review and release: PRD; discovery notes, product owner. Upload as a precondition: our reading, not stated as a gate in the sources.)
- **C-2** No diagnosis, test result, clinical measurement or treatment detail in the message, the notification logs or operational logs. (PRD; discovery notes, privacy owner)
- **C-3** Access to the result is authenticated in the existing portal. No result attachments and no public result link. (PRD)
- **C-4** No duplicate notifications for the same released result version. (PRD)
- **C-5** Delivery failures are handled without sending duplicate patient messages. (PRD)
- **C-6** Patient consent is still under privacy review; its outcome feeds the channel decision (OPEN-1). (discovery notes, privacy owner)

## Open questions and owners

- **OPEN-1** Channel (SMS, email or portal push). Owners: product owner and privacy owner, to decide after the consent and delivery review. (PRD; discovery notes, privacy owner)
- **OPEN-2** Notification to the referring doctor. Owners: clinical owner and privacy owner, to decide whether this recipient is authorized. Not approved by the PRD, and approval must not be inferred from the superseded request. (PRD; discovery notes, clinical owner)

## Decision record

```json
{
  "notifyWhen": ["lab-upload-complete", "doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
