# manager

Let the main agent manage the project while subagents carry out the work.

manager is a Codex and Agent Skill. When enabled, the main agent clarifies the goal, assesses difficulty and risk, chooses available models and reasoning effort, delegates and coordinates work, reports progress, and verifies the results. Subagents handle planning, code, configuration, testing, debugging, integration, and technical review.

## Core principles

- **Manager role.** The main agent delegates project code, implementation plans, and other deliverables, including small tasks.
- **Task-based routing.** Choose a lightweight, cost-efficient, or top-tier model based on the task and the options the host actually offers. Choose reasoning effort separately and respect the user's preferences and the host's limits.
- **Staffing by need.** One assignee is enough when one can do the work. Add assignees when the work benefits from them.
- **Responsibility through delivery.** Report significant results, blockers, and changes as they arise. Verify the final integrated result with evidence from actual checks.
- **Existing permissions.** Follow authorization, environment restrictions, and concurrency limits. Report the blocker if no assignee is available.

See [manager/SKILL.md](manager/SKILL.md) for the full instructions.

## Installation

### Ask Codex to install it

Give Codex the GitHub URL for this repository and ask it to install the skill.

> Use $skill-installer to install the manager skill from the manager directory in this repository.

Codex can use `$skill-installer` to install skills from other repositories. The installer determines the installation location. [Official installation instructions](https://learn.chatgpt.com/docs/build-skills#install-curated-skills-for-local-use)

### Install locally by hand

Download or clone the repository, then enter its root directory. These macOS and Linux commands preserve any existing installation.

```sh
mkdir -p "$HOME/.agents/skills"
if [ -e "$HOME/.agents/skills/manager" ] || [ -L "$HOME/.agents/skills/manager" ]; then
  printf '%s\n' 'manager already exists. Inspect and back up the existing version first.'
else
  cp -R manager "$HOME/.agents/skills/manager"
fi
```

To use the skill in a single project, put the `manager` directory in that project's `.agents/skills/manager/`. Keep `SKILL.md`, `agents/`, and `assets/` in their relative locations. Codex detects changes automatically. Restart Codex if the skill does not appear. [Official local skill directory instructions](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)

## Usage

In the Codex CLI or IDE, find the skill with `/skills` or use `$manager` in your prompt. In ChatGPT, use `@` to select the installed skill. [Official invocation instructions](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills)

> Use $manager for this task. Assess its complexity and risk, choose suitable models and reasoning effort from the available options, then delegate planning, implementation, testing, and review. Coordinate the work, report progress, and verify the results. Leave project code and plans to the assignees.

Use the skill for projects where the user explicitly requests manager-led collaboration. Ordinary Q&A and general coding requests keep their normal workflow.

## Requirements and boundaries

- The host must provide working subagent or collaboration tools and an execution environment.
- Model availability, reasoning settings, and concurrency depend on the host's actual capabilities.
- The skill guides agent behavior. Enforcement depends on the model, tools, and higher-priority rules.

## Files

- `manager/SKILL.md` contains the rules for manager-led collaboration.
- `manager/agents/openai.yaml` contains display metadata and invocation policy.
- `manager/assets/icon.svg` is the interface icon.
