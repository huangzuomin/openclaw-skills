# Quality Checklists

## Document Quality Checklist

Before finalizing, verify:

- The problem statement is concrete.
- The artifact type is justified.
- Inputs and outputs are explicit.
- The runtime boundary is explicit.
- Non-goals are explicit.
- Acceptance criteria are testable and use Given / When / Then.
- Assumptions are separated from confirmed facts.
- Risks, mitigations, dependencies, and open questions are separated.
- OpenClaw runtime paths are not guessed.
- OpenClaw CLI commands are not invented.
- The next Codex action is obvious.
- Another coding agent can continue from the document without reading the chat history.

## Full Document Set Checklist

When generating the full set, verify:

- `docs/project_spec.md` includes goal, artifact type, architecture, target user, scenario, input, output, workflow, capabilities, non-goals, acceptance criteria, risks, dependencies, assumptions, open questions, implementation hints, and notes for Codex.
- `docs/openclaw-contract.md` states development repository boundary, runtime boundary, source paths, target paths, allowed changes, forbidden changes, allowed commands, forbidden commands, validation requirements, and open questions.
- `docs/test_plan.md` includes static validation, local functional validation, OpenClaw runtime validation, manual task tests, and regression checklist.
- `docs/decision_log.md` records the positioning decision made during document generation.

## Safety Checklist

Reject or revise output that:

- Treats uncertain assumptions as facts.
- Turns the document into marketing copy.
- Adds product frameworks, packages, APIs, or deployment machinery not requested by the user.
- Claims tests or validation have passed without evidence.
- Instructs direct edits under `~/.openclaw/`.
- Includes invented OpenClaw CLI commands.
- Mixes development repository files and runtime workspace files without a clear boundary.

## Completion Report Checklist

When the user asked to write files, report:

- Files changed.
- Commands run.
- Validation result.
- Anything not validated.
