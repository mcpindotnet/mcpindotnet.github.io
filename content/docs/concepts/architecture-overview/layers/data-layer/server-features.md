---
weight: 2132
title: "Server Features"
description: "Enables servers to provide core functionality including tools for AI actions, resources for context data, and prompts for interaction templates from and to the client"
icon: dns
date: 2025-08-07T05:30:22+01:00
lastmod: 2025-08-07T05:30:22+01:00
draft: false
images: []
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