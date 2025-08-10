---
weight: 2136
title: "Completion"
description: "A standardized way for servers to offer
argument autocompletion suggestions for prompts and resource URIs."
icon: auto_awesome_motion
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
Completion in MCP is designed to support interactive user experiences similar to IDE code
completion.

For example, applications may show completion suggestions in a dropdown or popup menu as
users type, with the ability to filter and select from available options.

However, implementations are free to expose completion through any interface pattern that
suits their needs—the protocol itself does not mandate any specific user
interaction model.

## Capabilities

Servers that support completions **MUST** declare the `completions` capability:

```json
{
  "capabilities": {
    "completions": {}
  }
}
```

## Protocol Messages

### Requesting Completions

To get completion suggestions, clients send a `completion/complete` request specifying
what is being completed through a reference type:

**Request:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "completion/complete",
  "params": {
    "ref": {
      "type": "ref/prompt",
      "name": "code_review"
    },
    "argument": {
      "name": "language",
      "value": "py"
    }
  }
}
```

**Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "completion": {
      "values": ["python", "pytorch", "pyside"],
      "total": 10,
      "hasMore": true
    }
  }
}
```

For prompts or URI templates with multiple arguments, clients should include previous completions in the `context.arguments` object to provide context for subsequent requests.

**Request:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "completion/complete",
  "params": {
    "ref": {
      "type": "ref/prompt",
      "name": "code_review"
    },
    "argument": {
      "name": "framework",
      "value": "fla"
    },
    "context": {
      "arguments": {
        "language": "python"
      }
    }
  }
}
```

**Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "completion": {
      "values": ["flask"],
      "total": 1,
      "hasMore": false
    }
  }
}
```

### Reference Types

The protocol supports two types of completion references:
{{< table "table-hover" >}}

| Type           | Description                 | Example                                             |
| -------------- | --------------------------- | --------------------------------------------------- |
| `ref/prompt`   | References a prompt by name | `{"type": "ref/prompt", "name": "code_review"}`     |
|
| `ref/resource` | References a resource URI   | `{"type": "ref/resource", "uri": "file:///{path}"}` |
{{< /table >}}
### Completion Results

Servers return an array of completion values ranked by relevance, with:

* Maximum 100 items per response
* Optional total number of available matches
* Boolean indicating if additional results exist

## Message Flow

```mermaid
sequenceDiagram
    participant Client
    participant Server

    Note over Client: User types argument
    Client->>Server: completion/complete
    Server-->>Client: Completion suggestions

    Note over Client: User continues typing
    Client->>Server: completion/complete
    Server-->>Client: Refined suggestions
```

## Data Types

### CompleteRequest

* `ref`: A `PromptReference` or `ResourceReference`
* `argument`: Object containing:
  * `name`: Argument name
  * `value`: Current value
* `context`: Object containing:
  * `arguments`: A mapping of already-resolved argument names to their values.

### CompleteResult

* `completion`: Object containing:
  * `values`: Array of suggestions (max 100)
  * `total`: Optional total matches
  * `hasMore`: Additional results flag

## Error Handling

Servers **SHOULD** return standard JSON-RPC errors for common failure cases:

* Method not found: `-32601` (Capability not supported)
* Invalid prompt name: `-32602` (Invalid params)
* Missing required arguments: `-32602` (Invalid params)
* Internal errors: `-32603` (Internal error)

## Implementation Considerations

1. Servers **SHOULD**:

   * Return suggestions sorted by relevance
   * Implement fuzzy matching where appropriate
   * Rate limit completion requests
   * Validate all inputs

2. Clients **SHOULD**:
   * Debounce rapid completion requests
   * Cache completion results where appropriate
   * Handle missing or partial results gracefully

## Security

Implementations **MUST**:

* Validate all completion inputs
* Implement appropriate rate limiting
* Control access to sensitive suggestions
* Prevent completion-based information disclosure