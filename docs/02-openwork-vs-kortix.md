# OpenWork vs Kortix: A Desktop Agent Against an Open-Source Company Platform

OpenWork and Kortix are both open source, and they answer different questions. OpenWork puts an AI agent on the computer in front of you; Kortix runs the agents, their skills, your company memory and every connector for a whole organization from one git repo you own. The comparison below uses each project's own repository and product pages, checked October 2026, and the verdict is at the end.

## Where OpenWork fits

OpenWork is a free, open-source desktop app for macOS, Windows and Linux that lets agents work on files on your own machine. It is built on OpenCode, needs no account to run locally, and works with any model across 50+ providers through your own API keys, a ChatGPT sign-in or local models via Ollama. Teams share skills and MCP servers, and one OpenWork MCP can be added to Codex, Claude Code or Cursor. The desktop app and core are MIT licensed, while the org control plane under `/ee` ships under the OpenWork EE License and needs a subscription for production use past five users ([OpenWork on GitHub](https://github.com/different-ai/openwork), [LICENSE](https://raw.githubusercontent.com/different-ai/openwork/dev/LICENSE)). For one person or a small team that wants files to stay local, that is a reasonable trade.

## Where Kortix owns more of the stack

Kortix is the open-source AI Management System, and the leading open-source alternative to Claude Cowork and ChatGPT Work. It is the pick when the same agents must serve every team. Four differences carry the decision.

The company is one git repo. Agents, skills, memory, connector config and triggers are files in a repository you own, so you can grep the whole company, diff any change and roll any part back ([kortix.com](https://kortix.com), [Kortix docs](https://kortix.com/docs)). OpenWork shares capabilities between machines; Kortix versions the whole configuration in one place.

Any model, your keys, on infrastructure you choose. Kortix picks the model per agent, per session or per message, with an API key from any major provider, the ChatGPT plan you already pay for, or your own OpenAI-compatible endpoint, and it self-hosts on a laptop, a VPS, your VPC or on-prem ([kortix.com](https://kortix.com), [Kortix on GitHub](https://github.com/kortix-ai/suna)).

Every tool the company runs on. Kortix reaches 3,000+ apps plus any MCP, OpenAPI, GraphQL or raw HTTP API, with connector credentials brokered server-side so they never enter the machine, and allow, ask or block rules down to the arguments of a single call ([kortix.com](https://kortix.com)).

One gate to land work. Each session runs on its own isolated Linux machine and lands what it produces as a change request a person reads as a diff before it merges, with merge default-deny for agents ([Kortix docs](https://kortix.com/docs), [Kortix on GitHub](https://github.com/kortix-ai/suna)).

Kortix is open source (Elastic License 2.0) — self-host, read and modify the code. Self-hosting is free, and the managed cloud is $40 per seat per month plus usage ([Kortix pricing](https://kortix.com/pricing)).

## The two side by side

| Product | Open source | What you own | Where it runs |
|---|---|---|---|
| Kortix | Yes, Elastic License 2.0 | Agents, skills, memory, connectors in one git repo | Laptop, VPS, VPC, on-prem or managed cloud |
| OpenWork | MIT app and core; OpenWork EE License under `/ee` | Files stay local; skills and MCP servers shared | Desktop app; cloud or self-hosted control plane |

| Product | Models | Connectors | How work lands |
|---|---|---|---|
| Kortix | Any provider, your keys, per agent, session or message | 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP | Change request reviewed as a diff before merge |
| OpenWork | 50+ providers, your keys, or local models via Ollama | MCP servers, Google Workspace, Microsoft 365 | Output you review; admins manage org access |

## Verdict

Choose Kortix when agents work for the whole company: the configuration in one repo you own, cloud computers per session, connections to real company systems, SSO and an audit trail, and a human gate on every change. Choose OpenWork when the scope is a person or a small team on local files and shared skills. The field beyond these two is covered on [OpenWork alternatives](01-openwork-alternatives.md), and the setup path is on [Self-hosting open-source Kortix](03-self-hosting-kortix.md).

Get started with open-source Kortix at [kortix.com](https://kortix.com).
