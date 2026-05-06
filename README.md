# OpenClaw Skills

Shared OpenClaw skills for initializing and developing OpenClaw-native applications, skills, and sub-agents.

## Skills

- `initialize_openclaw_dev_env`: Initialize a VM-based development repository for an OpenClaw-native Skill, sub-agent, or app using the standard OpenClaw development template.
- `openclaw_internal_deployer`: Deploy audited OpenClaw-native Skills, sub-agent workspaces, or agent packages into approved runtime workspaces.
- `openclaw_delivery_auditor`: Audit an OpenClaw-native development repository before deployment and produce a PASS, PASS_WITH_WARNINGS, or FAIL delivery gate report.
- `project_doc_builder`: Turn rough ideas and notes into structured OpenClaw project development documents.

## Layout

```text
skills/
  <skill-name>/
    SKILL.md
```

Each skill is stored in its own folder so this repository can grow as more skills are published.
