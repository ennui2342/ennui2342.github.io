---
publish: true
title: How to grow your way to enterprise selling
excerpt: Understanding the difference between products, solutions, and enterprise solutions is critical to tierd business models.
header:
  og_image: /assets/images/software tiers.png
---
![skyscrapers at night.jpg](../assets/images/skyscrapers%20at%20night.jpg)

Software companies are strongly motivated to service as much of the [market demand curve](https://en.wikipedia.org/wiki/Demand_curve) as possible, but in practice it's challenging to sell at volume to end-users with a [product-led growth model](https://openviewpartners.com/product-led-growth/), and at the same time sell to enterprises with an [account-based sales model](https://www.drift.com/blog/account-based-selling/). While it's common to see tiered models on SaaS pricing pages, if you look under the hood, the company's commercial organisational design usually results in a clear revenue bias to either low-cost mass-market, or high-cost enterprise sales.

But it's not just the commercial model that can prove a barrier. Product managers are often guilty of treating tiers as feature checklists; the enterprise version is a souped-up version of the standard package. That's like approaching the design of a truck by incrementally adding more features to a car. It misses that the [JTBD](https://strategyn.com/jobs-to-be-done/) has changed, meaning a souped-up car will likely lose out to a competitor who approaches the truck JTBD afresh with [first principles thinking](https://www.techtello.com/first-principles-thinking/). The reality is that feature hierarchies don't evince the experiential difference between mass-market software and enterprise software.

Software architects may express the opinion that the difference is in the technology. Enterprise software is clearly more valuable if it's had more developer time invested, has more sophisticated algorithms and patents at its core, or if it's client-server rather than desktop - each tier is a jump to increasingly sophisticated technology. However, often when you take things apart, the reality is that you find the same technology residing at the heart of each tier. More lines of code and clever infrastructure won't help you sell to more of the demand curve.

So how do we create a tiered offering which genuinely covers the market, from end-user sales all the way to enterprise selling? The answer is hinted at by the language of products, solutions, and enterprise solutions. What do these labels really mean for customers? The best way to understand these concepts is to show rather than tell, so let's explore a fictional story which takes backup as our market opportunity.

# The product era

Backing up is such a common task that it's a verb, and there are many simple and affordable tools to backup everything from filesystems to databases. These products are designed to create value directly for the end user - I have a need at a point in time, I'll grab my tool and make the backup, and then I'm done. At some time in the future, if the worst happens, I'll be able to restore from the backup to save my bacon.

Our fictional company notices a gap in the backup market and launches a command-line tool with a low-friction, product-led growth commercial model. Thanks to our [lean startup](https://theleanstartup.com/) approach and our designers nailing a great user experience, it takes off and we win over thousands of individual users all happily protecting their data with our product. Over time, these users request further functional features like encryption, incremental backups, and operating system support, so we pile on the development and eventually become the dominant tool in our market.

![software tiers product.png](../assets/images/software%20tiers%20product.png)

*Common attributes of the product era*

# The solution era

Sometime later we notice our backup product has made its way into organisations. They seem to use our product differently from our individual users so we send in some researchers who discover that backups are being shared between developers for collaboration, and to send development changes to the operations team for deployment, and operations teams are restoring daily production backups into staging for developers to test against. Crucially, all these new collaborative JTBD are either manually orchestrated processes, or customers are hacking together custom scripting to do all the making, copying and restoring of backup files. 

We notice that our cost of support is rising as users want to do ever more complicated things in their unique environments, and with every release we're in danger of breaking some custom customer workflow we weren't aware of. Our backlog fills with more command-line options and APIs to support these new automation uses, but however complicated the product's feature set gets our product is still, unfortunately, positioned in the customer's mind as a low-cost task-centric tool.

Meanwhile, conversations with technical managers in these organisations increasingly focus on the lack of reliability of all this homegrown scripting in mission-critical processes, the manual bottlenecks and wait times that are slowing down their pace of innovation, and the inefficiency of maintaining their own tooling. The organic spread of the backup tool within their organisation is creating a new JTBD of backup automation, for a new persona - the technical managers.

We switch our development effort to focus on the needs of this new persona. Unlike the end-users they don't request more functional features, instead they're looking for something meta. They want something that works at the organisational level, providing a platform to automate and monitor all their backup pipelines - a backup solution for an organisation.

Emerging from our design conversations comes a need for an asset which indirectly represents a backup - the BackupFile. Much like a VagrantFile or DockerFile, our BackupFile is a declarative representation of the [backup-as-code](https://venturebeat.com/automation/what-everything-as-code-is-and-why-it-matters/) which allows us to shift-left ownership into development and apply standard development practices such as version control, release management, monitoring, testing, and drift detection. We realise that BackupFiles should be the centre of the solution for the technical managers. We package it up, hire a team of [inbound salespeople](https://blog.hubspot.com/sales/inbound-sales-transforming-the-way-you-sell), and start on the road to domination of the mid-market.

![software tiers solution.png](../assets/images/software%20tiers%20solution.png)

*Common attributes of the solution era*

# The enterprise era

With our success in the mid-market, we start to get interest from true enterprise customers. But again we find that the buyer persona has shifted from technical managers to business managers and our salespeople find themselves in losing conversations about risk and compliance.

These enterprises are huge and their data estates are expansive and sprawling. The sheer number of backup files they have is shocking and growing rapidly, each one potentially containing dangerous sensitive data. For the business managers, our backup tool is potentially a disaster waiting to happen, meaning their primary value proposition for an enterprise solution is to deliver them the situational awareness to demonstrate policy compliance. It isn't enough to be able to automate backups at an organisational level, they need to have detailed audit trails to show that the current state of their backups is compliant with organisational policies for access, retention, isolation, inventory, and provenance.

However, an important point to recognise is that while each tier can be defined by a new job for a new persona, the previous tier's personas are also present in the customer and are just as important. In effect there are mass-market personas even in the enterprise scenario - these personas aren't defined as being SMB only. What emerges is the [buyer group](https://www.forbes.com/sites/forbesbusinesscouncil/2020/08/19/four-steps-to-building-a-buyer-group-based-demand-generation-program/) - an enterprise sale needs to win the support of multiple users - the end user who needs to backup, and the technical manager who is automating backup across their organisation, and the business manager who is ensuring the backups are compliant with policy. Product management was much simpler when we just had to please the end user!

The product once again grows to meet the new persona. By auditing the use of BackupFiles and how they change over time, we develop a stateful view of what backups are happening across the customer's entire estate, where data is, and who has access to it. This time the key deliverable is information for situational awareness, meaning a focus on building dashboards, reports, and automated policy checks, to deliver a secure and compliant enterprise backup solution.

We now have total dominance of the backup market with tiered offers for all points of the demand curve... until the next disruption occurs.

![software tiers enterprise solution.png](../assets/images/software%20tiers%20enterprise%20solution.png)

*Common attributes of the enterprise solution era*

# Wrap-up

Of course,  it doesn't always work this way, but you'd be surprised at how common this pattern is once you start looking for it. The reality is, many tools vendors have all the IP they need to grow into selling enterprise solutions (and are often acquired by enterprise vendors for exactly this reason), and many successful enterprise solutions are substantially built around the same core IP as the tools vendor. The fact is that while most companies stay in their lane their whole lives, the organisations that can execute the internal transitions needed to cover the entire demand curve are the ones that end up leading their markets.

![software tiers.png](../assets/images/software%20tiers.png)