---
name: incident-triage
description: This skill should be used when the user asks to "triage an incident", "debug production", "analyze logs", "find the root cause", "investigate an outage", or pastes a stack trace or error log.
triggers:
- incident
- triage
- production error
- analyze logs
- root cause
- outage
---

# Incident Triage

Investigate a production incident and produce a structured report with a
likely root cause and recommended fixes. Do not change code unless the user
asks; triage first.

## Workflow

1. Gather the evidence: logs, stack traces, error IDs, time window, affected
   services, and recent deploys or config changes.
2. Build a timeline. Identify the first error or warning and the sequence of
   events that followed.
3. Locate the failure in the codebase. Trace from the stack trace into our
   code, not framework internals. Name the exact file and line.
4. Form a hypothesis for the root cause and check it against the evidence.
   List what would confirm or rule it out.
5. Assess blast radius: who and what are affected, and whether it is ongoing.
6. Recommend fixes, from the immediate mitigation to the durable fix.
7. Note how to prevent recurrence: missing test, alert, or guard.

## Report format

```
Summary
  One paragraph: what broke, when, and the impact.

Timeline
  HH:MM first signal
  HH:MM ...

Root cause (hypothesis)
  File:line and the mechanism. Confidence: high/medium/low.
  Evidence for and against.

Blast radius
  Services, users, data affected. Ongoing or resolved.

Recommended fixes
  1. Immediate mitigation
  2. Durable fix
  3. Preventive change

Open questions
  - ...
```

## Rules

- Separate what the evidence shows from what is inferred. Label inferences.
- Do not guess a root cause without pointing to code or log evidence.
- If the incident is ongoing, state the mitigation first, before analysis.
- Keep secrets and personal data out of the report.
