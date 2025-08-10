---
weight: 4000
date: "2025-08-07T05:33:22+01:00"
draft: false
author: "Ankit Sarkar"
title: "Understand C# SDK"
icon: "developer_guide"
toc: true
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
description: "Explore C# SDK for building with the Model Context Protocol"
publishdate: "2025-08-07T05:33:22+01:00"
tags: ["Beginners"]
categories: [""]

twitter:
  card: "summary"
  site: "@anktsrkr"
  creator: "@anktsrkr"
  title: "What is Model Context Protocol?"
  description: "Get started with the Model Context Protocol (MCP)"
  image: ""
---
Let's explore the official C# SDK for MCP, which offers a robust set of NuGet packages that empower .NET developers to build applications that seamlessly interact with LLMs. This guide will provide a deep dive into the three core components of the MCP SDK for .NET.

The SDK is structured as a layered architecture with three distinct packages, each serving a specific purpose in the ecosystem:

  1. [ModelContextProtocol.Core](https://www.nuget.org/packages/ModelContextProtocol.Core)
  2. [ModelContextProtocol](https://www.nuget.org/packages/ModelContextProtocol)
  3. [ModelContextProtocol.AspNetCore](https://www.nuget.org/packages/ModelContextProtocol.AspNetCore)

Let's examine each package in detail.
### ModelContextProtocol.Core
#### Overview
ModelContextProtocol.Core is the essential building block of the MCP ecosystem. As the minimal dependency package, it provides the fundamental client and server APIs without the overhead of additional frameworks.

#### When to use this package:

- When you need the absolute minimum dependencies
- For low-level server implementation
- When building lightweight clients
- In constrained environments where dependency count matters
#### Key Features
- Basic client/server communication
- Tool registration and invocation
- Protocol message handling
- STDIO transport implementation

### ModelContextProtocol 
#### Overview
ModelContextProtocol is the primary package for most MCP implementations in .NET. It builds upon the Core package by adding dependency injection, hosting integration, and automatic tool discovery capabilities.

#### When to use this package:
- For standard application development
- When using dependency injection
- When you need automatic tool discovery
- For most server implementations that don't require HTTP
#### Key Features
- Full dependency injection integration
- Automatic tool discovery via attributes
- Advanced server configuration
- Seamless integration with AI functions
- Hosting extensions for background services
### ModelContextProtocol.AspNetCore
#### Overview
ModelContextProtocol.AspNetCore extends the MCP capabilities to HTTP-based communication, allowing you to create MCP servers that operate over standard HTTP protocols.

#### When to use this package:

- When you need HTTP-based MCP servers
- For web-based integrations
- When working with cloud services that require HTTP endpoints
- For scenarios where STDIO isn't appropriate
#### Key Features
- HTTP transport implementation
- ASP.NET Core middleware integration
- Web API endpoint configuration
- Standard HTTP request/response handling
- Compatibility with existing web infrastructure


### Final Thoughts
Want to build a .NET MCP server (console or hosted)? Start with **ModelContextProtocol**.

Building an HTTP-powered MCP server in ASP.NET Core? Use **ModelContextProtocol.AspNetCore**.

Need a lightweight client or minimal integration? Choose **ModelContextProtocol.Core**.

{{< alert context="warning" text="All are in preview! so expect potential breaking changes—but they offer powerful foundations for LLM-tool integration within .NET." />}}

Let's build real world applications using these packages to demonstrate their capabilities.