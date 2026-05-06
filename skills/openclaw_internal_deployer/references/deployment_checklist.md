# Deployment Checklist

Use this checklist before and after every deployment attempt.

## Required Manifest Fields

`docs/deploy_manifest.md` must include:

- `Project`
- `Artifact Type`
- `Development Repository`
- `Source Package`
- `Runtime Target`
- `Deployment Mode`
- `Files Allowed to Deploy`
- `Files Never Deploy`
- `Backup Rule`
- `Deployment Strategy`
- `Post-deployment Validation`
- `Rollback`
- `Deployment Record`

Stop if any required field is missing or contradictory.

## Required Evidence

- Confirm `docs/deploy_manifest.md` exists.
- Confirm `docs/delivery_audit_report.md` exists.
- Confirm `docs/openclaw-contract.md` exists.
- Confirm `docs/project_manifest.md` exists.
- Read `docs/test_plan.md` and `docs/decision_log.md` when present.
- Extract audit status as `PASS`, `PASS_WITH_WARNINGS`, or `FAIL`.

Audit handling:

- `PASS`: continue.
- `PASS_WITH_WARNINGS`: continue only after explicit user confirmation.
- `FAIL`: stop.
- Missing or ambiguous status: stop.

## Static Validation

Default command:

```bash
bash scripts/validate.sh
```

Run the manifest-provided validation command if it differs and is clearly trusted by the project documents. Stop on failure.

## Source Checks

For `skill_sync`:

- Confirm `openclaw/skill/` exists.
- Confirm `openclaw/skill/SKILL.md` exists.
- Confirm Skill frontmatter has `name` and `description`.

For `agent_workspace_sync`:

- Confirm `openclaw/agent/` exists.
- Confirm `AGENTS.md`, `IDENTITY.md`, `SOUL.md`, and `TOOLS.md` exist.

For `agent_skill_sync`:

- Confirm the manifest identifies the source Skills.
- Confirm each deployed Skill has `SKILL.md`.
- Confirm each Skill frontmatter has `name` and `description`.

## Target Checks

- Resolve the target to an absolute path.
- Confirm the path is under an expected OpenClaw runtime root.
- Reject targets outside `~/.openclaw/workspace`, `~/.openclaw/workspace/skills/`, or `~/.openclaw/workspace-<agent-name>`.
- Do not modify `~/.openclaw/openclaw.json`, `~/.openclaw/credentials`, or `~/.openclaw/sessions`.

## File Filtering

Deploy only manifest-allowed files.

Always skip:

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
- `docs/`, unless specific docs are declared runtime resources

## Backup

- Create `<runtime-target>.backup.<YYYYMMDDHHMMSS>` before copying.
- Stop if backup fails.
- Record backup path.

## Delete Behavior

- Default to no deletion of extra target files.
- If the manifest requests delete sync, require a second explicit user confirmation.
- Record delete confirmation in the final report.

## Post-Deployment

- Run only verified post-deployment validation commands from trusted project documents.
- If no command is provided, report: `Runtime validation not performed because no verified command was provided.`
- Append deployment record to `docs/deploy_log.md`.
- Include rollback instruction in the final report.
