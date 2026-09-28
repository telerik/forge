---
title: Effort Levels
meta_title: Configure Progress Forge Model Effort Levels
description: Set reasoning effort per agent, target, or operation and understand which coding agents support it.
slug: effort-levels
---

# Effort Levels

## What an Effort Level Does

An effort level sets a model's reasoning or thinking depth. Higher effort trades latency and token cost for deeper reasoning. Effort levels are only meaningful for models that support variable reasoning depth; other models ignore the setting or the agent CLI reports it as unsupported.

## Agent Support

Progress Forge passes the configured effort level to the agent's CLI only where the agent exposes a corresponding flag:

| Agent | Supported | Mechanism | Documented values |
|---|---|---|---|
| `github_copilot` | Yes | `--reasoning-effort` CLI flag | `none`, `minimal`, `low`, `medium`, `high`, `xhigh`, `max` |
| `claude_code` | Yes | `--effort` CLI flag | `low`, `medium`, `high`, `xhigh`, `max`, `ultracode` |
| `opencode` | Yes | `--variant` CLI flag (verified with OpenCode 1.18.11; provider-specific reasoning effort) | provider-specific, e.g. `minimal`, `high`, `max` |
| `gemini` | No | Set `thinkingConfig` in Gemini CLI's own `settings.json` | — |

## Configure an Effort Level

Set an agent-wide default that applies to all targets and operations:

```toml
[agent.github_copilot]
effort = "medium"
```

Override the default for a specific target:

```toml
[agent.github_copilot.targets]
issue = { model = "claude-sonnet-5", effort = "high" }
```

Override the default (and any target override) for a specific operation:

```toml
[agent.github_copilot.operations]
"issue.plan" = { model = "claude-opus-5", effort = "xhigh" }
```

## Precedence

Progress Forge resolves effort levels with:

```
operation override > target override > agent default > unset
```

An unset effort level means no flag is passed and the model uses its own default reasoning behavior.

## Progress Forge Does Not Validate the Value

Progress Forge passes the configured value through to the agent CLI verbatim. It does not check the value against the agent's documented list before running the command. The values in the [Agent Support](#agent-support) table are agent-published and may change at any time.

`low`, `medium`, `high`, and `max` are common examples across the three supported agents, not a guaranteed portable subset — `opencode`'s `--variant` values are provider-specific (see the [Agent Support](#agent-support) table), so a value accepted by one provider may be rejected by another. Confirm accepted values for your configured provider before sharing a single `agents.toml` across agents.

A mistyped or model/provider-unsupported value produces an error from the agent's own CLI, not from Progress Forge. Claude Code's `ultracode` value additionally requires Claude Code v2.1.203 or later.

## Agent CLI Versions

Progress Forge does not check the installed agent CLI's version. If the installed agent predates its effort flag, the agent reports an unknown-option error. Update the agent CLI (for example `claude update`) to resolve it.

OpenCode support reflects its current CLI contract: OpenCode 1.18.11 exposes `--variant` on `opencode run`. This supersedes the earlier config-file-only behavior assumed when this feature was specified. Progress Forge passes the value through that flag and still never reads or writes OpenCode's native configuration.

## Unsupported Agents

Configuring an effort level for `gemini` prints a non-fatal warning, and the command runs normally with the setting ignored. Progress Forge never reads or writes an agent's own configuration files. Users who want equivalent behavior for Gemini CLI configure `thinkingConfig` directly in Gemini CLI's own `settings.json`.

## Effort Levels and Custom Agents

An effort level and a custom agent can be configured together. Progress Forge applies no precedence between them — it passes both to the agent CLI unchanged, and the invoked agent (or custom agent) decides how to reconcile them.

## Related Information

- [Model Selection](./model-selection.md)
- [Prompt Formats](./prompt-formats.md)
- [Custom Agent Configurations](./custom-agent-configurations.md)
- [Troubleshooting](./troubleshooting.md)
