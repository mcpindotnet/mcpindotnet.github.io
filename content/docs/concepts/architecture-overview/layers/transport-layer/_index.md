---
weight: 2150
title: "Transport Layer"
description: "Manages communication channels and authentication between clients and servers.It handles connection establishment, message framing, and secure communication between MCP participants.The transport layer abstracts communication details from the protocol layer, enabling the same JSON-RPC 2.0 message format across all transport mechanisms."
icon: "compare_arrows"
date: 2025-08-07T05:30:22+01:00
lastmod: 2025-08-07T05:30:22+01:00
draft: false
images: []
---

Welcome to the Lotus Docs user guide. This guide shows you how to start creating technical documentation sites using Lotus Docs, including site customisation and using Lotus Docs' features and templates.

## What is Lotus Docs?

Lotus Docs is a theme for the [Hugo](https://gohugo.io) static site generator (SSG), specifically designed for technical documentation sets and includes many best practices by default (The site you’re currently reading was built using the Lotus Docs theme!). Use Lotus Docs to get a working and reliable documentation site [up and running]() fast, leaving valuable time to focus on creating content for your users.

### Features

Many of the [features]() and [configurations]() available in the Lotus Docs theme are on display here in this documentation. You can clone this entire site and edit it to suit your projects, or explore the site, its source and see what Lotus Docs can do. Check out a few of Lotus Docs' features:

<div class="row flex-xl-wrap pb-4">

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../features/syntax-highlighting/">
  <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">highlight</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">Syntax Highlighting</p>
        <p class="para card-text mb-0">Highlight your code blocks via PrismJS</p>
      </div>
    </div>
  </a>
</div>

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../guides/landing-page/overview/">
    <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">flight_land</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">Landing Page</p>
        <p class="para card-text mb-0">Customizable landing page and templates</p>
      </div>
    </div>
  </a>
</div>

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../features/docsearch/">
    <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">search</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">DocSearch</p>
        <p class="para card-text mb-0">A powerful Server Side Search plugin</p>
      </div>
    </div>
  </a>
</div>

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../features/plausible-analytics/">
    <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">trending_up</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">Plausible Analytics</p>
        <p class="para card-text mb-0">Open source, Privacy-focused web analytics</p>
      </div>
    </div>
  </a>
</div>

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../shortcodes/">
    <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">code</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">Shortcodes</p>
        <p class="para card-text mb-0">Custom shortcodes for when you want to do more than Markdown can offer</p>
      </div>
    </div>
  </a>
</div>

<div id="list-item" class="col-md-4 col-12 py-2">
  <a class="text-decoration-none text-reset" href="../features/feedback-widget/">
    <div class="card h-100 features feature-full-bg rounded p-4 position-relative overflow-hidden border-1">
      <span class="h1 icon-color">
        <i class="material-icons align-middle">reviews</i>
      </span>
      <div class="card-body p-0 content">
        <p class="fs-5 fw-semibold card-title mb-1">Feedback Widget</p>
        <p class="para card-text mb-0">Collect feedback from your visitors on your site’s content</p>
      </div>
    </div>
  </a>
</div>

</div>

## Who is Lotus Docs for?

Lotus Docs is (currently) suited to small or medium technical documentation sets with 100 or fewer pages of docs. That's not to say Lotus Docs won't scale to larger documentation sets, just that its navigation and site structure may not be sufficient for larger data sets without heavy customisation.

The good news is that development to accommodate such sites is part of the development roadmap. So keep an eye on the [Lotus Docs GitHub repository](https://github.com/colinwilson/lotusdocs) for updates.