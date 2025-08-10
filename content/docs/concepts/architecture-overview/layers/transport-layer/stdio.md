---
weight: 2151
title: "Stdio transport"
description: "Uses standard input/output streams for direct process communication between local processes on the same machine, providing optimal performance with no network overhead."
icon: terminal
date: 2025-08-07T05:30:22+01:00
lastmod: 2025-08-07T05:30:22+01:00
draft: false
images: []
---

In the **stdio** transport:

1. The client launches the MCP server as a subprocess.
2. The server reads JSON-RPC messages from its standard input (`stdin`) and sends messages
   to its standard output (`stdout`).
3. Messages are individual JSON-RPC requests, notifications, or responses.
4. Messages are delimited by newlines, and **MUST NOT** contain embedded newlines.
5. The server **MAY** write UTF-8 strings to its standard error (`stderr`) for logging
   purposes. Clients **MAY** capture, forward, or ignore this logging.
6. The server **MUST NOT** write anything to its `stdout` that is not a valid MCP message.
7. The client **MUST NOT** write anything to the server's `stdin` that is not a valid MCP message.

```mermaid
sequenceDiagram
    participant Client
    participant Server Process

    Client->>+Server Process: Launch subprocess
    loop Message Exchange
        Client->>Server Process: Write to stdin
        Server Process->>Client: Write to stdout
        Server Process--)Client: Optional logs on stderr
    end
    Client->>Server Process: Close stdin, terminate subprocess
    deactivate Server Process
```

