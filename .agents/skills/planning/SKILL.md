---
name: planning
description: This skill should be used when the user asks to "make a plan", "plan this out", "break this down", "design an approach", or mentions planning, architecture, or task decomposition before implementation.
triggers:
- plan
- planning
- break this down
- design approach
- task breakdown
---

# Planning

Use this skill when the task is large enough that jumping straight to code
would risk wasted work. Plan first, get agreement, then implement.

## When to plan

- The change touches more than one file, service, or component.
- Requirements are ambiguous or several approaches are plausible.
- The work spans multiple sessions or must be handed to another person.
- A wrong design choice would be expensive to undo.

For a single small edit, skip this skill and just make the change.

## Workflow

1. Explore the relevant code before proposing anything. Read the files,
   trace the call paths, and note the existing conventions.
2. State the goal in one or two sentences so it can be confirmed.
3. List the constraints: language and framework, existing patterns,
   compatibility requirements, and anything that must not change.
4. Propose two or three candidate approaches with trade-offs. Prefer the
   smallest approach that fully meets the goal.
5. Recommend one approach and say why the others were rejected.
6. Break the chosen approach into ordered, verifiable steps. Each step
   should name the file or component it touches and how it will be checked.
7. Record open questions and assumptions that need confirmation.
8. Stop and confirm before writing code, unless the user asked for
   implementation in the same request.

## Plan format

```
Goal
  One or two sentences.

Constraints
  - ...

Approaches considered
  1. ... (trade-offs)
  2. ... (trade-offs)

Recommended approach
  Which one and why.

Steps
  1. [file/component] change - verification
  2. ...

Open questions
  - ...
```

## Rules

- Keep the plan proportional to the task. A three-line fix does not need a
  three-page plan.
- Do not invent requirements. Mark assumptions explicitly.
- Do not start editing until the plan is confirmed or the user has asked for
  both planning and implementation.
