---
name: incident
description: Respond to a production incident — stabilize first, diagnose second, prevent recurrence third. Use when something is down, degraded, or erroring in production, or you're asked to handle an outage, incident, or on-call page.
---

In an incident the order is fixed: **stop the bleeding, preserve the evidence, then find the cause.** Diagnosing before mitigating keeps users in pain while you think — resist it.

## Steps

1. **Stabilize before you understand.** Cut user impact first with the fastest safe lever: roll back the last deploy, flip the feature flag off, scale out, fail over, shed load. The clean root-cause fix comes later; right now, mitigation wins over understanding.
2. **Preserve the evidence.** Before logs, metrics, and traces rotate out, capture them with timestamps — including the state you're about to change by mitigating. You cannot diagnose from evidence that's already gone.
3. **Communicate.** State the user impact, what you're doing now, and when the next update comes. Keep it current. A silent incident is a second incident.
4. **Diagnose once stable.** Now hand the preserved evidence to the `debug` loop: reproduce, isolate to a named mechanism, confirm. The pressure is off, so do it properly rather than guessing under fire.
5. **Prevent recurrence.** Write a blameless postmortem: timeline, the cause, *why it wasn't caught*, and the concrete guardrail that stops a repeat — a test, an alert, a limit, a rollback automation. An incident without a guardrail added is an incident you'll have again.

## Completion

User impact is mitigated; evidence is preserved; the cause is found via the debug loop; a specific guardrail is added; a blameless postmortem records the timeline and the gap that let it through.
