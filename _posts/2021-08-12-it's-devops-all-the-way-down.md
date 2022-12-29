---
publish: true
title: It's DevOps all the way down
filename: 2021-08-12-it's-devops-all-the-way-down
excerpt: DevOps teams can't own a vertical slice of your entire stack, the
  cognative load is too great. We instead need to thing about layered DevOps
  teams each owning their horizontal slice of the stack.
header:
  og_image: /assets/images/DevOps wardley map.png
tags:
  - devops
  - platform-teams
  - organisational-design
---

One of the more memorable phrases of the DevOps movement is Amazon CTO Werner Vogel’s [2006 statement](https://queue.acm.org/detail.cfm?id=1142065): ‘You build it, you run it’. As definitions of DevOps go, its clarity and measurability have made it foundational to DevOps transformations ever since. Like many DevOps principles it emphasises decentralisation and autonomy, favouring cross-functional teams owning a solution end-to-end over the choreographed dance of functional teams. But how much can a team really ‘run it’ given the cognitive load on a typical engineering team?

Often, the reality is that no matter how thinly we slice a modern product, that slice turns out to contain a very deep tech stack. Under our team’s microservice, might be open-source application server, in a container, on Kubernetes, on Linux, on a virtual machine, in a public IaaS cloud. Do we expect our team to be Kubernetes administrators?

This isn’t DevOps — it’s kitbashing a whole IT department into a team. We need to shift our thinking from seeing DevOps accountability as a vertical slice of everything to being a horizontal layer. Modern software is built on [platforms](https://teamtopologies.com/), which are in turn built on other platforms, and so on. These platforms pull toil from the teams they serve; commoditising, outsourcing, or investing in tooling to automate it out of existence, creating more time for our team to invest in value adding work for competitive advantage. It’s what unlocks accelerating rates of cheap innovation as we stand on the shoulders of others, but the abstraction also drives increasing complexity into the stack.

![DevOps wardley map.png](../assets/images/DevOps%20wardley%20map.png)

Fortunately for our team, complexity gets packaged up as a service and increasingly commoditised by the layers below. If we lay this out on a [Wardley map](https://medium.com/ingeniouslysimple/map-camp-2019-37545bb3dcb4), there’s a chain of dependencies on underlying platforms and the teams that deliver them. Crucially, each of these platform teams is also a DevOps team responsible for delivery of their slice of the overall tech stack as a service. Each one is ideally guided by the [four key metrics](https://medium.com/ingeniouslysimple/forget-dumb-productivity-measures-focus-on-software-delivery-performance-with-the-four-key-3ad0e045e5b8) covering both development and operational delivery of their layer. It’s DevOps all the way down.

![DevOps four key metrics.png](../assets/images/DevOps%20four%20key%20metrics.png)

At Redgate we started investing seriously in our platform layer in 2019, to underpin a business transformation from highly decoupled product teams to an integrated enterprise-ready portfolio. As we’ve journeyed from initial concepts to portfolio re-platforming, we’ve had to consider how to adapt our dev and ops organisational structure to make the transition to production. This is complicated by the breadth of our product portfolio, meaning the platform has to target on-premise, SaaS, and our internal systems.

![Layered DevOps.png](../assets/images/Layered%20DevOps.png)

Organisationally, we can unpack the internal platform to a platform group consisting of three teams that, amongst other things, play a significant platform role (remembering that in practice [abstractions like this are leaky](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)). We have a team that releases environment specific distributions of the platform based on our shared reference architecture and tech stack, we have a team that operates production instances of those distributions, and we have a team that delivers shared services running on those platforms.

![Platform group.png](../assets/images/Platform%20group.png)

Each of these teams _is_ a DevOps team, for some their output might be mostly code, for others their output might be mostly infrastructure, but the job isn’t finished by throwing that work over the fence to the next team — the measure of a team is how their work runs in the production environment.

   