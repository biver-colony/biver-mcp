<div align="center">

<img src="https://mcp.biver.id/icon-256.png" alt="Biver" width="96" height="96" />

# Biver MCP

**Build, edit, and publish Biver landing pages from your AI assistant.**

Bikin, edit, dan terbitkan landing page Biver langsung dari asisten AI Anda.

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-id.biver%2Fbiver-0A7B83)](https://registry.modelcontextprotocol.io/v0.1/servers?search=id.biver/biver)
[![Protocol](https://img.shields.io/badge/MCP-2026--07--28-1F2937)](https://modelcontextprotocol.io)
[![Tools](https://img.shields.io/badge/tools-50-F59E0B)](https://biver.id/docs/mcp-server)
[![Auth](https://img.shields.io/badge/auth-OAuth%202.1-16A34A)](https://biver.id/docs/claude-connector)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

[Website](https://biver.id) · [Docs](https://biver.id/docs/mcp-ai-assistant) · [Server reference](https://biver.id/docs/mcp-server) · [Support](mailto:support@biver.id)

</div>

---

Biver is a landing page builder for Indonesian businesses. This repository connects a Biver workspace to Claude, ChatGPT, Cursor, VS Code, Codex, Gemini CLI, and any other client that speaks the Model Context Protocol.

One connection works on one workspace. You sign in with your Biver account in the browser. You do not copy an API key.

## Server

| | |
| --- | --- |
| Sign in with Biver (OAuth) | `https://mcp.biver.id/mcp` |
| API key | `https://api.biver.id/mcp` with `Authorization: Bearer <key>` |
| Transport | Streamable HTTP |
| Protocol | `2026-07-28`, `2025-11-25`, `2025-06-18`, `2025-03-26` |

## Install in one click

| Client | Sign in with Biver | API key |
| --- | --- | --- |
| Cursor | [Install](https://cursor.com/install-mcp?name=biver&config=eyJ1cmwiOiJodHRwczovL21jcC5iaXZlci5pZC9tY3AifQ%3D%3D) | [Install](https://cursor.com/install-mcp?name=biver&config=eyJ1cmwiOiJodHRwczovL2FwaS5iaXZlci5pZC9tY3AiLCJoZWFkZXJzIjp7IkF1dGhvcml6YXRpb24iOiJCZWFyZXIgJHtlbnY6QklWRVJfQVBJX0tFWX0ifX0%3D) |
| VS Code | [Install](https://insiders.vscode.dev/redirect/mcp/install?name=biver&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.biver.id%2Fmcp%22%7D) | [Install](https://insiders.vscode.dev/redirect/mcp/install?name=biver&inputs=%5B%7B%22type%22%3A%22promptString%22%2C%22id%22%3A%22biver_api_key%22%2C%22description%22%3A%22Biver%20API%20key%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.biver.id%2Fmcp%22%2C%22headers%22%3A%7B%22Authorization%22%3A%22Bearer%20%24%7Binput%3Abiver_api_key%7D%22%7D%7D) |
| Visual Studio | [Install](https://vs-open.link/mcp-install?%7B%22name%22%3A%22biver%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.biver.id%2Fmcp%22%7D) | |
| LM Studio | [Install](https://lmstudio.ai/install-mcp?name=biver&config=eyJ1cmwiOiJodHRwczovL21jcC5iaXZlci5pZC9tY3AifQ%3D%3D) | |
| Kiro | [Install](https://kiro.dev/launch/mcp/add?name=biver&config=%7B%22url%22%3A%22https%3A%2F%2Fmcp.biver.id%2Fmcp%22%7D) | |

## Install from the terminal

**Claude Code** (plugin with the Biver workflow skill):

```bash
claude plugin marketplace add biver-colony/biver-mcp
claude plugin install biver@biver
```

Or the server only:

```bash
claude mcp add --transport http biver https://mcp.biver.id/mcp
```

**Codex**

```bash
codex mcp add biver --url https://mcp.biver.id/mcp
codex mcp login biver
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/biver-colony/biver-mcp
```

**Claude.ai and ChatGPT:** add a custom connector with the URL `https://mcp.biver.id/mcp`, then sign in.

Guides for Cline, Kilo Code, OpenCode, Zed, Goose, JetBrains, Devin Desktop, OpenClaw, Hermes Agent, and n8n are in the [install guide](https://biver.id/docs/mcp-ai-assistant).

## What your assistant can do

| Area | Examples |
| --- | --- |
| Pages | Create a page from a template, a brief, or a copy. Edit sections. Publish after you agree. Restore an older version. |
| Store | Create products and coupons. Read and update orders. Read checkout and shipping settings. |
| Leads | Read form submissions and change their status. Build forms. |
| Insights | Read traffic, revenue, and tracking setup for a period. |
| Domains | Check a subdomain. Connect and verify a custom domain. |
| Search | `search` and `fetch` across pages, products, and forms. |

Tools that change data ask for your approval in the client. Page edits go to the draft. The live page changes only after `publish_page`.

**Too many tools for your client?** Send the header `X-MCP-Toolsets` with the groups you need, for example `pages,sections,search`. Send `X-MCP-Readonly: true` to list only the tools that read data.

## Safety

- The connector cannot move money, change bank accounts, or read payment keys.
- The connector does not generate images with AI.
- Each connection uses the permissions you choose on the Biver consent screen: view, or view and change, for each group.
- Disconnect at any time: Biver dashboard, **API Keys**, **Connected apps**.

## Repository contents

| File | Purpose |
| --- | --- |
| `.claude-plugin/`, `.mcp.json`, `skills/` | Claude Code plugin and marketplace |
| `.cursor-plugin/plugin.json`, `mcp.json` | Cursor plugin |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `server.json` | Official MCP Registry entry (`id.biver/biver`) |
| `llms-install.md` | Install notes for agents such as Cline |

## Bahasa Indonesia

Biver adalah landing page builder untuk UMKM, freelancer, dan agency di Indonesia. Dengan repo ini, asisten AI Anda bisa membuat halaman, mengubah section, mengelola produk dan pesanan, membaca lead, dan membaca traffic.

Masuk dengan akun Biver lewat browser. Pilih workspace, pilih izin untuk tiap kelompok, lalu pilih **Izinkan**. Panduan lengkap ada di [biver.id/docs/mcp-ai-assistant](https://biver.id/docs/mcp-ai-assistant).

## Support

Write to [support@biver.id](mailto:support@biver.id).

## License

[MIT](LICENSE). Product names belong to their owners. Their mention is not an endorsement.
