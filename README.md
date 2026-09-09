# 🛠️ Awesome ADE [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> A curated list of open-source **Agentic Development Environments** — the tools that make AI agents first-class citizens of your development workflow.

An **ADE** is the evolution of the IDE. An IDE assumes a human types and the machine completes. An ADE assumes an **agent** plans, edits files, runs terminal commands, manages git branches and fixes failing tests — while the human steers, reviews and merges.

That inversion changes which questions matter. Instead of "how do I edit text faster", an ADE is designed around:

- **How many agents run at once?** One session, or a dozen in parallel?
- **Where do they run?** Local worktree, tmux pane, container, VM, or the cloud?
- **How are they isolated?** Can agent A break what agent B is building?
- **How do I review?** Diffs, PRs, CI checks, human-in-the-loop gates.
- **How do I steer from anywhere?** Terminal, desktop app, browser, phone.

This list is organised the way you actually pick these tools: **by packaging** (TUI, tmux, desktop, web, mobile), then by the layer of the stack they occupy. Every entry is open source, actively maintained and hosted on GitHub. See [CONTRIBUTING.md](CONTRIBUTING.md).

Maintained by [KyroLabs](https://github.com/kyrolabs). See also: [Awesome Agents](https://github.com/kyrolabs/awesome-agents) · [Awesome LangChain](https://github.com/kyrolabs/awesome-langchain).

---

## Contents

- [Anatomy of an ADE](#anatomy-of-an-ade)
- [Orchestrators — Terminal & TUI](#orchestrators--terminal--tui)
- [Orchestrators — tmux-native](#orchestrators--tmux-native)
- [Orchestrators — Desktop](#orchestrators--desktop)
- [Orchestrators — Web & Self-hosted](#orchestrators--web--self-hosted)
- [Remote & Mobile Control](#remote--mobile-control)
- [Coding Agents (the engines)](#coding-agents-the-engines)
- [Harnesses & Agent SDKs](#harnesses--agent-sdks)
- [Editor-native Agents](#editor-native-agents)
- [Autonomous & CI Runners](#autonomous--ci-runners)
- [Isolation & Sandboxing](#isolation--sandboxing)
- [Spec, Planning & Task Layers](#spec-planning--task-layers)
- [Context, Skills & Routing](#context-skills--routing)
- [Observability & Cost](#observability--cost)
- [Review & Quality Gates](#review--quality-gates)
- [Protocols & Standards](#protocols--standards)
- [Browser & Computer-use Runtimes](#browser--computer-use-runtimes)
- [Comparison Matrix](#comparison-matrix)
- [Notable Proprietary ADEs](#notable-proprietary-ades)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

---

## Anatomy of an ADE

Most tools in this list sit on exactly one of five layers. Knowing which layer you are missing is usually the fastest way to pick your next tool.

| Layer | What it does | Typical examples |
| --- | --- | --- |
| **Harness** | The agent loop itself: model calls, tool use, permissions | OpenCode, Codex CLI, Gemini CLI, Pi, Goose, Claude Agent SDK |
| **Orchestrator** | Runs many harnesses in parallel, tracks their state | Claude Squad, Emdash, Vibe Kanban, herdr |
| **Isolation** | Keeps parallel agents from stepping on each other | git worktrees, container-use, microsandbox, E2B |
| **Surface** | How a human watches and steers — TUI, desktop, web, phone | agent-deck, Crystal, Happy, VibeTunnel |
| **Context** | What the agent knows: specs, skills, memory, MCP tools | Spec Kit, AGENTS.md, Serena, MCP servers |

**Packaging legend used below:** ⌨️ TUI · 🪟 tmux · 🖥️ Desktop · 🌐 Web · 📱 Mobile · 🧩 Editor extension · 🌲 git worktree isolation · 📦 container/VM sandbox

---

## Orchestrators — Terminal & TUI

Keyboard-driven mission control. You stay in the terminal; the tool handles session lifecycle, worktrees and switching between agents.

- [herdr](https://github.com/herdrdev/herdr): Agent-aware multiplexer and runtime your coding agents live on — persistent workspaces, session recovery, and a fast TUI across agents. ![GitHub Repo stars](https://img.shields.io/github/stars/herdrdev/herdr?style=social)
- [Claude Squad](https://github.com/smtg-ai/claude-squad): Terminal app managing multiple agents in isolated workspaces — detached background sessions backed by tmux and persistent git worktrees. Supports Claude Code, Codex, Aider, Gemini, OpenCode and Amp. ![GitHub Repo stars](https://img.shields.io/github/stars/smtg-ai/claude-squad?style=social)
- [ralph-tui](https://github.com/subsy/ralph-tui): Drives an agent through a task list autonomously with an exit-detection loop, so long-running work does not need babysitting. ![GitHub Repo stars](https://img.shields.io/github/stars/subsy/ralph-tui?style=social)
- [ccmanager](https://github.com/kbwo/ccmanager): Coding-agent session manager across git worktrees and projects — carries conversation history and project state into new worktrees. Works with Claude Code, Gemini CLI, Codex CLI, Cursor Agent, Copilot CLI, Cline CLI, OpenCode and Kimi CLI. ![GitHub Repo stars](https://img.shields.io/github/stars/kbwo/ccmanager?style=social)
- [agent-deck](https://github.com/asheshgoplani/agent-deck): One TUI over every session — groups, search, forking, git worktrees, cost tracking and a phone-controlled conductor for the whole fleet. ![GitHub Repo stars](https://img.shields.io/github/stars/asheshgoplani/agent-deck?style=social)
- [ccswarm](https://github.com/nwiizo/ccswarm): Multi-agent orchestration with git worktree isolation and specialised roles for collaborative development. ![GitHub Repo stars](https://img.shields.io/github/stars/nwiizo/ccswarm?style=social)

## Orchestrators — tmux-native

tmux turns out to be an excellent agent substrate: sessions survive disconnects, panes are cheap, and everything is scriptable over SSH. These tools lean into it rather than reinventing it.

- [CLI Agent Orchestrator](https://github.com/awslabs/cli-agent-orchestrator): AWS Labs multi-agent orchestration for coding CLIs — Claude Code, Kiro, Codex and more, each coordinated inside isolated tmux sessions. ![GitHub Repo stars](https://img.shields.io/github/stars/awslabs/cli-agent-orchestrator?style=social)
- [dmux](https://github.com/standardagents/dmux): Dev agent multiplexer pairing coding agents with git worktrees over tmux, one pane per task. ![GitHub Repo stars](https://img.shields.io/github/stars/standardagents/dmux?style=social)
- [amux](https://github.com/mixpeek/amux): Single-file, tmux-native control plane — run, monitor and orchestrate dozens of parallel Claude Code, Codex and Gemini sessions from one web dashboard or your phone, with self-healing sessions. ![GitHub Repo stars](https://img.shields.io/github/stars/mixpeek/amux?style=social)

## Orchestrators — Desktop

Native and Electron/Tauri apps. Better for diff review, multi-pane layouts and anything you want visible on a second monitor.

- [Orca](https://github.com/stablyai/orca): Fan one prompt across several agents, each in its own git worktree, then compare and merge the winner. Ghostty-class terminals with infinite splits, SSH worktrees onto a remote box, native GitHub and Linear browsing, line-level annotation of AI diffs, a design mode that pipes a clicked DOM element into the prompt, and an `orca` CLI so agents can drive the workspace themselves. Desktop, mobile companion and VPS. ![GitHub Repo stars](https://img.shields.io/github/stars/stablyai/orca?style=social)
- [Emdash](https://github.com/generalaction/emdash): Open-source ADE for running multiple coding agents in parallel, each task in its own git worktree. Local-first SQLite state, SSH to remote machines, and Linear/GitHub/Jira/GitLab ticket ingestion with PR creation and CI review built in. ![GitHub Repo stars](https://img.shields.io/github/stars/generalaction/emdash?style=social)
- [Aperant](https://github.com/AndyMik90/Aperant) (formerly Auto Claude): Describe a goal and agents plan, implement and validate it — up to 12 agent terminals in parallel, all changes in git worktrees, a self-validating QA loop before you review, AI-assisted merge-conflict resolution, a memory layer across sessions, and GitHub/GitLab/Linear task import behind a Kanban board. Three-layer security model (OS sandbox, filesystem restriction, dynamic command allowlist). Windows, macOS and Linux. *Note: 2.x is in maintenance mode and code PRs are paused while 3.0 is rebuilt.* ![GitHub Repo stars](https://img.shields.io/github/stars/AndyMik90/Aperant?style=social)
- [superset](https://github.com/superset-sh/superset): Code editor built around running many agents at once rather than around a single cursor. ![GitHub Repo stars](https://img.shields.io/github/stars/superset-sh/superset?style=social)
- [Paseo](https://github.com/getpaseo/paseo): A local daemon manages the agents; desktop, mobile, web and CLI clients all attach to it. One interface over Claude Code, Codex, Copilot, OpenCode and Pi, running on your own machine with your own dev environment. Voice mode, and no telemetry, tracking or forced log-in. ![GitHub Repo stars](https://img.shields.io/github/stars/getpaseo/paseo?style=social)
- [CodeLayer (HumanLayer)](https://github.com/humanlayer/humanlayer): Human-in-the-loop control plane for coding agents — approvals, interventions and durable session state so autonomous runs stay reviewable. ![GitHub Repo stars](https://img.shields.io/github/stars/humanlayer/humanlayer?style=social)
- [CodexMonitor](https://github.com/Dimillian/CodexMonitor): Native macOS app to orchestrate and monitor multiple Codex agents locally. ![GitHub Repo stars](https://img.shields.io/github/stars/Dimillian/CodexMonitor?style=social)
- [AutoMaker](https://github.com/AutoMaker-Org/automaker): Kanban board that turns product tickets into working code, each card implemented by an agent in its own worktree. ![GitHub Repo stars](https://img.shields.io/github/stars/AutoMaker-Org/automaker?style=social)
- [Crystal](https://github.com/stravu/crystal): Desktop app running parallel Claude Code sessions in isolated git worktrees, with side-by-side diff review before merge. ![GitHub Repo stars](https://img.shields.io/github/stars/stravu/crystal?style=social)
- [mux](https://github.com/coder/mux): Coder's desktop app for isolated parallel agentic development. ![GitHub Repo stars](https://img.shields.io/github/stars/coder/mux?style=social)
- [Nimbalyst](https://github.com/nimbalyst/nimbalyst): Visual workspace where you and the agent collaborate in WYSIWYG editors — markdown, mockups with annotations, Mermaid, Excalidraw, CSV, data models and Monaco — reviewing the agent's changes as red/green diffs. Parallel sessions on a kanban, sessions linked to the files they touched, worktrees, and a mobile companion. ![GitHub Repo stars](https://img.shields.io/github/stars/nimbalyst/nimbalyst?style=social)
- [parallel-code](https://github.com/johannesjo/parallel-code): Desktop app for running Claude Code, Codex CLI and Gemini CLI side by side, with a built-in diff viewer and merge flow. ![GitHub Repo stars](https://img.shields.io/github/stars/johannesjo/parallel-code?style=social)
- [Arbor](https://github.com/penso/arbor): Fully native desktop app built around git worktrees, terminals and diffs — the three things an agentic workflow actually touches, and nothing else. ![GitHub Repo stars](https://img.shields.io/github/stars/penso/arbor?style=social)
- [Dorothy](https://github.com/Charlie85270/Dorothy): Desktop app orchestrating multiple AI CLI agents (Claude Code, Codex, Gemini) simultaneously with automations, Kanban management, remote control and MCP servers. ![GitHub Repo stars](https://img.shields.io/github/stars/Charlie85270/Dorothy?style=social)
- [Sculptor](https://github.com/imbue-ai/sculptor): Imbue's agent workspace running each session in a container so agents can execute freely without touching your machine. ![GitHub Repo stars](https://img.shields.io/github/stars/imbue-ai/sculptor?style=social)
- [Termic](https://github.com/simion/termic): Spawns the real `claude`, `codex`, `agy`, `copilot` and `grok` binaries rather than vendor SDKs, so inference rides the Pro/Max plan you already pay for. One git worktree per agent, an optional per-workspace macOS sandbox cage, prompt broadcast to every agent at once, and a work-done indicator per pane. ![GitHub Repo stars](https://img.shields.io/github/stars/simion/termic?style=social)
- [Tempest](https://github.com/tempestai-dev/tempest): Keeps a local code-knowledge graph shared across every parallel session, so five agents do not each re-read the codebase from scratch — the project reports up to 64% less context consumption and 58% fewer tool calls. Worktree and branch per agent, built-in diff and PR, and per-OS process isolation (Job Objects on Windows, Seatbelt on macOS, bubblewrap on Linux). Note that agents are spawned permission-skipping by default, toggleable in settings. ![GitHub Repo stars](https://img.shields.io/github/stars/tempestai-dev/tempest?style=social)
- [Orkas](https://github.com/Orkas-AI/Orkas): Local-first desktop AI workforce whose Commander coordinates specialist agents and external coding CLIs through one chat. ![GitHub Repo stars](https://img.shields.io/github/stars/Orkas-AI/Orkas?style=social)

## Orchestrators — Web & Self-hosted

Browser-based, which means team-shareable and reachable from any device without installing anything.

- [Vibe Kanban](https://github.com/BloopAI/vibe-kanban): Kanban board for managing AI coding agents — queue tasks, review diffs, and switch between Claude Code, Codex, Gemini and others per card. ![GitHub Repo stars](https://img.shields.io/github/stars/BloopAI/vibe-kanban?style=social)
- [gastown](https://github.com/gastownhall/gastown): Scales to 20–30 concurrent agents with a coordinator and a merge queue, aimed at swarm-sized workloads. ![GitHub Repo stars](https://img.shields.io/github/stars/gastownhall/gastown?style=social)
- [OpenHands](https://github.com/OpenHands/OpenHands): Self-hostable platform for software development agents — the agent gets a browser, a terminal and an editor, and you watch it work in a web UI. ![GitHub Repo stars](https://img.shields.io/github/stars/OpenHands/OpenHands?style=social)
- [Open SWE](https://github.com/langchain-ai/open-swe): LangChain's cloud-sandboxed asynchronous coding agent, invoked from Slack, Linear or GitHub and returning a PR. ![GitHub Repo stars](https://img.shields.io/github/stars/langchain-ai/open-swe?style=social)
- [ruflo](https://github.com/ruvnet/ruflo): Agent meta-harness for deploying coordinated multi-agent swarms and long-running autonomous workflows. ![GitHub Repo stars](https://img.shields.io/github/stars/ruvnet/ruflo?style=social)

## Remote & Mobile Control

The ADE stops being a place you sit and becomes a thing you check on. These bridge running sessions to your phone or a chat app.

- [Happy](https://github.com/slopus/happy): Mobile and web client for Claude Code with end-to-end encryption — start a session at your desk, keep steering it from your phone. ![GitHub Repo stars](https://img.shields.io/github/stars/slopus/happy?style=social)
- [VibeTunnel](https://github.com/amantus-ai/vibetunnel): Turns any terminal session into a browser-accessible one, so agents running on your Mac are controllable from anywhere. ![GitHub Repo stars](https://img.shields.io/github/stars/amantus-ai/vibetunnel?style=social)
- [Omnara](https://github.com/omnara-ai/omnara): Command centre for agents across web, mobile and terminal, with live notifications and permission prompts routed to you. ![GitHub Repo stars](https://img.shields.io/github/stars/omnara-ai/omnara?style=social)
- [takopi](https://github.com/banteg/takopi): Telegram bridge that puts an agent session in a chat thread. ![GitHub Repo stars](https://img.shields.io/github/stars/banteg/takopi?style=social)
- [ClaudeClaw](https://github.com/sbusso/claudeclaw): Persistent agent orchestrator as a Claude Code plugin — multi-channel routing (Slack, WhatsApp, Telegram), OS-level sandbox isolation, composable extensions, structured memory and webhook triggers. ![GitHub Repo stars](https://img.shields.io/github/stars/sbusso/claudeclaw?style=social)
- [ADE](https://github.com/arul28/ADE): One workspace for Claude Code, Codex, Cursor, Factory Droid and OpenCode, with every chat and CLI session syncing in real time across macOS, Windows, iOS, web and terminal — start a thread on the desktop and finish it from another machine. ![GitHub Repo stars](https://img.shields.io/github/stars/arul28/ADE?style=social)

## Coding Agents (the engines)

The harnesses that orchestrators drive. Pick the orchestrator for the workflow, the agent for the loop quality and provider support.

- [OpenCode](https://github.com/anomalyco/opencode): The open-source coding agent — keyboard-driven TUI, build/plan agent modes, LSP integration for 20+ languages, MCP support, and 75+ providers plus local models via Ollama and LM Studio. Client-server architecture lets multiple frontends attach to one server. ![GitHub Repo stars](https://img.shields.io/github/stars/anomalyco/opencode?style=social)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli): Google's open-source terminal agent with a large context window and built-in tooling. ![GitHub Repo stars](https://img.shields.io/github/stars/google-gemini/gemini-cli?style=social)
- [Codex CLI](https://github.com/openai/codex): OpenAI's local coding agent, with sandboxed execution modes and headless/CI operation. ![GitHub Repo stars](https://img.shields.io/github/stars/openai/codex?style=social)
- [Aider](https://github.com/Aider-AI/aider): AI pair programming in your terminal, with repo-map context and automatic commits per change. ![GitHub Repo stars](https://img.shields.io/github/stars/Aider-AI/aider?style=social)
- [Crush](https://github.com/charmbracelet/crush): Charm's glamourous terminal coding agent, multi-model with LSP and MCP support. ![GitHub Repo stars](https://img.shields.io/github/stars/charmbracelet/crush?style=social)
- [Qwen Code](https://github.com/QwenLM/qwen-code): Alibaba's CLI agent tuned for the Qwen-Coder models, with agentic repo understanding and workflow automation. ![GitHub Repo stars](https://img.shields.io/github/stars/QwenLM/qwen-code?style=social)
- [SWE-agent](https://github.com/SWE-agent/SWE-agent): The research harness that popularised issue-to-patch automation, with a configurable agent-computer interface. ![GitHub Repo stars](https://img.shields.io/github/stars/SWE-agent/SWE-agent?style=social)
- [mini-SWE-agent](https://github.com/SWE-agent/mini-swe-agent): The same idea in ~100 lines of Python — the reference implementation to read before writing your own harness. ![GitHub Repo stars](https://img.shields.io/github/stars/SWE-agent/mini-swe-agent?style=social)
- [3code](https://github.com/capocasa/3code): The economical coding agent — token budget as a first-class constraint via chunked context, supersede-aware compaction, and aggressive caching; works with any OpenAI-compatible endpoint, benchmarked at 75% fewer tokens than OpenCode on a SWE-bench subset. ![GitHub Repo stars](https://img.shields.io/github/stars/capocasa/3code?style=social)

## Harnesses & Agent SDKs

The loop underneath everything above: model calls, tool dispatch, permissions, session state. You reach for this layer when no existing ADE does what you want and you are building your own — a custom coding agent, an in-house review bot, an orchestrator with opinions.

Listed here because each one is a plausible foundation for an ADE. General-purpose agent frameworks aimed at things other than software development belong in [Awesome Agents](https://github.com/kyrolabs/awesome-agents) instead.

- [Pi](https://github.com/earendil-works/pi): Unified LLM API, agent loop, TUI and a coding CLI, built on a deliberately tiny system prompt with lazily-loaded skills. Usable as-is, but the design intent is that you fork and rewire it. ![GitHub Repo stars](https://img.shields.io/github/stars/earendil-works/pi?style=social)
- [Goose](https://github.com/aaif-goose/goose): Extensible on-machine agent that installs, executes and edits rather than only suggesting. MCP-native, ACP-compatible, and embeddable as a runtime rather than only a CLI. ![GitHub Repo stars](https://img.shields.io/github/stars/aaif-goose/goose?style=social)
- [Agno](https://github.com/agno-agi/agno): Full-stack framework for building, running and managing agent platforms, with memory, knowledge and a control plane included. ![GitHub Repo stars](https://img.shields.io/github/stars/agno-agi/agno?style=social)
- [LangGraph](https://github.com/langchain-ai/langgraph): Graph-structured agent runtime with durable execution, checkpointing and human-in-the-loop interrupts — the state machine most long-running agents eventually need. ![GitHub Repo stars](https://img.shields.io/github/stars/langchain-ai/langgraph?style=social)
- [smolagents](https://github.com/huggingface/smolagents): Hugging Face's barebones library for agents that think in code — small enough to read end to end in an afternoon. ![GitHub Repo stars](https://img.shields.io/github/stars/huggingface/smolagents?style=social)
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python): Lightweight framework for multi-agent workflows with handoffs, guardrails and tracing. Also available for [TypeScript](https://github.com/openai/openai-agents-js). ![GitHub Repo stars](https://img.shields.io/github/stars/openai/openai-agents-python?style=social)
- [Mastra](https://github.com/mastra-ai/mastra): Modern TypeScript framework for agents and AI applications — workflows, agent memory, tool calling, evals and a local dev playground in one package. ![GitHub Repo stars](https://img.shields.io/github/stars/mastra-ai/mastra?style=social)
- [Vercel AI SDK](https://github.com/vercel/ai): The TypeScript toolkit most agent UIs are built on — provider-agnostic model calls, tool loops and streaming primitives. ![GitHub Repo stars](https://img.shields.io/github/stars/vercel/ai?style=social)
- [Pydantic AI](https://github.com/pydantic/pydantic-ai): Type-safe agent framework built on Pydantic, with structured outputs and dependency injection for production pipelines. ![GitHub Repo stars](https://img.shields.io/github/stars/pydantic/pydantic-ai?style=social)
- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework): Successor to Semantic Kernel and AutoGen, for building, orchestrating and deploying agents and multi-agent workflows in .NET and Python. ![GitHub Repo stars](https://img.shields.io/github/stars/microsoft/agent-framework?style=social)
- [VoltAgent](https://github.com/VoltAgent/voltagent): TypeScript agent framework with built-in LLM observability, so traces and evals are not bolted on afterwards. ![GitHub Repo stars](https://img.shields.io/github/stars/VoltAgent/voltagent?style=social)
- [Claude Agent SDK](https://github.com/anthropics/claude-agent-sdk-python): Anthropic's SDK for building on the Claude Code harness — tool execution, sandboxing, hooks and stateful sessions. Also available for [TypeScript](https://github.com/anthropics/claude-agent-sdk-typescript). ![GitHub Repo stars](https://img.shields.io/github/stars/anthropics/claude-agent-sdk-python?style=social)
- [Strands Harness SDK](https://github.com/strands-agents/harness-sdk): AWS's SDK for building an agent harness and controlling it end to end, rather than accepting a vendor's loop. ![GitHub Repo stars](https://img.shields.io/github/stars/strands-agents/harness-sdk?style=social)
- [Cloudflare Agents](https://github.com/cloudflare/agents): Stateful agents on Durable Objects — hibernation between turns, WebSocket sessions and scheduled wake-ups at the edge. ![GitHub Repo stars](https://img.shields.io/github/stars/cloudflare/agents?style=social)
- [TrueForge](https://github.com/truefoundry/trueforge): Owns the whole execution loop — model calls, MCP tools with OAuth, git-backed `SKILL.md` packs, sandboxed execution, tool approvals, subagents, deferred tool loading and compaction — exposed three ways: a chat UI, an HTTP API with a TypeScript SDK, and an embeddable UI SDK. SQLite in local mode, Postgres and Redis once a team shares it. ![GitHub Repo stars](https://img.shields.io/github/stars/truefoundry/trueforge?style=social)

## Editor-native Agents

For when the ADE is your editor rather than a separate app.

- [Zed](https://github.com/zed-industries/zed): High-performance multiplayer editor with a native agent panel, and the origin of the Agent Client Protocol — bring Claude Code, Gemini CLI or Goose into the editor over ACP. ![GitHub Repo stars](https://img.shields.io/github/stars/zed-industries/zed?style=social)
- [Cline](https://github.com/cline/cline): Open-source coding agent in VS Code with plan/act separation, terminal execution and full transparency over every model call. ![GitHub Repo stars](https://img.shields.io/github/stars/cline/cline?style=social)
- [Continue](https://github.com/continuedev/continue): Build and share custom agents and rules across VS Code and JetBrains, with any model. ![GitHub Repo stars](https://img.shields.io/github/stars/continuedev/continue?style=social)
- [Kilo Code](https://github.com/Kilo-Org/kilocode): VS Code agent combining orchestration modes, memory-bank context and multi-provider routing. ![GitHub Repo stars](https://img.shields.io/github/stars/Kilo-Org/kilocode?style=social)

## Autonomous & CI Runners

The headless end of the spectrum: no human at the terminal, work triggered by an issue, a PR or a schedule.

- [gh-aw](https://github.com/github/gh-aw): GitHub's agentic workflows — write the workflow in Markdown, compile it to a GitHub Actions run with a safe, permission-scoped agent. ![GitHub Repo stars](https://img.shields.io/github/stars/github/gh-aw?style=social)
- [claude-code-action](https://github.com/anthropics/claude-code-action): Anthropic's official GitHub Action for running Claude Code on issues and pull requests. ![GitHub Repo stars](https://img.shields.io/github/stars/anthropics/claude-code-action?style=social)
- [run-gemini-cli](https://github.com/google-github-actions/run-gemini-cli): Google's official Action for issue triage, PR review and on-demand agent runs. ![GitHub Repo stars](https://img.shields.io/github/stars/google-github-actions/run-gemini-cli?style=social)
- [codex-action](https://github.com/openai/codex-action): OpenAI's official Action for running Codex headlessly in CI. ![GitHub Repo stars](https://img.shields.io/github/stars/openai/codex-action?style=social)
- [Cyrus](https://github.com/cyrusagents/cyrus): Watches Linear, GitHub and GitLab for issues assigned to it and works them to a PR. ![GitHub Repo stars](https://img.shields.io/github/stars/cyrusagents/cyrus?style=social)
- [remote-swe-agents](https://github.com/aws-samples/remote-swe-agents): Serverless AWS control plane for long-running autonomous software agents. ![GitHub Repo stars](https://img.shields.io/github/stars/aws-samples/remote-swe-agents?style=social)

## Isolation & Sandboxing

The layer that makes parallelism safe. Worktrees isolate the filesystem; containers and microVMs isolate everything else.

- [E2B](https://github.com/e2b-dev/E2B): Secure isolated cloud runtimes purpose-built for executing LLM-generated code, with SDKs for spawning sandboxes per task. ![GitHub Repo stars](https://img.shields.io/github/stars/e2b-dev/E2B?style=social)
- [Daytona](https://github.com/daytonaio/daytona): Secure and elastic infrastructure for running AI-generated code, with sub-second sandbox creation and stateful workspaces. ![GitHub Repo stars](https://img.shields.io/github/stars/daytonaio/daytona?style=social)
- [microsandbox](https://github.com/superradcompany/microsandbox): Self-hosted microVM sandboxes with hardware-level isolation and near-instant startup — the safety of a VM without the boot time. ![GitHub Repo stars](https://img.shields.io/github/stars/superradcompany/microsandbox?style=social)
- [sandbox-runtime](https://github.com/anthropic-experimental/sandbox-runtime): Anthropic's OS-level sandboxing runtime for agents — filesystem and network restrictions applied to the agent's own process tree. ![GitHub Repo stars](https://img.shields.io/github/stars/anthropic-experimental/sandbox-runtime?style=social)
- [container-use](https://github.com/dagger/container-use): Gives every agent its own containerised environment and git branch, so many agents work in parallel without conflicts and you can inspect any of them mid-run. ![GitHub Repo stars](https://img.shields.io/github/stars/dagger/container-use?style=social)
- [Greywall](https://github.com/GreyhavenHQ/greywall): Deny-by-default command sandbox for coding agents — filesystem isolation, network control via a transparent proxy, built-in profiles for Claude Code and OpenCode, and a learning mode that generates configs. ![GitHub Repo stars](https://img.shields.io/github/stars/GreyhavenHQ/greywall?style=social)

## Spec, Planning & Task Layers

Autonomy without a spec produces confident nonsense. These tools give the agent a plan to execute against and a place to record progress.

- [Spec Kit](https://github.com/github/spec-kit): GitHub's toolkit for spec-driven development — specify, plan, break into tasks, then let the agent implement against an explicit contract. ![GitHub Repo stars](https://img.shields.io/github/stars/github/spec-kit?style=social)
- [OpenSpec](https://github.com/Fission-AI/OpenSpec): Spec-driven workflow that gets agent and human aligned on the change before any code is written. ![GitHub Repo stars](https://img.shields.io/github/stars/Fission-AI/OpenSpec?style=social)
- [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD): Agile agent framework assigning planning, architecture and implementation to distinct specialised agent roles. ![GitHub Repo stars](https://img.shields.io/github/stars/bmad-code-org/BMAD-METHOD?style=social)
- [Task Master](https://github.com/eyaltoledano/claude-task-master): Turns a PRD into a dependency-aware task graph the agent works through one task at a time. ![GitHub Repo stars](https://img.shields.io/github/stars/eyaltoledano/claude-task-master?style=social)
- [Backlog.md](https://github.com/MrLesk/Backlog.md): Git-native task manager — Markdown task files in the repo, with CLI, TUI and web board views that agents and humans share. ![GitHub Repo stars](https://img.shields.io/github/stars/MrLesk/Backlog.md?style=social)
- [Agent OS](https://github.com/buildermethods/agent-os): Structured standards, specs and workflows so agents produce code that matches how your team actually builds. ![GitHub Repo stars](https://img.shields.io/github/stars/buildermethods/agent-os?style=social)

## Context, Skills & Routing

What the agent knows, what tools it can reach, and which model answers.

- [MCP Servers](https://github.com/modelcontextprotocol/servers): Reference and community servers for the Model Context Protocol — the standard way to hand agents tools and data sources. ![GitHub Repo stars](https://img.shields.io/github/stars/modelcontextprotocol/servers?style=social)
- [Serena](https://github.com/oraios/serena): Semantic code toolkit exposed over MCP — gives agents symbol-level retrieval and editing instead of blind file reads. ![GitHub Repo stars](https://img.shields.io/github/stars/oraios/serena?style=social)
- [claude-code-router](https://github.com/musistudio/claude-code-router): Routes the Claude Code harness to arbitrary model backends, with per-task routing rules and cost control. ![GitHub Repo stars](https://img.shields.io/github/stars/musistudio/claude-code-router?style=social)
- [claude-code-templates](https://github.com/davila7/claude-code-templates): Large library of ready-made agents, commands, hooks, MCP configs and settings, installable per project. ![GitHub Repo stars](https://img.shields.io/github/stars/davila7/claude-code-templates?style=social)
- [AgentAPI](https://github.com/coder/agentapi): One HTTP API in front of Claude Code, Goose, Aider, Codex and Copilot — the integration seam for building your own ADE surface. ![GitHub Repo stars](https://img.shields.io/github/stars/coder/agentapi?style=social)

## Observability & Cost

Parallel agents burn tokens in parallel. These tell you where they went.

- [ccusage](https://github.com/ccusage/ccusage): Fast CLI for usage and cost analysis of Claude Code sessions, with daily, monthly and per-session breakdowns. ![GitHub Repo stars](https://img.shields.io/github/stars/ccusage/ccusage?style=social)
- [Claude Code Usage Monitor](https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor): Live terminal dashboard with burn-rate tracking and predictions before you hit the limit. ![GitHub Repo stars](https://img.shields.io/github/stars/Maciek-roboblog/Claude-Code-Usage-Monitor?style=social)
- [Manifest](https://github.com/mnfst/manifest): Local-first cost observability for agents and harnesses — tokens, costs, messages and model usage across providers, with OTLP ingestion and self-hosting. ![GitHub Repo stars](https://img.shields.io/github/stars/mnfst/manifest?style=social)

## Review & Quality Gates

Agents generate more diff than a human can read. The bottleneck moves to review.

- [PR-Agent](https://github.com/The-PR-Agent/pr-agent): Automated PR description, review and code suggestions, runnable from CI or as a bot on every pull request. ![GitHub Repo stars](https://img.shields.io/github/stars/The-PR-Agent/pr-agent?style=social)
- [claude-code-security-review](https://github.com/anthropics/claude-code-security-review): Anthropic's security-focused review Action — reasons about the semantics of a diff rather than pattern-matching it, with false-positive filtering. ![GitHub Repo stars](https://img.shields.io/github/stars/anthropics/claude-code-security-review?style=social)

For human-in-the-loop approval gates inside the agent loop itself, see [CodeLayer (HumanLayer)](#orchestrators--desktop) above.

## Protocols & Standards

The plumbing that stops every ADE from writing bespoke glue for every agent.

- [Agent Client Protocol (ACP)](https://github.com/agentclientprotocol/agent-client-protocol): "LSP for coding agents" — a JSON-RPC standard letting any editor host any agent. Originated at Zed, with SDKs in TypeScript, Python, Rust, Kotlin and Java. ![GitHub Repo stars](https://img.shields.io/github/stars/agentclientprotocol/agent-client-protocol?style=social)
- [Model Context Protocol](https://github.com/modelcontextprotocol/modelcontextprotocol): The specification for connecting agents to tools, resources and prompts. ![GitHub Repo stars](https://img.shields.io/github/stars/modelcontextprotocol/modelcontextprotocol?style=social)
- [AGENTS.md](https://github.com/agentsmd/agents.md): A simple open format for the README your agents read — adopted across most harnesses in this list. ![GitHub Repo stars](https://img.shields.io/github/stars/agentsmd/agents.md?style=social)

## Browser & Computer-use Runtimes

When the task leaves the repository: end-to-end testing, scraping, and driving real applications.

- [Browser Use](https://github.com/browser-use/browser-use): Connects any LLM to a live scriptable browser for end-to-end web interaction and testing. ![GitHub Repo stars](https://img.shields.io/github/stars/browser-use/browser-use?style=social)
- [Stagehand](https://github.com/browserbase/stagehand): Production-grade AI browser automation on top of Playwright, mixing deterministic code with natural-language actions. ![GitHub Repo stars](https://img.shields.io/github/stars/browserbase/stagehand?style=social)
- [Steel Browser](https://github.com/steel-dev/steel-browser): Open-source browser infrastructure for agents — session-backed automation, extraction, screenshots and PDFs behind an AI-native CLI. ![GitHub Repo stars](https://img.shields.io/github/stars/steel-dev/steel-browser?style=social)
- [Cua](https://github.com/trycua/cua): Computer-use agent framework with high-performance macOS and Linux VMs for full-desktop automation. ![GitHub Repo stars](https://img.shields.io/github/stars/trycua/cua?style=social)
- [Superagent](https://github.com/pungme/superagent-desktop): macOS desktop app that gives Claude Code and Codex a real browser to drive and an iOS Simulator to install and screenshot apps in, not a headless cloud session. ![GitHub Repo stars](https://img.shields.io/github/stars/pungme/superagent-desktop?style=social)

---

## Comparison Matrix

Orchestrators only — the tools you would actually choose between. "Isolation" is what keeps two parallel agents from colliding.

| Tool | Packaging | Isolation | Parallel agents | Notes |
| --- | --- | --- | --- | --- |
| [Claude Squad](https://github.com/smtg-ai/claude-squad) | ⌨️ TUI | 🌲 worktree + 🪟 tmux | Many | Detached background sessions |
| [herdr](https://github.com/herdrdev/herdr) | ⌨️ TUI | 🌲 worktree | Many | Persistent workspaces, session recovery |
| [ccmanager](https://github.com/kbwo/ccmanager) | ⌨️ TUI | 🌲 worktree | Many | Carries session state into new worktrees |
| [agent-deck](https://github.com/asheshgoplani/agent-deck) | ⌨️ TUI + 📱 | 🌲 worktree | Many | Cost tracking, forking, phone conductor |
| [ralph-tui](https://github.com/subsy/ralph-tui) | ⌨️ TUI | — | One (looped) | Autonomous task-list loop |
| [ccswarm](https://github.com/nwiizo/ccswarm) | ⌨️ TUI | 🌲 worktree | Many | Role-specialised agents |
| [CLI Agent Orchestrator](https://github.com/awslabs/cli-agent-orchestrator) | 🪟 tmux | 🪟 tmux session | Many | AWS Labs, multi-CLI |
| [dmux](https://github.com/standardagents/dmux) | 🪟 tmux | 🌲 worktree + 🪟 tmux | Many | One pane per task |
| [amux](https://github.com/mixpeek/amux) | 🪟 tmux + 🌐 | 🪟 tmux session | Dozens | Single file, self-healing, phone dashboard |
| [Orca](https://github.com/stablyai/orca) | 🖥️ Desktop + 📱 | 🌲 worktree (local + SSH) | Many, fan-out | Terminal splits, diff annotation, scriptable CLI |
| [Emdash](https://github.com/generalaction/emdash) | 🖥️ Desktop | 🌲 worktree | Many | Ticket ingestion, PR + CI review, SSH remotes |
| [Aperant](https://github.com/AndyMik90/Aperant) | 🖥️ Desktop | 🌲 worktree + OS sandbox | Up to 12 | Kanban, QA loop, AI merge, memory layer |
| [Paseo](https://github.com/getpaseo/paseo) | 🖥️ + 📱 + 🌐 + ⌨️ | 🌲 worktree | Many | Local daemon, all clients attach; voice mode |
| [Nimbalyst](https://github.com/nimbalyst/nimbalyst) | 🖥️ Desktop + 📱 | 🌲 worktree | Many | Visual WYSIWYG editors, red/green agent diffs |
| [Arbor](https://github.com/penso/arbor) | 🖥️ Desktop | 🌲 worktree | Many | Native; worktrees, terminals, diffs only |
| [Termic](https://github.com/simion/termic) | 🖥️ Desktop | 🌲 worktree + macOS sandbox | Many | Real CLIs, no SDK; prompt broadcast |
| [Tempest](https://github.com/tempestai-dev/tempest) | 🖥️ Desktop | 🌲 worktree + 📦 process isolation | Many | Shared code-knowledge graph cuts token spend |
| [Crystal](https://github.com/stravu/crystal) | 🖥️ Desktop | 🌲 worktree | Many | Side-by-side diff review |
| [mux](https://github.com/coder/mux) | 🖥️ Desktop | 🌲 worktree | Many | From Coder |
| [Sculptor](https://github.com/imbue-ai/sculptor) | 🖥️ Desktop | 📦 container | Many | Agents run fully sandboxed |
| [Dorothy](https://github.com/Charlie85270/Dorothy) | 🖥️ Desktop | 🌲 worktree | Many | Kanban + automations + MCP |
| [parallel-code](https://github.com/johannesjo/parallel-code) | 🖥️ Desktop | 🌲 worktree | Many | Built-in diff and merge |
| [CodexMonitor](https://github.com/Dimillian/CodexMonitor) | 🖥️ Desktop | 🌲 worktree | Many | Codex-focused, native macOS |
| [Vibe Kanban](https://github.com/BloopAI/vibe-kanban) | 🌐 Web | 🌲 worktree | Many | Board-driven, agent per card |
| [gastown](https://github.com/gastownhall/gastown) | 🌐 Web | 🌲 worktree | 20–30 | Coordinator + merge queue |
| [OpenHands](https://github.com/OpenHands/OpenHands) | 🌐 Web | 📦 container | Many | Browser + terminal + editor per agent |
| [Open SWE](https://github.com/langchain-ai/open-swe) | 🌐 Web | 📦 cloud sandbox | Many | Async, issue-triggered |
| [Happy](https://github.com/slopus/happy) | 📱 Mobile + 🌐 | — (client) | Many | E2E encrypted remote control |
| [Omnara](https://github.com/omnara-ai/omnara) | 📱 Mobile + 🌐 | — (client) | Many | Permission prompts routed to phone |
| [ADE](https://github.com/arul28/ADE) | 🖥️ + 📱 + ⌨️ + 🌐 | — (synced sessions) | Many | Real-time session sync across every device |
| [Orkas](https://github.com/Orkas-AI/Orkas) | 🖥️ Desktop | — | Many | Commander coordinates specialist agents and external coding CLIs |

---

## Notable Proprietary ADEs

Not eligible for this list — it is an open-source list — but they define the category and are worth knowing.

- **[Claude Code](https://claude.com/claude-code)** — Anthropic's terminal agent. Source-available CLI, and the harness most tools above orchestrate.
- **[Warp](https://www.warp.dev/)** — Terminal-first ADE with an integrated autonomous agent that executes multi-step workflows across any repository.
- **[Cursor](https://cursor.com/)** — The editor that made agent-first coding mainstream, with background agents and parallel worktree runs.
- **[Conductor](https://conductor.build/)** — Polished commercial workspace for running many Claude Code agents in parallel with end-to-end task delegation.
- **[Agentastic](https://www.agentastic.dev/)** — Native macOS multi-agent IDE covering 52 coding agents, with each agent in its own git worktree or container (Apple containers and Docker), plus editor, terminals, git, browser automation and agentic review. Free to use, closed development, extensibility said to be on the roadmap.
- **[Factory](https://factory.ai/)** — "Droids" as delegated engineers, with a CLI and a browser control plane.
- **[Trae](https://www.trae.ai/)** — ByteDance's agentic IDE showing live agent to-do lists, context panels and tool pipelines.
- **[Devin](https://devin.ai/)** — Cognition's autonomous engineer with its own cloud workspace.
- **[Amp](https://ampcode.com/)** — Sourcegraph's agent, terminal and editor surfaces sharing one thread model.
- **[Kiro](https://kiro.dev/)** — AWS's spec-driven agentic IDE.
- **[Google Antigravity](https://antigravity.google/)** — Agent-first IDE built around a browser-and-editor agent manager.
- **[Jules](https://jules.google/)** — Google's asynchronous coding agent working from GitHub issues.

## Related Lists

- [Awesome Agents](https://github.com/kyrolabs/awesome-agents) — open-source tools and products for building AI agents.
- [Awesome LangChain](https://github.com/kyrolabs/awesome-langchain) — the LangChain ecosystem.
- [Awesome Agent Orchestrators](https://github.com/andyrewlee/awesome-agent-orchestrators) — exhaustive index of parallel-agent orchestrators.
- [Awesome CLI Coding Agents](https://github.com/bradAGI/awesome-cli-coding-agents) — terminal-native agents and their harnesses.
- [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code) — commands, files and workflows for Claude Code.

## Contributing

Contributions welcome — read [CONTRIBUTING.md](CONTRIBUTING.md) first. In short: open source, on GitHub, in English, actively maintained, demonstrated traction, related to agentic development environments, and added at the **bottom** of the relevant section. Submit a PR, not an issue.

## License

[CC0 1.0 Universal](LICENSE) — to the extent possible under law, KyroLabs has waived all copyright and related rights to this work.
