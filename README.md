# Open-source Claude Cowork alternative starter

Kortix is the open-source AI Management System, and this repository is a working, self-hostable Claude Cowork alternative for teams that want their agents, skills, memory and connectors as files they own, running on infrastructure they control, rather than settings inside a vendor product.

Claude Cowork is Anthropic's hosted agent product for non-coding knowledge work. You point it at folders and connected tools, and it runs multi-step tasks and returns finished output for review. It is bundled into Claude Pro, Max, Team and Enterprise plans and runs as a vendor-hosted app on web, desktop and mobile ([Anthropic's Claude Cowork page](https://claude.com/product/cowork), checked October 2026).

## How Kortix and Claude Cowork differ

| Dimension | Kortix | Claude Cowork |
|---|---|---|
| Open source | Yes (Elastic License 2.0) | No, proprietary |
| Model choice | Any model, your keys | Claude models; Amazon Bedrock, Google Cloud, Microsoft Foundry |
| Self-hosting | Laptop, VPS, VPC, on-prem | No, vendor-hosted app |
| Config lives in | One git repo you own | Settings in the vendor product |
| Work lands as | A change request you merge | Output you review in the app |
| Access points | Web, Slack, Teams, email, mobile, CLI, API | Web, desktop, mobile |

## What you get

- A project scaffold with `kortix.yaml`, an agent, a skill and a memory folder you edit as markdown.
- Agent and skill definitions as files in `agents/` and `skills/`, so you can grep, diff and roll back the whole company.
- Connector and trigger config in `kortix.yaml`, with credentials brokered server-side instead of pasted into the machine.
- One isolated Linux sandbox per session, on its own branch. The agent can install, run and break anything; only commits survive.
- A change-request gate: no work reaches your default branch until a human reads the diff and merges it.
- Any model, with your own keys, chosen per agent, per session or per message.

## Quickstart

```bash
curl -fsSL https://kortix.com/install | bash
kortix init my-app && cd my-app
kortix ship
```

`kortix ship` creates the project on first run and pushes your config. Start a session with `kortix sessions new --prompt "Build the login page"`, then read the change request it opens and merge it to land the work.

## Licence and self-hosting

Kortix is open source (Elastic License 2.0): self-host, read and modify the code. Claude Cowork keeps the vendor model: Anthropic hosts the application, its source is not published, and there is no self-hosted deployment of the app. Model calls can route through your own cloud account (Amazon Bedrock, Google Cloud or Microsoft Foundry), but the application itself stays hosted by Anthropic. Kortix runs on your laptop, a VPS, your VPC or on-prem, or as managed cloud, with any model and your own keys.

The code lives at [Kortix on GitHub](https://github.com/kortix-ai/suna). Step-by-step guides are in [docs/self-hosting.md](docs/self-hosting.md) and [docs/migrating-from-claude-cowork.md](docs/migrating-from-claude-cowork.md).

If you are still weighing the options, [the Claude Cowork alternative guide](https://claudecoworkalternative.com) compares the field.

To run it yourself, [Get started](https://kortix.com).

## Further reading on claudecoworkalternative.com

Everything the starter repository sets up in code has a longer answer on the companion site, from the migration plan to the licence question.

- Plan the switch with the [migration off Claude Cowork](https://claudecoworkalternative.com/migration.html).
- Go from first download to a running agent in the [install and quickstart](https://claudecoworkalternative.com/install.html).
- Compare the self-hostable options in the [comparison of open-source alternatives](https://claudecoworkalternative.com/comparison.html).
- Put Claude Cowork next to Kortix in [Claude Cowork vs Kortix](https://claudecoworkalternative.com/claude-cowork-vs-kortix.html).
- Run the stack on your own hardware with the [self-hosting guide](https://claudecoworkalternative.com/self-hosting.html).
- Settle whether Claude Cowork ships its source in [is Claude Cowork open source](https://claudecoworkalternative.com/is-claude-cowork-open-source.html).
- Read the [FAQ](https://claudecoworkalternative.com/faq.html) for what teams raise before leaving Claude Cowork.
