# Claude Cowork alternative FAQ (open source)

Kortix is the open-source AI Management System, and these are the questions teams ask when they move off Claude Cowork.

## Where does my data live after I switch?

On Kortix you choose. Self-host the open-source stack on your laptop, a VPS, your VPC or on-prem, and the data stays on infrastructure you control. Managed Kortix Cloud runs the same system for you. Claude Cowork is a vendor-hosted app, so Anthropic operates the service ([Anthropic's Claude Cowork page](https://claude.com/product/cowork)).

## Does Kortix run without Anthropic?

Yes. Kortix is model-agnostic. Pick Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, per agent, per session or per message, and bring your own API key. Claude Cowork uses Claude models and can route model calls through Amazon Bedrock, Google Cloud or Microsoft Foundry, but it remains an Anthropic product.

## Can I keep using Slack, Teams and email?

Kortix starts the same session from the web app, Slack, Microsoft Teams, email, mobile, the CLI or the API. Cron schedules and signed webhooks start sessions with no one present. Claude Cowork runs on web, desktop and mobile, and its Slack connector is included on Team seats.

## How much work is the migration?

Most of the effort goes into rewriting skills and agent instructions as markdown files in one git repo. Connectors, triggers and secrets move into `kortix.yaml`, and `kortix ship` prompts for the values it needs. Start with one job, watch the change requests, then move the rest. The [migration guide](migrating-from-claude-cowork.md) has the steps.

## What does Kortix cost?

Self-hosting the open-source code has no Kortix seat fee; you pay for your own infrastructure. Managed Kortix Cloud is Free ($0, 200 sandbox credits a month, one project), Team ($40 per seat per month, 2,500 pooled credits per seat) or Enterprise (custom, with VPC and on-prem options). [Kortix](https://kortix.com/pricing) lists the current plans, checked October 2026.

## Who approves what the agents do?

Every session runs on its own branch and cannot reach the default branch. When the agent finishes, it opens a change request, and nothing lands until a human reads the diff and merges it. In Claude Cowork you review output inside the app and choose the folders and tools Claude may reach.

## Is Kortix really open source?

Yes. The code is public at [Kortix on GitHub](https://github.com/kortix-ai/suna), and you can self-host it, read it and modify it. The [self-hosting guide](self-hosting.md) covers install, updates and backups.

## Do I lose the skills and plugins I built for Claude Cowork?

Claude Cowork skills and plugins are built for that product, so they do not load in Kortix unchanged. The instructions and procedures inside them port over: rewrite each as a markdown skill file in the project's `skills/` directory. Connectors are rewired in `kortix.yaml`, and memory arrives as files you can grep and diff.

If you are still comparing tools, [the Claude Cowork alternative guide](https://claudecoworkalternative.com) has the full field.
