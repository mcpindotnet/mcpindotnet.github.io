---
weight: 100
date: "2025-08-07T05:33:22+01:00"
draft: false
author: "Ankit Sarkar"
title: "Introduction"
icon: "bolt"
toc: true
description: "Get started with the Model Context Protocol (MCP)"
publishdate: "2025-08-07T05:33:22+01:00"
twitter:
  card: "summary"
  site: "@anktsrkr"
  creator: "@anktsrkr"
  title: "What is Model Context Protocol?"
  description: "Get started with the Model Context Protocol (MCP)"
  image: ""
---
Imagine giving your AI assistant a passport — a secure, standardized way to travel across your company’s internal systems, access relevant data, and perform tasks with the right permissions. This isn’t science fiction — it’s the **Model Context Protocol (MCP)**.

Here, we’ll break down what MCP is, why it matters, and how you can think of it as a **digital passport for your AI agents** — enabling secure, two-way communication between tools, models, and data sources without the headache of one-off integrations.

 ### ✳️What Is MCP?

The **Model Context Protocol (MCP)** is an open standard that defines how AI-powered tools can securely connect to external data and services. Instead of custom connectors, MCP offers a universal way to expose structured resources, actions, and prompts — all discoverable by any compatible AI client.

In short, MCP turns disconnected systems into plug-and-play context providers, and AI agents into authorized travelers who can request, consume, and interact with that context — all under strict access control.

 ### 🎒 The Passport Analogy: Why It Matters
 
Think of MCP as a passport system for AI:

{{< table "table-hover" >}}
| Real-World Concept | MCP Equivalent | Explanation |
|---------|--------|-----|
| 🌍 **Passport** | AI client identity & access scope | Just as a passport identifies a traveler and indicates their nationality and basic privileges, the AI client in MCP carries verifiable identity metadata and a defined scope of access (e.g., which tools or data it’s allowed to request).
 |
| 🏛️ **Immigration checkpoint** | MCP Server | This acts as the enforcement point—verifying credentials, checking permissions, and applying organizational policies before granting access. Like border control, it decides who gets in, what they can do, and under what conditions.
 |
| 📜 **Visa**  | Authorized Tools, Resources, and Prompts | A visa grants specific permissions (e.g., work, study, duration). Similarly, MCP issues scoped authorizations—specifying which tools the AI can use, which data it can access, and under what contextual constraints (e.g., prompt templates or usage limits).
 |
| 🔎 **Customs declaration**  | Context Request from the AI Agent | When crossing a border, travelers declare what they’re bringing. In MCP, the AI agent declares the context it needs—what data, tools, or external functions it wants to use—enabling transparency and auditability.
 |
| ✈️ **Travel** | Secure, Traceable Communication Across Systems | Just as air travel is monitored and logged, MCP enables secure, encrypted, and auditable communication between the AI and external systems—ensuring every "journey" is traceable and compliant.
 |
{{< /table >}}

### 🧱 MCP Primitives: The Building Blocks
MCP is made up of three core primitives, all exposed by the MCP Server and consumed by an MCP Client:

🧩 **Prompts (User-invoked)**
Think of these as task templates or UI actions — like predefined commands the AI can offer the user (e.g. /summarize-meeting, /fetch-sales-report).

📂 **Resources (Model-readable)**
Structured, relevant chunks of information the AI can access to enhance its output. For example:
 - A database row
 - A document excerpt
 - A list of user preferences

🛠️ **Tools (Model-invoked)**
Executable actions the AI can trigger autonomously — such as:
 - Sending an email
 - Querying a third-party API
 - Creating a Jira ticket

Each of these primitives is advertised by the server and dynamically discovered by the client. You don’t hardcode the connections — the model simply asks for **what’s available**, like scanning the services at a border checkpoint.

So next time you deploy an AI assistant or workig with them, ask yourself:

**Have you stamped its passport?**


