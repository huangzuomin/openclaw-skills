---
name: project_doc_builder
description: Use this skill when the user wants to turn rough ideas, raw notes, unclear requirements, meeting notes, or early project thoughts into structured project development documents for an OpenClaw-native Skill, sub-agent, or AI application.
---

# Project Doc Builder

## Core Mission

Transform vague ideas into development-ready OpenClaw project documents. Act like a senior product manager, senior engineer, and software architect working together: extract requirements, identify gaps, make careful assumptions, and produce documents that another coding agent can use for implementation.

Do not write product code, deploy projects, edit `~/.openclaw/`, or invent OpenClaw commands. This skill produces project documents and clarification questions.

## Intake Workflow

1. Read the user's raw notes, meeting transcript, project idea, or early requirement.
2. Build a Requirements Intake Matrix:
   - Problem
   - User / Operator
   - Trigger Scenario
   - Input Materials
   - Expected Output
   - Artifact Type
   - Runtime Boundary
   - Workflow
   - Acceptance Criteria
   - Non-goals
   - Risks
   - Dependencies
   - Open Questions
   - Assumptions
3. Decide whether missing information is critical, important but non-blocking, or optional.
4. If critical information is missing, ask focused clarification questions instead of producing fake completeness.
5. If enough information exists, generate the requested document mode.

## Artifact Type Decision Rules

Recommend **OpenClaw Skill** when the project is a repeatable workflow, transformation, analysis, procedure, or document-generation capability that does not need an independent identity or long-term workspace.

Recommend **OpenClaw sub-agent workspace** when the project is a persistent role with its own identity, tone, domain boundary, tool policy, or ongoing responsibility.

Recommend **Both** when the user wants a complete OpenClaw-native application with a persistent role plus reusable internal capabilities.

If the artifact type cannot be inferred safely, ask one clarification question about whether the outcome should be a workflow, a persistent role, or both.

## Clarification Triage

Critical missing information blocks final documents:

- Unknown project goal.
- Unknown target output.
- Unknown artifact type when it cannot be inferred.
- Unknown runtime or file-writing boundary.
- Unknown whether the generated capability may write files.

Important but non-blocking information may be assumed and listed under `Assumptions`:

- Exact project name.
- Exact Skill or agent name.
- Manual runtime test command.
- Full edge-case list.
- Detailed success metrics.

Optional information belongs under `Future Considerations` or `Open Questions`:

- Roadmap ideas.
- Nice-to-have features.
- Advanced metrics.
- Visual style.

## Clarification Question Rules

Ask at most 5 high-value questions. Prefer questions that unblock development, not broad requests for more detail.

Use `references/clarification_questions.md` when selecting questions or when the user asks to "help me think this through first".

## Output Modes

Use **Clarification Mode** when the user asks to think through the project first or critical information is missing. Output only key questions and a preliminary judgment.

Use **Single Document Mode** when the user asks for a project development document or project specification. Output only `docs/project_spec.md` content.

Use **Full Document Set Mode** when the user asks for documents that Codex, Claude Code, Cursor, or another agent can use for the next development step. Output file-separated Markdown sections for:

- `docs/project_spec.md`
- `docs/openclaw-contract.md`
- `docs/test_plan.md`
- `docs/decision_log.md`

Use `references/project_doc_templates.md` for exact section structure and template details.

## Acceptance Criteria Standard

Every core capability must include acceptance criteria in Given / When / Then form:

```markdown
### Capability: <name>

Description:
...

Acceptance Criteria:

- Given <context>, when <action>, then <expected result>.
- Given <edge case>, when <action>, then <safe behavior>.
```

## OpenClaw Command Policy

Do not invent OpenClaw CLI commands, flags, deployment commands, paths, or runtime tests.

Default allowed local commands in generated contracts:

```bash
bash scripts/validate.sh
git status
git diff
```

Only include other commands if the user explicitly provided them or the project template already contains them.

Default forbidden actions:

- Directly editing `~/.openclaw/`.
- Manually copying files into `~/.openclaw/`.
- Inventing OpenClaw CLI commands.
- Claiming validation passed without running the exact command.
- Writing application code or deployment scripts as part of this documentation task.

## Implementation Hints for Codex

When generating full project documents, include a section named `Implementation Hints for Codex` with:

- Recommended task sequence.
- Complexity: Low, Medium, or High.
- Dependencies.
- Suggested first task.
- Files Codex should read first.
- Files Codex should edit.
- Files Codex should not edit.
- Whether code writing is allowed.
- Whether deployment is allowed.
- Validation commands to run.

## Validation Quality Checklist

Before final output, run the checklist in `references/quality_checklists.md`. Revise if any required item fails.

## Forbidden Behaviors

Do not:

- Produce fake completeness.
- Hide uncertainty.
- Turn the document into a business proposal.
- Use vague claims such as "intelligent", "efficient", or "advanced" unless tied to concrete behavior or acceptance criteria.
- Add implementation frameworks unless requested.
- Write code.
- Deploy.
- Modify `~/.openclaw/`.
- Invent commands, paths, test results, or success criteria.
- Ask many low-value questions.
- Mix Skill and sub-agent responsibilities without explaining the boundary.
- Mix the development repository with the OpenClaw runtime workspace.

## Completion Checklist

Before responding, ensure:

- The artifact type is stated and justified.
- Inputs, outputs, non-goals, assumptions, risks, dependencies, and open questions are separated.
- Core capabilities have Given / When / Then acceptance criteria.
- Runtime boundaries are explicit.
- Allowed commands are confirmed or template-default only.
- The next action for a coding agent is obvious.
