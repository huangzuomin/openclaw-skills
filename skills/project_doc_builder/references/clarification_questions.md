# Clarification Questions

Ask at most 5 questions. Choose the smallest set needed to unblock document generation.

## Goal and Success

- What concrete problem should this project solve, and what outcome would make it successful?
- What should a user be able to do after this Skill or agent exists that they cannot do reliably now?
- What are the must-pass acceptance criteria for the first usable version?

## Artifact Type

- Should this be implemented as a repeatable Skill workflow, a sub-agent with its own identity and workspace, or both?
- Does this capability need long-term responsibility, a role identity, or coordination across multiple Skills?
- Is the output mainly a document/transformation/procedure, or an ongoing operational role?

## Input, Output, and Boundary

- What exact input materials will the user provide: rough notes, files, meeting transcripts, existing code, or something else?
- What exact output should be produced: Markdown text, files under `docs/`, a Skill folder, an agent workspace, or another artifact?
- May the implementation write files automatically, or should it only return copy-ready Markdown?
- What should this project explicitly not touch or change?

## Runtime and Deployment

- What is the intended development repository path, and what is only a runtime deployment target?
- If this is a Skill, what should the `skill_name` be in `snake_case`?
- If this is an agent, what should the `agent-name` be in `kebab-case`?
- Has the user confirmed any deployment or runtime validation command?

## Testing and Handoff

- What local validation command is confirmed by the template or user?
- What manual runtime test should prove the Skill or agent works in OpenClaw?
- Which files should the next coding agent read first before implementing?

## Good Question Pattern

Good:

```text
Should this be implemented as a Skill that performs one repeatable workflow, or as a sub-agent with its own identity, tools, and long-term workspace?
```

Weak:

```text
Can you provide more details?
```
