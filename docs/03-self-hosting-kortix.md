# Self-Hosting Open-Source Kortix: Setup and What You Own

Kortix is the open-source AI Management System, and it self-hosts as one Docker Compose stack you run on your own hardware. The verified setup path below comes from Kortix's own documentation and says exactly what you own once the stack is up. The steps and flags below come from the Kortix self-hosting page, checked October 2026 ([Kortix self-hosting docs](https://kortix.com/docs/host)).

## What the stack is

A self-hosted Kortix instance is one Docker Compose stack: the frontend, the API, the LLM gateway and the Supabase distribution. Agent sessions run on a separate sandbox provider rather than on this stack, and the default provider is Daytona, with Platinum and E2B also supported ([Kortix self-hosting docs](https://kortix.com/docs/host)). You can run it on a laptop, a VPS, your own VPC or your own on-prem network, and a Kortix Cloud account is not required for a self-hosted install ([Kortix on GitHub](https://github.com/kortix-ai/suna)).

## Install the CLI

Every path starts with the Kortix CLI. On any OS, install it with:

```bash
curl -fsSL https://kortix.com/install | bash
```

The same install line is what the Kortix quickstart publishes ([Kortix on GitHub](https://github.com/kortix-ai/suna), [Kortix docs](https://kortix.com/docs)).

## Manual install on a Linux server

This is the production-style path.

1. Point DNS. Create an A or AAAA record for your domain and for `api.<domain>`, both pointing at the server's IP, and open ports 80 and 443. The bundled Caddy proxy uses those ports to issue a TLS certificate ([Kortix self-hosting docs](https://kortix.com/docs/host)).
2. Initialize the instance:

```bash
kortix self-host init --domain kortix.example.com
```

3. Start the stack:

```bash
kortix self-host start
```

4. Watch it come up with `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor` ([Kortix self-hosting docs](https://kortix.com/docs/host)).
5. Configure the sandbox provider key and optionally a managed-git token:

```bash
kortix self-host configure
```

Then sign up in the dashboard and connect your own LLM key in the model picker. Self-hosted instances use your own key by default ([Kortix self-hosting docs](https://kortix.com/docs/host)).

On a bare Linux box you can skip the manual steps with the one-shot bootstrap script, which installs Docker, installs the CLI, and starts the stack in one command. The script and its flags are documented on the [Kortix self-hosting page](https://kortix.com/docs/host).

## Evaluation install with a tunnel

To try Kortix without buying a domain, use a Cloudflare tunnel instead of a domain:

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use this mode for evaluation rather than production ([Kortix self-hosting docs](https://kortix.com/docs/host)).

## Updates and backups

Self-hosted instances update themselves automatically. You can pin an exact release with `kortix self-host update --tag <version>` or turn the updater off with `--auto-update off` ([Kortix self-hosting docs](https://kortix.com/docs/host)).

Kortix has no separate backup system. Each instance stores its data under `~/.config/kortix/self-host/<instance>/`: the Postgres database in `volumes/db/data`, file storage in `volumes/storage`, and every secret and signing key in the instance `.env` file. Back up all three ([Kortix self-hosting docs](https://kortix.com/docs/host)).

## What you own afterwards

The point of running Kortix yourself is that the company becomes a git repository you control. Agents, skills, memory, connector config and triggers are files in one repo, and `kortix.yaml` declares the machine image, the connectors and the triggers ([kortix.com](https://kortix.com), [Kortix docs](https://kortix.com/docs)). Each session runs an agent in an isolated sandbox on its own branch, and when the work is ready the agent opens a change request you review and merge to the default branch ([Kortix docs](https://kortix.com/docs)). The configuration, the memory and the connectors stay in your repo wherever the stack runs, so moving between self-hosted and cloud changes the machine and not the company. Kortix is open source (Elastic License 2.0) — self-host, read and modify the code ([Kortix on GitHub](https://github.com/kortix-ai/suna)).

Get started with open-source Kortix at [kortix.com](https://kortix.com).
