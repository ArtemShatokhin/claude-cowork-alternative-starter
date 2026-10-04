# Migrating from Claude Cowork to open-source Kortix

Kortix is the open-source AI Management System, and moving a team off Claude Cowork means turning settings you configured inside a vendor product into files in a git repository you own.

Claude Cowork is Anthropic's hosted agent product: it works in folders and connected tools and returns finished work for review ([Anthropic's Claude Cowork page](https://claude.com/product/cowork)). Kortix has the same concepts, but each one is a file in the project repo instead of a setting in someone else's database.

## What carries over

| Concept | In Claude Cowork | In Kortix |
|---|---|---|
| Agents | Sub-agents configured in the app | Markdown files in `agents/`, declared in `kortix.yaml` |
| Skills | Skills and plugins built for Cowork | Markdown files in `skills/` |
| Memory | Context held inside the product | Files in `memory/` you can grep and diff |
| Connectors | Tools connected in the app | Connectors in `kortix.yaml`, credentials brokered server-side |
| Scheduled tasks | Recurring tasks in the app | Triggers in `kortix.yaml` (cron and webhooks) |
| Model access | Claude models, plus Amazon Bedrock, Google Cloud, Foundry | Any model, your keys, per agent or session |
| Review | Output you review in the app | A change request you read as a diff and merge |

## What does not carry over

Claude Cowork skills and plugins are built for that product and do not load in Kortix unchanged. The instructions and procedures inside them port over as markdown skill files you write into the repo.

App-level settings, seat assignments and Anthropic admin controls have no direct equivalent. Kortix grants access per agent in `kortix.yaml` (connectors, secrets, skills and permissions), and manages people through account roles.

Model routing tied to Claude does not carry over either, because Kortix is model-agnostic. Each agent picks its model and key.

## The migration, step by step

1. Install the CLI with `curl -fsSL https://kortix.com/install | bash`, then run `kortix init my-app` and `cd my-app`.
2. Add the work as files. Put agent instructions in `agents/`, procedures in `skills/`, and the context the team relies on in `memory/`. All three are markdown.
3. Declare the tools. Add connectors and triggers to `kortix.yaml`. Run `kortix ship`; it prompts for any missing secret or connection.
4. Rebuild scheduled tasks as triggers. A cron schedule or a signed webhook starts a session with no one present, the same jobs Claude Cowork runs on a schedule.
5. Point each agent at a model and a key. Bring your own from any major provider, or use your own OpenAI-compatible endpoint.
6. Connect the channels you use: Slack, Microsoft Teams, email, mobile, the API.
7. Run a session, read the change request it opens, and merge it. Move one job first, then the rest.

## Why the git-repo model changes the migration

A Kortix project is one git repository. It holds a manifest (`kortix.yaml`), the agent config, and the state the agent produces, with no separate database to keep in sync. You can grep the whole company, diff any change an agent makes to its own config, and roll back any part of it.

Each session runs on its own branch in its own isolated Linux sandbox. The agent can install, run and break anything inside that sandbox, and only commits survive. Work reaches your default branch only through a change request you review as a diff and merge.

Kortix is model-agnostic. You pick the model per agent, per session or per message, so a migration is not tied to one vendor's roadmap.

Start with the [self-hosting guide](self-hosting.md) if you run your own infrastructure, or [the Claude Cowork alternative guide](https://claudecoworkalternative.com) if you are still comparing options. Kortix runs self-hosted or as managed cloud; [Get started](https://kortix.com).
