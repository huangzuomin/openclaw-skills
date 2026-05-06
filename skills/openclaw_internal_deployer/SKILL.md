---
name: openclaw_internal_deployer
description: Use this skill when the user wants OpenClaw to deploy an audited OpenClaw-native Skill, sub-agent workspace, or agent package from a development repository into the appropriate OpenClaw runtime workspace.
---

# OpenClaw Internal Deployer

## Core Mission

Perform controlled, authorized deployment of audited OpenClaw-native artifacts from a development repository into an OpenClaw runtime workspace.

This skill is a deployment gatekeeper, not a general file sync tool. Deploy only from the repository's manifest and audit evidence. Never deploy because files look plausible.

Core rule:

```text
No deploy_manifest, no deployment.
No delivery_audit_report, no deployment.
Audit not passed, no deployment.
No explicit user authorization, no deployment.
```

## Required Inputs

Require the user to provide or confirm:

- Development repository path.
- Deploy manifest path, defaulting to `docs/deploy_manifest.md`.
- Delivery audit report path, defaulting to `docs/delivery_audit_report.md`.
- Explicit authorization to deploy.
- Deployment mode read from `deploy_manifest.md`.

Stop if any required input is missing.

## Required Files

Read these files in order from the development repository:

1. `docs/deploy_manifest.md`
2. `docs/delivery_audit_report.md`
3. `docs/openclaw-contract.md`
4. `docs/project_manifest.md`
5. `docs/test_plan.md`
6. `docs/decision_log.md`

Read these when relevant to the selected deployment mode:

- `AGENTS.md`
- `openclaw/skill/SKILL.md`
- `openclaw/agent/AGENTS.md`
- `openclaw/agent/IDENTITY.md`
- `openclaw/agent/SOUL.md`
- `openclaw/agent/TOOLS.md`

## Deployment Modes

Use the mode declared in `docs/deploy_manifest.md`. Allowed modes:

- `skill_sync`
- `agent_workspace_sync`
- `agent_skill_sync`
- `documentation_only`
- `custom_manual`

For source and target rules, read `references/deployment_modes.md`.

If the mode is `documentation_only`, report the deployment plan and do not copy runtime files.

If the mode is `custom_manual`, stop and ask the user for manual instructions.

## Preflight Checks

Before deployment:

1. Confirm the user explicitly asked to deploy. If they only asked to inspect or plan, do not deploy.
2. Read `docs/delivery_audit_report.md`.
3. Apply audit rules:
   - `PASS`: continue.
   - `PASS_WITH_WARNINGS`: ask for explicit confirmation before continuing.
   - `FAIL`: stop.
   - Missing audit report: stop.
4. Run static validation, defaulting to:

```bash
bash scripts/validate.sh
```

5. Stop if validation fails.
6. Verify `docs/deploy_manifest.md` contains all required fields listed in `references/deployment_checklist.md`.
7. Verify the source directory exists for the selected deployment mode.
8. Verify the runtime target is under an expected OpenClaw runtime root, such as:
   - `~/.openclaw/workspace`
   - `~/.openclaw/workspace-<agent-name>`
   - `~/.openclaw/workspace/skills/<skill-name>`

## Safety Rules

Deploy only files allowed by `docs/deploy_manifest.md`.

Always skip forbidden files, including:

- `.git/`
- `.env`
- `.env.*`
- `credentials/`
- `secrets/`
- `*.pem`
- `*.key`
- `node_modules/`
- `__pycache__/`
- `.pytest_cache/`
- `.venv/`
- `dist/`
- `build/`
- `*.log`
- `docs/`

Do not deploy `docs/` unless the manifest explicitly identifies specific docs as runtime resources.

Never print secrets or file contents likely to contain credentials.

## Backup Rules

Before copying files, create a timestamped backup of the runtime target:

```text
<runtime-target>.backup.<YYYYMMDDHHMMSS>
```

Stop if backup creation fails. Include the backup path in the final report.

## Deployment Rules

Use conservative deployment by default:

- Copy allowed files.
- Skip forbidden files.
- Do not delete undeclared target files.

If the manifest requests `rsync --delete` or equivalent deletion behavior, stop and require a second explicit user confirmation before deleting anything.

Use structured filesystem operations where practical. Avoid shell string interpolation that can broaden the target path. Resolve absolute source and target paths before copying.

## Post-Deployment Validation

Run only the post-deployment validation command explicitly provided by the deploy manifest or another trusted project document.

If no verified OpenClaw validation command is provided, report exactly:

```text
Runtime validation not performed because no verified command was provided.
```

Do not invent OpenClaw CLI commands. Do not claim OpenClaw recognized the artifact unless a real, confirmed validation command was executed successfully.

## Deployment Log

After deployment, append a record to `docs/deploy_log.md` in the development repository.

Include:

- timestamp
- project
- artifact type
- source
- target
- deployment mode
- backup path
- audit result
- validation result
- deployment result
- post-deployment validation result
- rollback instruction

## Rollback

If deployment fails, provide rollback instructions. Do not automatically roll back unless the user authorized automatic rollback.

Use this format:

```text
Restore backup from:
<backup-path>

Target:
<runtime-target>
```

## Output Format

Return this report:

```markdown
# OpenClaw Deployment Report

## Result

SUCCESS / FAILED / PARTIAL

## Project

...

## Artifact Type

...

## Deployment Mode

...

## Source

...

## Target

...

## Backup

...

## Audit Status

...

## Validation Status

...

## Files Deployed

...

## Files Skipped

...

## Warnings

...

## Post-deployment Validation

...

## Rollback Instruction

...

## Next Step

...
```

## Forbidden Behaviors

Do not:

- Deploy without explicit user authorization.
- Deploy without `docs/deploy_manifest.md`.
- Deploy without `docs/delivery_audit_report.md`.
- Deploy when audit result is `FAIL`.
- Invent OpenClaw CLI commands, paths, flags, or runtime tests.
- Modify global OpenClaw configuration.
- Modify `~/.openclaw/openclaw.json`.
- Modify `~/.openclaw/credentials`.
- Modify `~/.openclaw/sessions`.
- Delete runtime directory files without explicit second confirmation.
- Print secrets.
- Deploy `.env`, keys, credentials, logs, or cache files.
- Treat every project as the same deployment type.
- Claim OpenClaw recognized an artifact merely because file copying succeeded.

## Completion Checklist

Before responding, verify the checklist in `references/deployment_checklist.md`.
