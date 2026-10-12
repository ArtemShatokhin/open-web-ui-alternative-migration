# Self-hosting Kortix and Open WebUI: the open-source AI Operating System

Kortix is the open-source AI Operating System, and it self-hosts for free on your own machine or network. Open WebUI self-hosts the same way, with Docker as its recommended install. Both commands are here, with notes on what each stack runs, so you can bring Kortix up beside an Open WebUI instance you already operate.

## Self-host Kortix first

Install the Kortix CLI and start the stack on your own box:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host start
```

That brings up one Docker Compose stack. The first run asks six things and no model key; models are bring-your-own-key in the app, GitHub connects from the dashboard, and the stack has no Redis and no separate worker. Self-host is free, and the same project runs on Kortix Cloud, in your VPC, or on your own on-prem network when you want managed compute ([Kortix documentation](https://kortix.com/docs)).

## Self-host Open WebUI

Open WebUI recommends Docker for most users. With Docker installed, its documented command is:

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data -e WEBUI_SECRET_KEY=your-secret-key --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

The UI comes up on port 3000, the `open-webui` volume holds chats, users, and settings, and the secret key should be generated once with `openssl rand -hex 32` and kept, because containers recreated without it log everyone out ([Open WebUI quick start](https://docs.openwebui.com/getting-started/quick-start/)). Open WebUI also installs with pip or Kubernetes, and offers a `:slim` image for chat over hosted APIs ([Open WebUI documentation](https://docs.openwebui.com/)).

## What each stack runs

The Kortix stack is one Docker Compose stack with no Redis and no separate worker. Open WebUI runs a single stateless application and, for multiple replicas behind a load balancer, coordinates them with Redis and WebSocket support ([Open WebUI repository](https://github.com/open-webui/open-webui)).

## Running both during a migration

Keep the Open WebUI instance up while Kortix takes over agent work, so people keep their chat interface and their history. Point both platforms at the same provider keys. As agents move to Kortix, the knowledge and tools they need move with them as connector configuration and memory files, and the Open WebUI instance can stay as the team's chat layer for as long as it is useful.

## Where to go next

The deployment comparison is at [openwebuialternative.com/self-hosting](https://openwebuialternative.com/self-hosting), and the migration steps are in [the walkthrough](01-migration-walkthrough.md).
