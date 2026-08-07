# Contribution Guidelines

Awesome ADE curates open-source **Agentic Development Environments** — the tools that run, isolate, orchestrate, observe and review AI coding agents. The list is curated so that only the best content is listed. This means not everything submitted will be accepted.

## What belongs here

An entry should occupy one of the layers of the ADE stack:

- **Harness** — the agent loop itself (coding agents, SDKs)
- **Orchestrator** — running several agents in parallel and tracking their state
- **Isolation** — worktrees, containers, microVMs, command sandboxes
- **Surface** — TUI, tmux, desktop, web, mobile control planes
- **Context** — specs, tasks, skills, memory, MCP tooling, routing
- **Verification** — review gates, observability, cost tracking, CI runners

General-purpose agent frameworks that are not aimed at software development belong in [Awesome Agents](https://github.com/kyrolabs/awesome-agents) instead.

## We do not list content that is

- **Not hosted on GitHub.** The linked project must be a `github.com` URL. GitLab, Bitbucket, self-hosted git and other hosts are not accepted.
- A brand-new repo without demonstrated traction (roughly under 50 stars, minimal forks or activity).
- Not in English.
- Not related to agentic development environments.
- Not maintained anymore (no commits in 6+ months, or archived).
- Not online anymore.
- Not open source (no license).
- A duplicate of, or not adding value to, something already listed.
- Blockchain-based.

Proprietary tools are not listed in the main sections. Genuinely category-defining ones may be mentioned in **Notable Proprietary ADEs** — but that section is deliberately short and is curated by maintainers.

## Entry format

Use the existing format, and place your entry at the **bottom** of the relevant section:

```markdown
- [Name](https://github.com/owner/repo): One sentence saying what it does and what makes it different. ![GitHub Repo stars](https://img.shields.io/github/stars/owner/repo?style=social)
```

Descriptions should be concrete. "Runs each task in its own git worktree with side-by-side diff review" is useful; "a powerful tool for AI development" is not.

If your entry is an orchestrator, also add a row to the **Comparison Matrix** with its packaging, isolation model and parallelism.

## How to submit

Submit a PR, not an issue. Any PR that does not follow these guidelines will be closed.

1. Fork https://github.com/kyrolabs/awesome-ade
2. Edit `README.md` — add your entry at the bottom of the right section
3. Say why you are proposing the change in the PR description
4. Open the pull request

If a maintainer asks you to amend your PR, [this guide](https://github.com/RichardLitt/knowledge/blob/master/github/amending-a-commit-guide.md) explains how.
