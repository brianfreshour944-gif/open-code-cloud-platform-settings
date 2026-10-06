---
name: security-review
description: This skill should be used when the user asks to "review for security", "scan for vulnerabilities", "check for secrets", "security audit", or mentions SQL injection, XSS, OWASP, or secure coding.
triggers:
- security
- vulnerability
- vulnerabilities
- secrets
- owasp
- security audit
---

# Security Review

Review the changed or named code for exploitable flaws and leaked secrets.
Report findings with evidence. Fix in place only when the user asked for
fixes, or when the finding is trivial and clearly in scope.

## Workflow

1. Determine scope: the files changed on this branch, or the paths the user
   named. Do not scan the whole repository unless asked.
2. Read each file in scope and trace where untrusted input enters and how it
   is used.
3. Check the categories below.
4. Report each finding with file, line, category, severity, and a concrete
   fix. Order by severity.
5. If asked to fix, make the smallest change that removes the flaw and add a
   test that exercises the malicious input.

## Categories to check

- Injection: SQL, command, template, and LDAP injection from string
  concatenation of user input.
- Cross-site scripting: unescaped user input rendered into HTML.
- Path traversal: user-controlled paths passed to file operations.
- Broken access control: missing authorization checks on sensitive actions.
- Hardcoded secrets: credentials, tokens, or private keys in source.
- Unsafe deserialization and unsafe use of eval or shell=True.
- Outbound requests to attacker-controlled hosts (SSRF).
- Verbose errors that leak stack traces or internal details.

## Secret scanning

Scan the diff for credentials before anything else. If a secret is found,
report it and recommend rotation. Do not print the secret value, and do not
move a secrets-bearing file to a more readable location.

## Optional tooling

If the repository already provides scanners, run them instead of guessing:

- Python: `bandit -r <path>`, `semgrep --config auto <path>`
- JavaScript: `npm audit`, `semgrep --config auto <path>`

Only install a scanner if the user agrees. Prefer tools already present in
the project.

## Report format

```
[SEVERITY] category - file:line
  What is wrong and how it can be exploited.
  Fix: the specific change.
```

## Rules

- Evidence over speculation. If a pattern is safe in context, do not flag it.
- Never expose secret values in the report.
- Address findings in-line when fixing; otherwise communicate them clearly.
