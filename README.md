# open-code-cloud-platform-settings

OpenHands Cloud platform settings, delivered as agent skills.

## Installed skills

Skills live in `.agents/skills/` and activate on their trigger words.

| Skill | Triggers | Purpose |
| - | - | - |
| planning | plan, planning, break this down | Plan before large changes |
| security-review | security, vulnerability, secrets, owasp | Review code for flaws and leaked secrets |
| code-coverage | coverage, untested code | Run tests under coverage and find gaps |
| incident-triage | incident, triage, logs, root cause | Investigate failures and report findings |

## Usage

Start a conversation on this repository and use a trigger word, for example
"plan this out", "review for security", "run coverage", or "triage this
incident". The matching skill loads automatically.

Skills can also be managed in the OpenHands Cloud UI under Customize >
Skills. Secrets belong in Settings > Secrets and must never be committed
here.

See `AGENTS.md` for conventions.
