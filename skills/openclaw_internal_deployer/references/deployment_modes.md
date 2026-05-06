# Deployment Modes

Use this reference after reading `docs/deploy_manifest.md`. The manifest is authoritative; these rules define the supported interpretation and safety boundaries.

## `skill_sync`

Deploy a single OpenClaw Skill.

Source:

```text
openclaw/skill/
```

Target:

```text
~/.openclaw/workspace/skills/<skill-name>
```

Required checks:

- `openclaw/skill/SKILL.md` exists.
- `SKILL.md` frontmatter exists.
- Frontmatter contains `name`.
- Frontmatter contains `description`.
- Runtime target resolves under `~/.openclaw/workspace/skills/`.

Common allowed files:

- `SKILL.md`
- `scripts/`
- `resources/`
- `references/`

## `agent_workspace_sync`

Deploy a sub-agent workspace.

Source:

```text
openclaw/agent/
```

Target:

```text
~/.openclaw/workspace-<agent-name>
```

Required checks:

- `openclaw/agent/AGENTS.md`
- `openclaw/agent/IDENTITY.md`
- `openclaw/agent/SOUL.md`
- `openclaw/agent/TOOLS.md`
- Runtime target resolves under `~/.openclaw/`.
- Runtime target name starts with `workspace-`.

Recommended checks:

- `openclaw/agent/USER.md`
- `openclaw/agent/skills/`
- `openclaw/agent/resources/`

Common allowed files:

- `AGENTS.md`
- `SOUL.md`
- `IDENTITY.md`
- `USER.md`
- `TOOLS.md`
- `skills/`
- `resources/`

## `agent_skill_sync`

Deploy only internal Skills for a sub-agent without overwriting the whole workspace.

Typical source:

```text
openclaw/agent/skills/
```

Typical target:

```text
~/.openclaw/workspace-<agent-name>/skills/
```

Required checks:

- Source skills directory exists.
- Each deployed Skill has `SKILL.md`.
- Each deployed `SKILL.md` has `name` and `description`.
- Runtime target resolves under `~/.openclaw/workspace-<agent-name>/skills/`.

Use this mode when the manifest says only selected internal Skills should change.

## `documentation_only`

Report the deployment plan and do not copy runtime files.

Use for:

- Deployment plan review.
- Manual pre-deployment inspection.
- Project documentation updates.

Still read the manifest and audit report. Still report blockers and warnings.

## `custom_manual`

Stop and request manual instructions.

Use when:

- OpenClaw registration flow is unclear.
- Global configuration would need modification.
- An unverified OpenClaw CLI command would be required.
- The project structure does not match a supported mode.
