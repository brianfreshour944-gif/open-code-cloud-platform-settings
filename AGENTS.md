# AGENTS.md

This repository holds OpenHands Cloud platform settings, delivered as agent
skills. Keep changes small and reviewable.

## How this repo is set up

OpenHands capabilities are configured as skills in `.agents/skills/`. Skills
load on demand when their trigger words appear, so they do not consume
context until they are needed.

| Skill | Triggers | Purpose |
| - | - | - |
| planning | plan, planning, break this down | Plan before large changes |
| security-review | security, vulnerability, secrets, owasp | Review code for flaws and leaked secrets |
| code-coverage | coverage, untested code | Run tests under coverage and find gaps |
| incident-triage | incident, triage, logs, root cause | Investigate failures and report findings |

## Cloud setup notes

- In OpenHands Cloud there is no `config.yaml` with `agents:` or `features:`
  toggles. Capabilities come from skills, secrets, MCP servers, and
  automations.
- Secrets live in Settings > Secrets and are exported as environment
  variables into the agent runtime. Never commit secrets here.
- MCP servers are configured under Customize > MCP Servers.
- Skills can also be managed in the Cloud UI under Customize > Skills.

## Conventions

- Add new skills under `.agents/skills/<name>/SKILL.md` with YAML frontmatter
  containing `name`, `description`, and `triggers`.
- Write descriptions in the third person and quote the phrases a user would
  say. This drives trigger matching.
- Never commit secrets. Never print secret values.
- Keep AGENTS.md concise; move detailed instructions into skills.
