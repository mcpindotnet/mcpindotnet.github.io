---
weight: 2132
title: "Server Features"
description: "Enables servers to provide core functionality including tools for AI actions, resources for context data, and prompts for interaction templates from and to the client"
icon: dns
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
Servers provide the fundamental building blocks for adding context to language models via MCP. These primitives enable rich interactions between clients, servers, and language models:

* **Prompts**: Pre-defined templates or instructions that guide language model
  interactions
* **Resources**: Structured data or content that provides additional context to the model
* **Tools**: Executable functions that allow models to perform actions or retrieve
  information

Each primitive can be summarized in the following control hierarchy:
{{< table "table-hover" >}}

| Primitive | Control                | Description                                        | Example                         |
| --------- | ---------------------- | -------------------------------------------------- | ------------------------------- |
|📝 **Prompts**   | User-controlled        | Interactive templates invoked by user choice       | Slash commands, menu options    |
|
|📚 **Resources** | Application-controlled | Contextual data attached and managed by the client | File contents, git history      |
|
|🛠️ **Tools**     | Model-controlled       | Functions exposed to the LLM to take actions       | API POST requests, file writing |
{{< /table >}}