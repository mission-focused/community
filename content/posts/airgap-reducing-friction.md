---
title: 'Delivering Cloud Native Software to Disconnected Environments'
date: '2025-05-08T10:00:00Z'
# weight: 1
# aliases: ["/first"]
tags: ["Airgap", "Cloud-Native", "Airgap-Chapter-2"]
author: "Brandt Keller"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Reducing friction at the edge"
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
    image: "https://content.bekindchooseviolence.com/airgap-friction-reduction.png" # image path/url
    alt: "Reducing airgap friction" # alt text
    caption: "Delivering Cloud Native Software to Disconnected Environments" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/mission-focused/community/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

![](https://content.bekindchooseviolence.com/airgap-friction-reduction.png)

We’ve talked about **personas**.  
We’ve talked about **environments**.  
Now we need to talk about **delivery**.

Because for all the advances in containerization, infrastructure as code, and supply chain security—getting software to run in disconnected or semi-connected environments is still far too hard.

And the reasons why come down to friction.

## Disconnection Isn’t New—But Our Tooling Assumes It Is

Disconnected systems have existed for decades: industrial control networks, classified enclaves, and remote field operations. What’s changed is the **expectation** that these environments should run modern, cloud-native applications—and the **tooling** that assumes a persistent cloud connection to do so.

What we often see in practice is one of two failure modes:

1. **Disconnection isn’t supported at all.**  
   The system assumes public registry access, cloud-based identity, and SaaS integrations.

2. **Disconnection is supported—but barely.**  
   The process involves pages of manual steps, brittle one-off scripts, and hidden assumptions that break easily.

In both cases, **friction is the enemy**—friction that turns an otherwise well-architected system into a support nightmare when pushed beyond its comfort zone.

## The Four Layers of Friction

Delivering cloud-native software to disconnected environments isn’t just about pushing a container image. It’s about reducing friction across **four interlocking layers**:

---

### 1. **Delivery: How the Software Gets There**

Disconnected environments can’t `docker pull`. They can’t `helm repo add`. They may not even have a reliable sync mechanism.

So every artifact—container images, manifests, charts, policies—needs to be:

- **Bundled ahead of time**, with complete dependency trees.
- **Signed and tamper-proof**, to meet supply chain security requirements.
- **Auditable**, so operators can trace exactly what’s being delivered.

Friction here looks like:

- Custom export scripts with implicit dependencies.
- Separate packaging for software vs. metadata.
- Inconsistent or manual artifact verification processes.

---

### 2. **Operation: How the Software Runs Once Delivered**

In cloud-connected environments, applications expect dynamic configuration via APIs, instant logs via observability backends, and auth via identity providers.

In disconnected environments, none of that is guaranteed.

Your software must:

- **Run offline**, with no dependency on real-time APIs.
- **Be observable locally**, or queue telemetry for later upload.
- **Support resilient identity models**, like pre-baked service tokens or hardware-based attestation.

If the system falls apart without internet, it’s not a good fit for the edge.

---

### 3. **Transparency: How the System Proves What It’s Doing**

Disconnected doesn’t mean unregulated. In fact, **many of the most disconnected environments are also the most controlled**—like classified enclaves or critical infrastructure.

Transparency is key:

- What software is running?
- What was delivered?
- What changed, and when?

This isn’t just about logs—it’s about **compliance**, **audits**, and **approvals**.

Friction shows up as:

- Unverifiable config drift.
- Manual SBOM generation.
- Opaque pipelines that obscure provenance.

---

### 4. **Infrastructure Support: How the Environment Enables It All**

Your application can be perfectly packaged and secure—but if the platform underneath it can’t support disaster recovery, resiliency, or degraded operations **without cloud APIs**, it doesn’t matter.

Disconnected infrastructure must:

- **Fail gracefully**, with local fallback logic.
- **Recover autonomously**, without calling home.
- **Support backup and rehydration workflows** natively.

A reliable disconnected platform treats cloud APIs as enhancements—not dependencies.

---

## Friction Is a Design Smell

When delivering to the edge feels like pulling teeth, it’s a signal:  
**The system was not designed with disconnection in mind.**

But this isn’t just about edge use cases. These principles benefit connected environments, too:

- Prepackaging software helps speed up recovery in cloud outages.
- Local observability makes systems more resilient under load.
- Stronger provenance and transparency improve trust and auditability across the board.

Designing for disconnection **doesn’t limit capability**—it sharpens it.

## The Path Forward

To serve the growing class of disconnected and semi-connected environments, we need to:

- **Simplify software delivery** with repeatable, declarative bundles.
- **Ensure offline-first operation** without breaking cloud-native patterns.
- **Embed supply chain metadata** as a first-class citizen in the packaging process.
- **Design platforms that don’t assume connectivity** as a precondition for resiliency.

Because disconnection isn’t the exception anymore.  
It’s an emerging norm.

And our software delivery workflows need to catch up.

## Want to go deeper?

- Check out the [Zarf project](https://github.com/zarf-dev/zarf) for building packages that run across the spectrum
- Join the `#zarf` channel in Kubernetes Slack
- Or hit me up on socials to chat about the weirdest places you’ve deployed an app