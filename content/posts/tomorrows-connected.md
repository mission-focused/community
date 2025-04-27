---
title: 'The Airgap Spectrum: Fully Disconnected to Controlled Connected'
date: '2025-04-19T13:00:00Z'
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
description: "Fully Disconnected to Controlled Connected"
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
    image: "https://content.bekindchooseviolence.com/airgap-spectrum.png" # image path/url
    alt: "airgap spectrum" # alt text
    caption: "Fully Disconnected to Controlled Connected" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/mission-focused/community/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

![](https://content.bekindchooseviolence.com/airgap-spectrum.png)

If you’ve heard the word *airgap* and thought “oh, that’s just for submarines,” you’re not wrong — but you’re also missing the bigger picture.

Airgaps aren’t binary. It’s not either full-internet or total-isolation. This may seem counterintuitive to some... Airgap _feels_ pretty binary.

There’s a spectrum here — maybe not all functions or capabilities within your system are airgap-dendent. Understanding where your system lives on this spectrum is key to building something that doesn’t fall over the second a network hiccups.

## What is the airgap spectrum?

Here’s how I usually explain it:

| Tier | Description |
|------|-------------|
| **Fully Disconnected** | No network access at all. No internet. No relay. Think submarines, remote outposts, satellites. |
| **Semi-Connected** | Some form of intermittent access—maybe via a satellite, a physical data drop, or a controlled sync window. Think forward operating bases, offline-first drones, or even industrial SCADA systems. |
| **Controlled Connected** | Internet access exists but is gated through policy, firewalls, or a limited egress path. Think SIPR/NIPR or compliance-heavy enclaves. |
| **Online** | Full internet access. Normal CI/CD pipelines, SaaS services, live GitOps syncs. |

You might move across this spectrum throughout the day.  
Or design a system that can **operate across the full range**, depending on where it's deployed.

## Why does this matter?

Because each tier changes the assumptions you can make.

In a *fully disconnected* system:
- You must bundle everything ahead of time
- You can’t rely on live telemetry or alerts
- There’s no such thing as an emergency patch from the internet

In a *controlled connected* system:
- You might get read access to a registry—but only through a scan-and-approve process
- Your Git repo might be mirrored across a firewall once per day
- You may be able to pull metrics out—but only via manual export

## You have to plan for the worst

If you build for “online” but deploy into “semi-connected,” you’re going to get burned.

But if you build for “fully disconnected,” your system will *still work* in every other tier.

That’s the point.

Start with no assumptions — then add capabilities where you can.  
Don’t start with full SaaS and try to claw your way back to self-reliant. That way lies broken deploys and a lot of guesswork.

I've lived this life - as have many others. There are assumptions about design and architecture that make or break how an application handles environments which may have different requirements or capabilities. 

## Real-world examples

- **A defense app** that runs on both SIPR (controlled) and a tactical kit (fully disconnected)
- **A field-deployed AI pipeline** that syncs new models over a Starlink relay once a week
- **A software demo** that works even if the expo WiFi fails (ask me how I know)

In all of those, it’s the same stack — but built to scale across the spectrum.

## Summary

> The airgap spectrum isn’t about policy — it’s about operational reality.

Connectivity can vary by:
- Region
- Time
- Approval
- Mission
- Physical infrastructure

But the software still has to work.

So treat “connected” as a luxury, not a baseline.  
And design like it might go away at any moment.

Because sometimes… it will.

## Want to go deeper?

- Check out the [Zarf project](https://github.com/zarf-dev/zarf) for building packages that run across the spectrum
- Join the `#zarf` channel in Kubernetes Slack
- Or hit me up on socials to chat about the weirdest places you’ve deployed an app