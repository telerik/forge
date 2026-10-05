# Progress Forge

**Turn AI-assisted development into a repeatable engineering process.**

Progress Forge is an agentic software development life cycle (SDLC) harness that orchestrates AI
coding agents, project context, tools, workflow rules, and human oversight. It provides a
structured, repeatable framework for guiding work, reviewing results, and maintaining traceability
across development, documentation, security, planning, and support workflows — while letting teams
customize the process to their needs.

Forge does not replace your coding agent. Your agent executes the work; Forge supplies the
surrounding structure and controls.

| | |
| --- | --- |
| Product page | https://www.telerik.com/forge |
| Documentation | https://www.telerik.com/forge/documentation |
| Free trial | https://www.telerik.com/try/forge |
| Releases | https://github.com/telerik/forge/releases |

This public repository distributes Progress Forge releases. The source code is maintained separately.

## How Forge Works

Forge connects a request to an agent through a sequence of controlled stages:

1. **Discovers project context** — the applicable project, toolchain, agent, and workflow
   configuration, plus work-item context such as an issue, pull request, or ticket.
2. **Builds the command surface** — utility capabilities combined with built-in and
   project-defined workflow targets.
3. **Composes the work request** — the selected operation with role instructions, task prompts,
   project metadata, relevant files, and configured model or agent choices.
4. **Invokes the selected agent** — streaming agent activity and managing sessions while work
   is in progress.
5. **Checks the result** — prerequisite checks, output validation, tests, builds, file checks,
   and retries determine whether a workflow proceeds, retries, pauses, or takes a failure path.
6. **Keeps people in control** — approval gates let a person review a plan, code review, or
   delivery decision before the next stage continues.
7. **Records the outcome** — artifacts, traces, state transitions, and execution metadata are
   preserved so work can be inspected, resumed, or audited later.

## Getting Started

Choose your onboarding experience:

| Interface | Best for |
| --- | --- |
| **Forge Desktop App** | Guided setup for repositories, agents, and issue trackers, with visual workflow monitoring and approvals |
| **`frg` CLI** | Direct control, terminal automation, scripting, CI/CD integration, and workflow recovery |

Both expose the same core Forge concepts and share one session and license key.

Follow the [getting started documentation](https://wwwuat.telerik.com/forge/documentation/introduction#getting-started-with-progress-forge).

You can also browse the documentation source under [`user-docs/src/`](user-docs/src/README.md), starting with the [Quick Start](user-docs/src/quick-start.md)

[GitHub Releases](https://github.com/telerik/forge/releases) contain the Forge binaries,
installers, and more. Installer
asset names are stable across releases, and `frg update` upgrades an existing installation.

## Licensing

Forge requires a valid Telerik license to run agent-backed workflow commands. 

Use of Progress Forge is governed by the
[Progress Forge License Agreement](https://www.telerik.com/purchase/license-agreement/forge) —
see [LICENSE.md](LICENSE.md). Third-party component notices are listed in [NOTICE.txt](NOTICE.txt).

## Support

- [Documentation](https://www.telerik.com/forge/documentation)
- [Progress Telerik Support](https://www.telerik.com/support)
- [Report an issue](https://github.com/telerik/forge/issues)

© Progress Software Corporation and/or its subsidiaries or affiliates. All Rights Reserved.
