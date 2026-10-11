---
name: observe
description: Decide the logs, metrics, traces, and alerts a change needs before it ships, so a future incident is diagnosable in minutes. Use when adding a feature or service, hardening for production, or asked what to instrument, log, or monitor.
---

Instrument the change while you still understand it, so that when it breaks at 3am the evidence is already there. `incident` assumes that evidence exists — this skill creates it. Design every signal backward from the question on-call will ask.

## Steps

1. **Ask the 3am question.** When this breaks in production, what would on-call need to *see* to find the cause in minutes? Every signal you add must answer some version of that; signals that answer nothing are noise with a storage bill.
2. **Pick the signal per layer.** Structured **logs** for the narrative (with a correlation/request id, never a secret or PII); **metrics** for rates, latencies, and error counts (the RED signals: Rate, Errors, Duration); **traces** for paths that cross service boundaries. Instrument what fails, not everything.
3. **Alert on symptoms, not causes.** Page on user-visible SLO breaches — error rate up, latency up, throughput down — not on every internal blip. A noisy alert gets muted, and a muted alert is no alert.
4. **Make every alert actionable.** Each one links to a runbook (hand to `document`) and names the owner and the threshold with the reason behind the number. An alert nobody knows how to act on wakes someone for nothing.
5. **Prove it fires.** Simulate the failure and confirm the signal actually appears and the alert actually triggers. Untested instrumentation is a guess that you'll discover is wrong during the incident.

## Completion

The change emits the logs, metrics, and traces on-call needs; alerts fire on user-visible symptoms and each links a runbook; no secret or PII is logged; and the signals were observed firing against a simulated failure — not assumed to work.
