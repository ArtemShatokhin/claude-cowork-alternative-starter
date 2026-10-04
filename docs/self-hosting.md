# Self-hosting open-source Kortix

Kortix is the open-source AI Management System, and you can run it on your own laptop, a VPS, your VPC or on-prem instead of renting a vendor cloud.

Self-hosting runs Kortix as one Docker Compose stack: the frontend, the API, the LLM gateway, and the Supabase distribution. Agent sessions run on a separate sandbox provider, not on this stack. The default is Daytona; Platinum and E2B are also supported.

## What you need

A Linux host for the one-shot bootstrap, or any macOS or Linux machine where you install the CLI and run the manual path. There is no Windows binary. Point an A/AAAA record for your domain and for `api.<domain>` at the machine, and open ports 80 and 443; the bundled Caddy proxy uses them to issue a TLS certificate.

## Install

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
kortix self-host configure
```

On a bare Linux box, install the CLI and start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host start
```

`kortix self-host configure` asks for your sandbox provider key and optionally a managed-git token.

## Point the CLI at your instance

Kortix stores authentication per host. Your self-hosted stack is the `selfhost` host, so `kortix hosts use selfhost` switches the CLI to it. If you have not signed in there yet, `kortix hosts login selfhost` does that and picks a default project.

## Try it without a domain

To evaluate Kortix with no DNS, initialize with a Cloudflare tunnel instead of a domain:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so keep this mode for evaluation rather than production.

## Updates and backups

Every instance updates itself automatically. Pin an exact version with `kortix self-host update --tag 0.9.84`, or turn the updater off with `--auto-update off`.

Kortix keeps no separate backup system. Each instance stores its data as two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` for the Postgres database and `volumes/storage` for file storage. The instance's `.env` file holds every secret and signing key it uses. Back up all three before you run a destructive command.

## Licence and models

Kortix is open source (Elastic License 2.0): self-host, read and modify the code. A self-hosted instance uses your own LLM key by default; connect it in the model picker after you sign up in the dashboard.

Kortix also runs as managed cloud. [Get started](https://kortix.com). The [migration guide](migrating-from-claude-cowork.md) covers moving a team off Claude Cowork.
