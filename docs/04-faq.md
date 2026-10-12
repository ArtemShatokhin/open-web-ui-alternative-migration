# FAQ: moving to Kortix, the open-source AI Operating System

Kortix is the open-source AI Operating System, and these are the questions a team running Open WebUI asks before it moves. Each answer stands on its own.

## Does Kortix replace Open WebUI?

Kortix is a different layer, and it can run alongside Open WebUI. Open WebUI is a chat and retrieval interface; Kortix is an AI Operating System that runs agents on isolated cloud computers and brings their work back for review. A team can keep Open WebUI as its chat window while Kortix takes over the agent work.

## Do my Open WebUI models and API keys carry over?

Yes. Open WebUI connects to Ollama and to any OpenAI-compatible API, so the provider keys you already hold are the ones you give Kortix. Kortix is model-agnostic: bring a key from any major provider, or sign in with the ChatGPT plan you already pay for, and choose the model per agent, per session, or per message.

## What happens to my prompts and tool servers?

Shared prompts become skills, and model presets become agent files in the project repo. Tool servers, whether MCP or OpenAPI, are added back as Kortix connectors, and connector credentials are brokered server-side and never enter the machine. Each agent's reach into a tool is set to Allow, Ask, or Block.

## How does approval work if the agent takes an action?

Kortix sets a policy per tool call, down to the arguments of the call. An Ask holds the call until a person approves it, then the agent resumes. Approval gates are off until you set them, so start with the calls that matter. Separately, merge is default-deny for agents, and session work reaches `main` through a change request a person approves.

## Can I self-host Kortix?

Yes. `kortix self-host start` brings up one Docker Compose stack on your own box, and self-host is free. The same project can run in your VPC or on your own on-prem network. The hardened path for multi-user access, SAML 2.0 single sign-on, SCIM 2.0, per-resource permissions, and an audit trail is the enterprise deployment.

## Is my company configuration locked into a service?

No. Agents, skills, memory, connector configuration, and triggers are files in a git repo you own, versioned and diffable. Separate from settings in a vendor's database, the repo is portable and auditable.

## Is Kortix open source?

Yes. Kortix is the open-source AI Operating System, and the code is open source: you can read it, fork it, and audit it. See [Kortix on GitHub](https://github.com/kortix-ai/suna).

## Where do I start?

Run the [migration walkthrough](01-migration-walkthrough.md), then compare the two platforms at [openwebuialternative.com/kortix-vs-open-webui](https://openwebuialternative.com/kortix-vs-open-webui). The reference site for both stacks is at [openwebuialternative.com](https://openwebuialternative.com/).
