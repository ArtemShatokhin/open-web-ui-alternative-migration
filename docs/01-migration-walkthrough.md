# Migrating from Open WebUI to Kortix: the open-source AI Operating System

Kortix is the open-source AI Operating System, and this walkthrough moves a team from an Open WebUI chat interface to agents that return finished work. Open WebUI is a self-hosted platform that puts a chat and retrieval interface over Ollama and OpenAI-compatible APIs. Kortix keeps the provider keys you already hold and moves the agent configuration into a git repo you own.

## What carries over unchanged

Your models and API keys move with you. Open WebUI connects to Ollama and to any OpenAI-compatible API, and its own documentation points that API URL at LMStudio, GroqCloud, Mistral, OpenRouter, and vLLM ([Open WebUI repository](https://github.com/open-webui/open-webui)). Kortix is model-agnostic: bring an API key from any major provider, or sign in with the ChatGPT plan you already pay for, and choose the model per agent, per session, or per message. The same credentials keep working. You re-enter them in Kortix as secrets rather than typing them into an admin panel.

## What moves into the git repo

Open WebUI keeps conversations, users, and settings in a data volume, backed by SQLite or PostgreSQL ([Open WebUI quick start](https://docs.openwebui.com/getting-started/quick-start/)). Kortix keeps the company as text: a project is a git repo that holds agents, skills, memory, connector configuration, and triggers, and `kortix.yaml` declares the machine image, the connectors, and the triggers. A prompt, a tool binding, or a permission rule becomes a file you can diff, review, and roll back.

## How prompts and agents move

In Open WebUI, an agent is a configuration wrapper: a base model with a system prompt, bound tools, and attached knowledge ([Open WebUI features](https://docs.openwebui.com/features/)). In Kortix, an agent is `agents/<name>.md` for its behavior plus an `agents.<name>` block in `kortix.yaml` for its governance. Recreate each Open WebUI model preset as an agent file and keep the system prompt as the body. Prompts the team reuses become skills: markdown plus scripts that encode how the company does one job.

## How tool servers become connectors

Open WebUI reaches external services through Python tools, pipelines, native MCP, and OpenAPI servers ([Open WebUI features](https://docs.openwebui.com/features/)). Kortix reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP, and connector credentials are brokered server-side and never enter the machine. Migrate each MCP or OpenAPI server by adding the same endpoint as a Kortix connector, then scope which agent may touch it with Allow, Ask, or Block.

## How approvals and review change

Open WebUI gives each chat a tool approval mode and controls the workspace boundary by workspace policy ([Open Terminal documentation](https://docs.openwebui.com/ecosystem/open-terminal/)). Kortix sets Allow, Ask, or Block per tool call, down to the arguments of the call, and approval gates are off until you set them. The larger change is review. Each session runs on its own isolated cloud computer on its own branch, and its work reaches `main` through a change request you read as a diff first. Merge is default-deny for agents, so nothing lands in the shared branch without a person.

## A migration checklist

1. List the provider connections and keys in Open WebUI's admin settings.
2. Install the Kortix CLI and scaffold a project with `kortix init`, which creates `kortix.yaml`.
3. Store the provider keys as secret names in the project.
4. Convert each model preset into an agent file and each shared prompt into a skill.
5. Recreate MCP and OpenAPI tool servers as connectors, with a policy per call.
6. Move reference documents into company memory files and connectors.
7. Run `kortix ship`, start a session, and review the first change request.

## What the team gets on the other side

The company configuration is one repo a person can read and an agent can edit. Thousands of agents can run in parallel on that one config, each on its own cloud computer. Work arrives as finished deliverables and reviewed diffs, and the model stays your choice, with your keys.

The same decision, with the two platforms side by side, is at [openwebuialternative.com/kortix-vs-open-webui](https://openwebuialternative.com/kortix-vs-open-webui), and the deployment notes are at [openwebuialternative.com/self-hosting](https://openwebuialternative.com/self-hosting).
