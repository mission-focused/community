---
title: 'How Airgaps Shape Tech Choices'
date: '2025-04-30T13:00:00Z'
# weight: 1
# aliases: ["/first"]
tags: ["Airgap", "Cloud-Native"]
author: "Brandt Keller"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
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

When you operate in an airgapped or semi-connected environment, technology decisions stop being expansive. 

It is no longer about which tools are shiny.  
It is about which ones will **actually work when the internet is gone**.

Airgap constraints force sharper decisions at every layer of the stack.  
And the truth is, many of the most popular cloud native tools are not built with disconnection in mind.

Let's walk through what changes.

## No runtime dependencies allowed

In connected environments, it is easy to let applications depend on:

- Pulling container images dynamically (operators)
- Fetching libraries or packages at startup
- Live access to cloud APIs (identity, storage, telemetry)
- SaaS-based Git, secrets, and monitoring systems

In an airgapped environment, every runtime dependency must already exist inside the boundary.  
There is no second chance to fetch something you forgot.

That forces two big shifts:

- **Preload everything** — container images, binaries, data sets, charts
- **Use self-contained solutions** — local Git servers, internal registries, bundled manifests

If a tool cannot operate without a live pull from the internet, it is out of consideration. This is the barrier to entry for these environments 

## Packaging is a first-class concern

If you cannot stream it from a service, you have to **package it** yourself.

That changes how you evaluate tools:

- Can you export a full, versioned package of this application?
- Can you carry dependencies inside the artifact?
- Does the tool have built-in airgap support (like Helm chart fetchers, OCI bundles, etc)?
- Can you create reproducible installs without internet access?
- Can supporting data, such as vulnerability feeds, be updated via imperative means?

If the answer is no, you will spend more time duct-taping workarounds than running your system.

**Tools like Zarf, Helm, Kustomize, and GitOps** become critical because they allow you to shape a complete, transportable unit of deployment.

## Self-hosted Realities

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

If a tool cannot answer yes to most of these, it becomes a risk.

## All is not lost

Cloud Native has made significant strides and communities do exist for collective collaboration and contribution on development and architectural patterns - but we need to have a voice. 

CNCF Technical Advisory Groups (TAG) provide a no-barrier-to-entry group for collaborating on theory and specific areas of importance such as storage, networking, security, etc.

Working Groups provide groups to self-form and autonomy to pursue new and fresh ideas or perspectives on research initiatives from a vendor agnostic perspective. 

User groups such as the [CNCF Public Sector User Group](https://github.com/cncf/public-sector-user-group) enable another group - End users - to collaborate on collective strategy of Cloud native use and how they can share experiences such as disconnected deployments. 

This is only a slice of the CNCF, one of many foundations that exist to enable users, and projects to evolve. 

This evolution only happens **when you get involved** - but because a technology doesn't support disconnected deployments today - doesn't mean it won't forever. The maintainers may have no idea they have built constraints into their systems without feedback

## Summary

> Airgap environments do not just stress-test your system. They stress-test your toolchain.

When the network is unreliable, slow, controlled, or missing altogether, you find out very quickly which tools were built for the resiliency — and which ones were only built for always-on cloud.

Choosing technology through the lens of airgap forces clarity:

- What does this tool actually depend on?
- Can I control and audit those dependencies?
- Can I install, operate, and update it without outside help?

If you build with those questions first, you will not just survive in disconnected environments—you will build systems that are **stronger everywhere**.

**Your voice matters** - get involved in groups that help shape the future rather than hoping someone else does the work for you. 

---

## Want to dig deeper?

- Check out [Zarf](https://github.com/zarf-dev/zarf) for airgap-native packaging
- Explore tools like MinIO, ArgoCD, Fluxcd, K3s, Distribution, and Loki that work well across the spectrum
- Join the `#zarf` channel in Kubernetes Slack to trade notes on building local-first cloud native systems
