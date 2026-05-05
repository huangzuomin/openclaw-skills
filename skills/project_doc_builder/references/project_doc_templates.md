# Project Document Templates

Use these templates when generating OpenClaw project documents. Keep placeholders only when information is genuinely missing, and list those placeholders under `Open Questions`.

## Clarification Mode

~~~markdown
# Key Questions to Clarify First

1. ...
2. ...
3. ...

# Preliminary Judgment

Recommended artifact type: <OpenClaw Skill / OpenClaw sub-agent workspace / Both>.

Reason: ...
~~~

## Single Document Mode: docs/project_spec.md

~~~markdown
# Project Spec: <project_name>

## Goal

## Artifact Type

State one of:

- OpenClaw Skill
- OpenClaw sub-agent workspace
- Both
- Unknown, with reason

Include a short justification.

## Recommended Architecture

Describe the document, Skill, agent, or combined structure at a practical level. Do not add frameworks unless requested.

## Target User

## User Scenario

## Input

## Output

## Workflow

## Core Capabilities

### Capability: <name>

Description:

Acceptance Criteria:

- Given <context>, when <action>, then <expected result>.
- Given <edge case>, when <action>, then <safe behavior>.

## Non-goals

## Acceptance Criteria

## Risks and Mitigations

## Dependencies

## Assumptions

## Open Questions

## Implementation Hints for Codex

Recommended task sequence:

1. Update `openclaw/skill/SKILL.md` or `openclaw/agent/*`.
2. Add supporting references under `resources/` or `references/` if needed.
3. Update validation checks if needed.
4. Run `bash scripts/validate.sh`.
5. Report files changed and validation result.

Complexity:

- Low / Medium / High

Dependencies:

- ...

Suggested first task:

- ...

## Notes for Codex

- Read these files first: ...
- Edit these files: ...
- Do not edit these files: ...
- Code writing allowed: Yes / No
- Deployment allowed: Yes / No
- Validation commands: ...
~~~

## Full Document Set Mode

Output separate sections with exact filenames:

~~~markdown
# docs/project_spec.md

...

# docs/openclaw-contract.md

...

# docs/test_plan.md

...

# docs/decision_log.md

...
~~~

## docs/openclaw-contract.md

~~~markdown
# OpenClaw Contract: <project_name>

## Artifact Type

## Development Repository Boundary

Development happens in the project repository. Do not directly edit the OpenClaw runtime workspace.

## Runtime Boundary

## Source Paths

## Runtime Target Paths

Use placeholders if not confirmed.

## Allowed File Changes

## Forbidden File Changes

- Do not directly edit `~/.openclaw/`.
- Do not manually copy files into `~/.openclaw/`.

## Allowed Commands

```bash
bash scripts/validate.sh
git status
git diff
```

Only add other commands if confirmed by the user or present in the template.

## Forbidden Commands and Actions

- Do not invent OpenClaw CLI commands.
- Do not deploy unless explicitly requested.
- Do not claim validation passed unless the exact command was run.

## Validation Requirements

## Manual Runtime Test Command

To be confirmed.

## Open Questions
~~~

## docs/test_plan.md

~~~markdown
# Test Plan: <project_name>

## Static Validation

- Command: `bash scripts/validate.sh`
- Expected result: validation passes without unresolved template placeholders.

## Local Functional Validation

- Test:
- Steps:
- Expected result:

## OpenClaw Runtime Validation

- Manual runtime test command: To be confirmed.
- Expected result: To be confirmed.

## Manual Task Tests

### Test: <scenario>

- Given:
- When:
- Then:

## Regression Checklist

- Project documents are complete enough for another coding agent.
- Artifact type and runtime boundary remain clear.
- No invented OpenClaw commands are present.
- No direct edits to `~/.openclaw/` are required.
- Assumptions and open questions are separated.
~~~

## docs/decision_log.md

~~~markdown
# Decision Log

## <YYYY-MM-DD>

### Observation

The user wants to turn rough project material into OpenClaw-native development documents.

### Decision

This project is designed as <OpenClaw Skill / OpenClaw sub-agent workspace / Both>.

### Reason

...

### Impact

Future coding agents should start from `docs/project_spec.md` and `docs/openclaw-contract.md`, respect the runtime boundary, and run confirmed validation commands before completion.
~~~
