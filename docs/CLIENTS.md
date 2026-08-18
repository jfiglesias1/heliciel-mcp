# Connecting from each client

The server is remote and speaks **streamable HTTP** with **OAuth 2.0 + PKCE (S256)**. There is
nothing to install and no local process to run.

```
https://mcp.heliciel.com/mcp
```

You need a Heliciel MCP pass — day, week or month — from
[mecaflux.com](https://www.mecaflux.com/suite/en/Index.php). On first connection a consent
screen asks for your pass key; you paste it once.

> The consent screen is currently in French. It has a single input field: paste your pass key
> and click **Autoriser** (Authorize).

---

## Claude

Install it from the connectors directory — no configuration at all:

**https://claude.ai/directory/connectors/heliciel-propeller-design**

To add it by hand instead: **Settings → Connectors → Add custom connector**, choose the **web**
(remote) option, and give the server URL above.

## ChatGPT

**Settings → Connectors → Add**, then the server URL. ChatGPT renders the interactive 3D viewer
inline in the conversation.

## Mistral Le Chat

**Settings → Connectors → Add a custom MCP connector**, then the server URL.

## VS Code

`.vscode/mcp.json` in your workspace, or the user-level `mcp.json`:

```json
{
  "servers": {
    "heliciel": {
      "type": "http",
      "url": "https://mcp.heliciel.com/mcp"
    }
  }
}
```

VS Code requires the explicit `type` field and uses `servers` as the root key — unlike the
clients below, which infer both.

## Cursor

`~/.cursor/mcp.json`, or `.cursor/mcp.json` in the project:

```json
{
  "mcpServers": {
    "heliciel": {
      "url": "https://mcp.heliciel.com/mcp"
    }
  }
}
```

## Claude Desktop

**Settings → Developer → Edit Config**, in `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "heliciel": {
      "url": "https://mcp.heliciel.com/mcp"
    }
  }
}
```

## Any other MCP client

Point it at the URL above with streamable HTTP. Discovery documents are served, so a client
that implements OAuth discovery finds everything it needs on its own:

- `https://mcp.heliciel.com/.well-known/oauth-protected-resource` (RFC 9728)
- `https://mcp.heliciel.com/.well-known/oauth-authorization-server` (RFC 8414)

The server advertises `client_id_metadata_document_supported`. It does **not** implement dynamic
client registration (RFC 7591) — there is no `registration_endpoint`.

---

## What to expect on first use

**The first call of a session can take up to two and a half minutes.** Each pass gets its own
private Heliciel instance — a real Windows application that may have to start. This happens once
per session; instances are kept pre-warmed when possible.

**Long computations do not block.** Optimizers and sweeps can run for minutes. Past 120 seconds
a tool returns `commande_en_cours` instead of hanging; the assistant then calls
`lire_etat_commande` to follow the milestones — genetic generations with their best fitness,
swept values, map points — and to collect the result when it lands.

**One command at a time.** Within a session, a second tool call while one is running is refused
with an explicit message, not queued. This mirrors the software: Heliciel computes one thing at
a time.

**Your files are temporary.** Exports live in the session folder and are erased when the instance
is recycled. Download links expire after 60 minutes. Retrieve what you want to keep before the
session ends.
