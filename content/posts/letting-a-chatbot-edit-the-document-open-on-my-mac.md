---
title: "Letting a Chatbot Edit an Open Word Document"
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

Ask a chatbot to fix one sentence in a document, and you often end up doing the moving yourself: copy the text into a chat, paste the answer back, and repair the formatting. Asking it to rewrite the whole file creates a different chore: checking what else changed.

I wanted the edit to happen where I was already writing.

With [WordCraft](https://getartcraft.com/apps/wordcraft), it can. In a simple test, I asked ChatGPT to add a Chinese seven-character quatrain to the end of an open document. The four lines appeared in the editor, with no file export or copy-and-paste step.

![ChatGPT conversation requesting a seven-character quatrain and confirming the edit](https://pub-0ca7268f5327450bb58d14ef32e91b39.r2.dev/2026/10/clipboard-87cd1f.png)

![WordCraft document with a four-line Chinese poem added at the end](https://pub-0ca7268f5327450bb58d14ef32e91b39.r2.dev/2026/10/clipboard-a82e9b.png)

*The poem was added directly to the open document.*

## Why WordCraft works

[WordCraft is open source](https://github.com/storytold/wordcraft) and can read and write Word (DOCX) files. Its menus, shortcuts, and external tools use the same document-editing commands. Those commands are also available through the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/), which lets an AI application use tools provided by another program.

This gives a chatbot a way to inspect the open document and make a targeted edit. It no longer needs to return a replacement file for every change.

## Connect a local AI agent

Start WordCraft with its [local control channel](https://github.com/storytold/wordcraft/blob/main/docs/control-protocol.md):

```sh
wordcraft --control 7981
```

A terminal-based agent on the same computer can connect through `wordcraft-cli`. For example, with Claude Code:

```sh
claude mcp add wordcraft-app -- wordcraft-cli mcp --connect 127.0.0.1:7981
```

The control channel listens on the computer itself, so no public address is needed.

## Connect a browser chatbot

ChatGPT and other browser chatbots need a secure web address for the tool server. The connection looks like this:

```text
Browser chatbot
      |
Cloudflare Access (sign-in)
      |
Cloudflare Tunnel (secure route)
      |
mcp-proxy (web-to-local bridge)
      |
wordcraft-cli
      |
WordCraft (open document)
```

First, use [mcp-proxy](https://github.com/sparfenyuk/mcp-proxy) to make the local MCP tools available over HTTP. The example below keeps the service on the local computer:

```sh
uvx mcp-proxy --port 8765 -- wordcraft-cli mcp --connect 127.0.0.1:7981
```

Next, create a [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/) that routes a hostname you control to `http://127.0.0.1:8765`. The tunnel gives the chatbot an HTTPS address without opening an inbound port on your computer.

Protect that hostname with a [Cloudflare Access policy](https://developers.cloudflare.com/cloudflare-one/access-controls/policies/). Allow only the intended account, then enable [Managed OAuth](https://developers.cloudflare.com/cloudflare-one/access-controls/applications/http-apps/managed-oauth/) so the chatbot can sign in. Set the permitted redirect addresses for your client. In this test, the ChatGPT redirect pattern was `https://chatgpt.com/*`.

Check that the endpoint rejects requests without sign-in:

```sh
curl -i -X POST https://docs.example.com/mcp
```

The response should have status `401 Unauthorized`. Replace `docs.example.com` with your own hostname.

Finally, add a custom MCP connector in the chatbot, using `https://docs.example.com/mcp` and OAuth authentication. After signing in through Cloudflare, you can ask the chatbot to edit the document already open in WordCraft.

A small change should be a small change. The document can stay in the editor, and so can your attention.

## Update: Claude Docs

The setup in this post already looks like a workaround. Claude now has a built-in document editor, [Claude Docs](https://claude.com/blog/cowork-is-now-claude): ask for a document in any conversation, and Claude drafts it on screen, asks clarifying questions, and leaves comments explaining its choices. You edit the text directly or ask for another pass, and the result lives at a shareable link. Claude Docs launched in beta on September 16, 2026, and on October 8 it [left beta and reached every plan, including Free](https://support.claude.com/en/articles/12138966-release-notes).

![Claude's "Make something new" menu: Docs, Slides, Design, and a Dashboard in beta](https://pub-0ca7268f5327450bb58d14ef32e91b39.r2.dev/2026/10/clipboard-ae873c.png)

Claude Docs is an AI-native Word: the document is born inside the chatbot instead of being connected to one afterwards through MCP. Yet it still [exports to Word and PDF](https://support.claude.com/en/articles/16923645-get-started-with-claude-docs), which is telling. The DOCX file survives because other people expect one. What is less clear is why I would open Word to write. If drafting, editing, and sharing happen where the AI already is, Word becomes a file format rather than a place to work.
