---
title: "Letting a Chatbot Edit the Word Document Open on your Device"
date: 2026-10-13
author: Yongkang Yang
draft: false
tags:
  - AI
  - MCP
  - Writing
categories:
  - Technology
---

Most AI writing help takes one of two routes. The first runs through the clipboard: you copy a paragraph into a chat window, copy the answer back, and repair the formatting that broke on the way. The second hands over the whole file: the model returns a new version, and you are left working out what it changed.

Both are poor at small adjustments. Fixing one sentence or one heading should not mean a round trip through a chat window or a rewritten file.

This week I connected a word processor on my Mac to the AI tools I already use. I select a heading, type "write a Chinese poem and put it underneath," and it appears in the document instantly. Nothing else in the file moves. see an example below:

![A WordCraft window showing a short test document with a four-line Chinese poem at the end](https://pub-0ca7268f5327450bb58d14ef32e91b39.r2.dev/2026/10/clipboard-a82e9b.png)

*The poem at the bottom was written into the open document by ChatGPT.*

![A ChatGPT conversation: a request for a seven-character quatrain at the end of the document, and the reply confirming it was added](https://pub-0ca7268f5327450bb58d14ef32e91b39.r2.dev/2026/10/clipboard-87cd1f.png)

## An editor built to be driven

The editor is [WordCraft](https://getartcraft.com/apps/wordcraft), an [open-source](https://github.com/storytold/wordcraft) word processor written in Rust that reads and writes .docx files. Every action in it is a command with an id, and the same commands drive the ribbon, the keyboard shortcuts, a command-line tool and an [MCP](https://modelcontextprotocol.io/) server. MCP, the Model Context Protocol, is the common standard that lets AI applications call external tools.

## How to connect your word tab to a cloud agent

A local MCP server talks to programs on the same machine. A coding agent in a terminal can start it directly. A chatbot in a browser cannot, because its tool calls come from the provider's servers, and those need a public HTTPS address.

The stack has four pieces:

| Piece | Tool | Job |
|---|---|---|
| Editor | WordCraft and `wordcraft-cli` | Exposes the open document as MCP tools |
| Bridge | [mcp-proxy](https://github.com/sparfenyuk/mcp-proxy) | Turns the local server into an HTTP endpoint |
| Tunnel | [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/) | Gives that endpoint a public hostname, with no open port |
| Gate | Cloudflare Access | Admits one account and handles the OAuth sign-in |

## The steps

Start the app with its [control channel](https://github.com/storytold/wordcraft/blob/main/docs/control-protocol.md), which listens on the local machine only:

```sh
wordcraft --control 7981
```

A terminal agent on the same machine needs nothing more. For Claude Code:

```sh
claude mcp add wordcraft-app -- wordcraft-cli mcp --connect 127.0.0.1:7981
```

For browser chatbots, run the bridge. By default it also listens only on the machine itself:

```sh
uvx mcp-proxy --port 8765 -- wordcraft-cli mcp --connect 127.0.0.1:7981
```

Create a tunnel in Cloudflare, route a hostname on your own domain to `http://127.0.0.1:8765`, and run the connector:

```sh
cloudflared tunnel run --token-file ~/.cloudflared/tunnel.token
```

Before the hostname goes live, put an Access application in front of it. Give it a [policy](https://developers.cloudflare.com/cloudflare-one/access-controls/policies/) that allows a single email address, and turn on [Managed OAuth](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/managed-oauth/):

```json
{
  "type": "self_hosted",
  "domain": "docs.example.com",
  "oauth_configuration": {
    "enabled": true,
    "dynamic_client_registration": {
      "enabled": true,
      "allowed_uris": [
        "https://claude.ai/api/mcp/auth_callback",
        "https://chatgpt.com/*"
      ]
    }
  }
}
```

Check the gate before trusting it. A request without credentials should be refused:

```sh
curl -i -X POST https://docs.example.com/mcp
# HTTP/2 401
# www-authenticate: Bearer ... resource_metadata="https://docs.example.com/.well-known/..."
```

Then add a custom connector in the chatbot's settings: a name, the URL ending in `/mcp`, and OAuth as the authentication method. The first connection opens Cloudflare's sign-in page. 

Enjoy!
