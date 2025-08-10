---
weight: 2133
title: "Client Features"
description: "Enables servers to ask the client to sample from the host LLM, elicit input from the user, and log messages to the client"
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
MCP also defines primitives that clients can expose. These primitives allow MCP server authors to build richer interactions.

* **Sampling**: Allows servers to request language model completions from the client's AI application. This is useful when servers' authors want access to a language model, but want to stay model independent and not include a language model SDK in their MCP server. They can use the `sampling/complete` method to request a language model completion from the client's AI application.
* **Elicitation**: Allows servers to request additional information from users. This is useful when servers' authors want to get more information from the user, or ask for confirmation of an action. They can use the `elicitation/request` method to request additional information from the user.
* **Roots**:  Roots define filesystem boundaries for server operations, allowing clients to specify which directories servers should focus on.
* **Logging**: Enables servers to send log messages to clients for debugging and monitoring purposes.