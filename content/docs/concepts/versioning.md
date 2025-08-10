---
weight: 2400
title: "Versioning"
description: "Learn about MCP specification versioning"
icon: difference
lead: ""
date: 2025-08-07T05:30:22+01:00
lastmod: 2025-08-07T05:30:22+01:00
draft: false
images: []
keywords: [
  "Model Context Protocol .NET",
  "MCP C# SDK",
  "MCP server in C#",
  "MCP client .NET",
  "build MCP server C#",
  "MCP vs function calling",
  "OpenAI MCP support",
  "DeepMind MCP integration",
  "Copilot MCP",
  "MCP security vulnerabilities",
  "MCP vulnerabilities prompt injection",
  "MCP security audit",
  "latest MCP updates 2025",
  "MCP adoption OpenAI Google DeepMind",
  "how to build an MCP server in C#",
  "step by step MCP C# example",
  "MCP integration .NET Azure Copilot",
  "MCP .NET tutorial 2025",
  "how to create an MCP server in C#",
  "step-by-step guide to Model Context Protocol in .NET",
  "MCP with Semantic Kernel C# tutorial",
  "best way to integrate MCP with Blazor",
  "C# MCP plugin for AI agents",
  "build AI agents in C#",
  "Semantic Kernel agents .NET",
  "LangChain vs Semantic Kernel",
  "C# AI integration",
  "AI agent framework C#",
  "Blazor AI chatbot example",
  "MCP server example code",
  "C# OpenAI integration",
  "AI tools for .NET developers",
  "Vector database integration C#",
  "MCP API server with ASP.NET Core",
  "real-time AI agent communication in C#",
  "Model Context Protocol .NET",
  "MCP .NET",
  "MCP in C#",
  "Semantic Kernel MCP",
  "MCP server .NET",
  "MCP client .NET",
  "MCP for Blazor",
  "Model Context Protocol C# example",
  "MCP agent framework .NET",
  "OpenAI MCP .NET"
]
---

The Model Context Protocol uses string-based version identifiers following the format
`YYYY-MM-DD`, to indicate the last date backwards incompatible changes were made.
## Revisions

Revisions may be marked as:

* **Draft**: in-progress specifications, not yet ready for consumption.
* **Current**: the current protocol version, which is ready for use and may continue to
  receive backwards compatible changes.
* **Final**: past, complete specifications that will not be changed.

The **current** protocol version is  **2025-06-18**.

## Negotiation

Version negotiation happens during
[initialization](/docs/concepts/architecture-overview/layers/data-layer/lifecycle-management/#initialization). Clients and
servers **MAY** support multiple protocol versions simultaneously, but they **MUST**
agree on a single version to use for the session.

The protocol provides appropriate error handling if version negotiation fails, allowing
clients to gracefully terminate connections when they cannot find a version compatible
with the server.