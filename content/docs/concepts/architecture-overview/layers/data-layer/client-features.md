---
weight: 2133
title: "Client Features"
description: "Enables servers to ask the client to sample from the host LLM, elicit input from the user, and log messages to the client"
icon: dns
date: 2025-08-07T05:30:22+01:00
lastmod: 2025-08-07T05:30:22+01:00
draft: false
images: []
---
MCP also defines primitives that clients can expose. These primitives allow MCP server authors to build richer interactions.

* **Sampling**: Allows servers to request language model completions from the client's AI application. This is useful when servers' authors want access to a language model, but want to stay model independent and not include a language model SDK in their MCP server. They can use the `sampling/complete` method to request a language model completion from the client's AI application.
* **Elicitation**: Allows servers to request additional information from users. This is useful when servers' authors want to get more information from the user, or ask for confirmation of an action. They can use the `elicitation/request` method to request additional information from the user.
* **Roots**:  Roots define filesystem boundaries for server operations, allowing clients to specify which directories servers should focus on.
* **Logging**: Enables servers to send log messages to clients for debugging and monitoring purposes.