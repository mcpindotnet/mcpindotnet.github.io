---
weight: 2138
title: "Cancellation"
description: "Allows either party to cancel in-progress requests through notification messages"
icon: autostop
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
When a party wants to cancel an in-progress request, it sends a `notifications/cancelled`
notification containing:

* The ID of the request to cancel
* An optional reason string that can be logged or displayed

```json
{
  "jsonrpc": "2.0",
  "method": "notifications/cancelled",
  "params": {
    "requestId": "123",
    "reason": "User requested cancellation"
  }
}
```

## Behavior Requirements

1. Cancellation notifications **MUST** only reference requests that:
   * Were previously issued in the same direction
   * Are believed to still be in-progress
2. The `initialize` request **MUST NOT** be cancelled by clients
3. Receivers of cancellation notifications **SHOULD**:
   * Stop processing the cancelled request
   * Free associated resources
   * Not send a response for the cancelled request
4. Receivers **MAY** ignore cancellation notifications if:
   * The referenced request is unknown
   * Processing has already completed
   * The request cannot be cancelled
5. The sender of the cancellation notification **SHOULD** ignore any response to the
   request that arrives afterward

## Timing Considerations

Due to network latency, cancellation notifications may arrive after request processing
has completed, and potentially after a response has already been sent.

Both parties **MUST** handle these race conditions gracefully:

```mermaid
sequenceDiagram
   participant Client
   participant Server

   Client->>Server: Request (ID: 123)
   Note over Server: Processing starts
   Client--)Server: notifications/cancelled (ID: 123)
   alt
      Note over Server: Processing may have<br/>completed before<br/>cancellation arrives
   else If not completed
      Note over Server: Stop processing
   end
```

## Implementation Notes

* Both parties **SHOULD** log cancellation reasons for debugging
* Application UIs **SHOULD** indicate when cancellation is requested

## Error Handling

Invalid cancellation notifications **SHOULD** be ignored:

* Unknown request IDs
* Already completed requests
* Malformed notifications

This maintains the "fire and forget" nature of notifications while allowing for race
conditions in asynchronous communication.