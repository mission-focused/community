---
title: 'How Airgaps Shape Tech Choices'
date: '2025-04-29T03:25:50Z'
# weight: 1
# aliases: ["/first"]
tags: ["Airgap", "Cloud-Native"]
author: "Brandt Keller"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: true
hidemeta: false
comments: false
description: "How Airgapped environments shape technology choices"
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "How Airgapped environments shape technology choices" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/mission-focused/community/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

When you operate in an airgapped or semi-connected environment, technology decisions stop being theoretical.

It is no longer about which tools are shiny.  
It is about which ones will **actually work when the internet is gone**.

Airgap constraints force sharper decisions at every layer of the stack.  
And the truth is, many of the most popular cloud native tools are not built with disconnection in mind.

Let's walk through what changes.

## No runtime dependencies allowed

In connected environments, it is easy to let applications depend on:

- Pulling container images dynamically
- Fetching libraries or packages at startup
- Live access to cloud APIs (identity, storage, telemetry)
- SaaS-based Git, secrets, and monitoring systems

In an airgapped environment, every runtime dependency must already exist inside the boundary.  
There is no second chance to fetch something you forgot.

That forces two big shifts:

- **Preload everything** — container images, binaries, data sets, charts
- **Use self-contained solutions** — local Git servers, internal registries, bundled manifests

If a tool cannot operate without a live pull from the internet, it is out of consideration.

## Packaging is a first-class concern

If you cannot stream it from a service, you have to **package it** yourself.

That changes how you evaluate tools:

- Can you export a full, versioned package of this application?
- Can you carry dependencies inside the artifact?
- Does the tool have built-in airgap support (like Helm chart fetchers, OCI bundles, etc)?
- Can you create reproducible installs without internet access?

If the answer is no, you will spend more time duct-taping workarounds than running your system.

**Tools like Zarf, Helm, Kustomize, and GitOps with mirrors** become critical because they allow you to shape a complete, transportable unit of deployment.

## Self-hosted > SaaS (almost always)

SaaS offerings are fast and easy to spin up when the cloud is available.

But in airgapped or controlled-connected environments, you have to think differently:

| SaaS Dependency         | Airgap Reality                |
|--------------------------|-------------------------------|
| GitHub Actions           | Local CI/CD runner             |
| Vault in the cloud       | Local Vault instance or sealed secrets |
| DataDog/New Relic        | Self-hosted Prometheus, Loki, Jaeger |
| S3 storage               | MinIO or artifact storage inside the fence |

The goal is not to reject SaaS forever.  
The goal is to **have autonomy inside the boundary** when it is required.

If your system assumes live access to SaaS for normal operation, it is fragile.

## Tool choice becomes survival, not preference

In an always-connected cloud, you can pick tools based on developer experience, ecosystem buzz, or familiarity.

In disconnected environments, the selection criteria change:

- **Portability** — Can it be fully exported and carried?
- **Determinism** — Does it behave the same way every time, independent of connection status?
- **Operability** — Can it be installed, managed, and upgraded without external control planes?
- **Observability** — Does it produce usable metrics and logs locally?
- **Updatability** — Can it evolve incrementally without a full re-install?

If a tool cannot answer yes to most of these, it becomes a risk, not a feature.

## Summary

> Airgap environments do not just stress-test your system. They stress-test your toolchain.

When the network is unreliable, slow, controlled, or missing altogether, you find out very quickly which tools were built for the real world—and which ones were only built for always-on cloud assumptions.

Choosing technology through the lens of airgap forces clarity:

- What does this tool actually depend on?
- Can I control and audit those dependencies?
- Can I install, operate, and update it without outside help?

If you build with those questions first, you will not just survive in disconnected environments—you will build systems that are **stronger everywhere**.

---

## Want to dig deeper?

- Check out [Zarf](https://github.com/zarf-dev/zarf) for airgap-native packaging
- Explore tools like MinIO, ArgoCD, Fluxcd,  K3s, Harbor, and Loki that work well across the spectrum
- Join the `#zarf` channel in Kubernetes Slack to trade notes on building local-first cloud native systems
