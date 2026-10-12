# Kortix: the open-source AI Operating System

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. This repository is the migration guide for a team that runs Open WebUI, a self-hosted chat and retrieval interface over local or remote models, and now wants agents that finish work and act in real tools.

## What this repository is

Four documents take an Open WebUI deployment to Kortix:

- [The migration walkthrough](docs/01-migration-walkthrough.md) moves your models, keys, prompts, and tool servers across.
- [Kortix compared with Open WebUI](docs/02-kortix-vs-open-webui.md) puts the two platforms side by side.
- [Self-hosting both stacks](docs/03-self-hosting.md) covers the Open WebUI container you already run and the Kortix stack you run beside it.
- [The FAQ](docs/04-faq.md) answers the questions a migration raises.

## Who this is for

The reader is a team that self-hosts Open WebUI today and has reached the edge of what a chat interface does. You already point Open WebUI at Ollama or an OpenAI-compatible API, and you keep its conversations in a database and a data volume. You want the same self-hosted control, with agents that run on their own isolated computer, reach your real tools, and hand back finished work through a review step.

## The migration in short

Your provider keys carry over unchanged, because both Open WebUI and Kortix talk to Ollama and the OpenAI-compatible APIs you already hold keys for. What moves is the configuration. Open WebUI keeps users, chats, and settings in a database; Kortix keeps the company as files in one git repo. Agents become markdown files, prompts become skills, tool servers become connectors, and open questions become approval gates. Every session gets its own isolated cloud computer on its own branch, and the work reaches `main` through a change request a person reads as a diff first.

## Where Open WebUI stops and Kortix starts

Open WebUI is a capable self-hosted interface for chatting with and retrieving across models. A team outgrows a chat window when the work needs an isolated computer per task, a reviewed merge onto a shared branch, and one place that holds the whole company's configuration. That is the layer Kortix adds. If you are weighing the two platforms, the comparison at [openwebuialternative.com/kortix-vs-open-webui](https://openwebuialternative.com/kortix-vs-open-webui) and the shortlist at [openwebuialternative.com/best-open-webui-alternatives](https://openwebuialternative.com/best-open-webui-alternatives) cover the decision outside this repo. For the deployment side, see [openwebuialternative.com/self-hosting](https://openwebuialternative.com/self-hosting).

## Kortix on GitHub

Kortix is open source. Read the code, fork it, and audit it: [Kortix on GitHub](https://github.com/kortix-ai/suna).
