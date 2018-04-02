---
layout: post
title: "Advancing Disaggregation Through P4 Runtime Integration"
date: 2018-04-02
author: "Nitin Kumar"
category: p4
header-img: assets/p4-background.png
---

    
*Editor's note: This guest post by Nitin Kumar (Juniper Networks) describes a next-generation control APIs based on P4 Runtime. It was originally published on the [New Network blog](https://forums.juniper.net/t5/The-New-Network/Juniper-Advancing-Disaggregation-Through-P4-Runtime-Integration/ba-p/319195) and is republished here with permission.*

---    
<br />
    
It’s a bit of an understatement to say that networking and distributed computing IT infrastructures are undergoing change. It’s fairly easy to point to well-entrenched trends like disaggregation, software-defined networking (SDN), and DevOps and understand that the fundamental ways in which infrastructure is architected, deployed, and operated are evolving faster than ever before. But what is driving all of the change?
 
In a word: control. Yes, these advances in technology allow greater performance or automated operations. But the baseline driver of all of this is control.
 
### Why control matters
Control manifests itself in lots of different ways within IT, ranging from packet manipulation to procurement.
 
Most technical people will immediately leap to network control. Advances like SDN grant greater control over network traffic. Google’s Espresso architecture, announced in 2017, is a great example. In April 2017, Google estimated that 20% of its traffic to the internet at the time was being managed by Espresso, an SDN architecture that allowed programmable and application-aware control extended to the peering edge.
 
But the power of control extends beyond traffic manipulation. The disaggregation of networking allows for things like white box network elements, which grant a greater degree of economic control to companies looking to maximize their purchasing power. When abstraction allows for simpler substitution of components, it stokes competition - which benefits consumers. For example, the rise of P4 as an abstraction layer above the network silicon level means that packet processing can be more easily extended beyond what has become an incumbent-dominated space. When there is a single switching silicon provider, the market dynamics go one way. When abstraction opens up that market to new players, competition drives those market dynamics a different way. And in the end, consumers get control.
 
The notion of control also plays into how much influence users have over roadmaps. In networking, for instance, companies have historically been extremely dependent on vendor roadmaps and resourcing. By disaggregating the technology stack to allow for external integration, users get some measure of control over what features they have access to and when those features become available. Facebook’s recent Open/R announcement is a good example of where standard interfaces that allow for off-box development allow for a different level of partnership between users and suppliers of networking technology.
 
Whether it’s control over packets, control over pricing or control over functionality, a major force behind change in networking today is control.
 
### Juniper and P4
Juniper has adopted P4 as the language that describes the contract between the control plane and the data plane of switches and routers. Juniper has also implemented the P4 Runtime across the portfolio as an open data plane programming API. Inside a Juniper switch or router, all programmatic access to the silicon is made across a forwarding abstraction layer called AFI (Abstract Forwarding Interface). This API layer provides programmatic access to ASICs for Juniper’s own control plane (Junos), as well as third-party control planes (such as an SDN Controller). The figure below gives an overview of an AFI system.
 
<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/juniper-large-1.png" alt="AFI system architecture" width="600" /><strong>Figure 1: AFI system architecture.</strong></p>
 
The AFT Interface provides the following three kinds of interfaces to its clients:
* **Nodes** to represent the packet path as a graph
* **Packet IO** to receive and transmit packets
* **Telemetry** to read counters associated with different nodes in the forwarding graph
 
Details regarding AFI can be found online [here](https://forums.juniper.net/t5/Automation-Programmability/Juniper-Forwarding-Interface/ba-p/310823).
 
### Integration with SDN Controller
An SDN Controller requires the following southbound interfaces to manage the networking devices
* Management Interface to control the chassis functions of the device. This utilizes OpenConfig over a GNMI transport.
* FIB management to program forwarding state, like lookup tables. This is P4 over a P4 runtime transport. The Juniper P4 agent provides the P4 Runtime implementation on the device. The P4 Agent handles the P4 Runtime RPCs and uses the AFI API to program the FIB state in the ASICs.
 
This is shown in the diagram below:
 
<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/juniper-large-2.png" alt="SDN controller integration" width="600" /><strong>Figure 2: SDN controller integration.</strong></p>
     
A few interesting things happen because of this implementation:
* The device is completely managed via standards based interfaces (OpenConfig, P4).
* The architecture applies uniformly to devices across different ASIC families that Juniper provides, with AFI absorbing the differences in ASIC capabilities.
* Well-defined interfaces enable the use of virtual platforms allowing easy co-development in lab environments, accelerating development.
* The P4 Agent is sufficiently decoupled from the on-box operating system and its development can move at a different trajectory than the OS. A new version of the agent can be tested and released without having to requalify the base OS.
 
### The importance of ubiquity
From a Juniper perspective, ubiquity was an important consideration. By supporting a P4 agent across the entire portfolio—ranging from the highest-end platforms to virtualized form factors—Juniper has allowed for ubiquitous control. And by making both the OS and the agent common, the integration burden is minimized, allowing for easy portability across different platforms. This is especially important as the switching silicon market heats up with new entrants optimizing around everything - from cost to scale to programmability.
 
### The value of end-to-end
When the networking industry talks about end-to-end, it’s typically in the context of network architecture. But the value of end-to-end is more than just a statement of how packets flow.
 
Where networking has traditionally been device-and-architecture led (meaning decisions and operations begin with the device or architecture), the cloud evolution has been largely operations-led. The need to drive certain operational practices in support of global user needs has provided the base set of functional requirements that filter down into architectural and device considerations. For instance, dynamic control requires real-time telemetry and standard APIs. This influences how architectures are conceived and ultimately which devices are suitable.  
 
In an operations-led environment, the architectural considerations extend well beyond packet forwarding and manipulation. Users have to consider end-to-end lifecycle management, as well. This means designing explicitly for how functionality is implemented, tested and deployed.  
 
### The role of open
When functionality is off-box, the line between vendor and consumer is blurred. The distinction between developer and user is less stark. Overlaps develop between roles and these overlaps can be the opportunities for streamlining both time and money.
 
For example, should a vendor and a user both have to execute the same tests because of an opaque boundary between the two? If end-to-end is defined within a vendor or user domain, then this kind of overlap is impossible to avoid. But what if end-to-end was recast from an overarching position that included both? Clearly, the process could be streamlined. But this requires a degree of transparency that traditional product development models do not support.
 
In this project, Juniper is leaning on the principles of open and open source. By keeping the P4 agent code in a transparent environment, two things become possible.
 
First, the developer need not reside on one or the other side of the vendor-user boundary. This means, of course, greater control. Second, if the testing and tooling environment is shared, there is an opportunity to use modern development and deployment tools more typically associated with continuous integration and delivery (CI/CD) to rapidly develop, test and deploy networking functionality.
 
### Rethinking what is possible
In the short term, Juniper is proving the viability of P4 as a useful abstraction in a production environment. Minimally, this should enable a more vibrant silicon ecosystem and functionality moves from fixed to programmable pipelines. This can bring economic and innovation advantages to the industry at large.
 
More broadly, this effort highlights the changing nature of how products are developed and delivered to market. Combining the P4 work with other notable disaggregation efforts—such as Open/R and Juniper’s AFT—the entire development model becomes far more open and transparent, capable of leveraging ideas and resources from across a much more expansive pool of talent.
 
This should make possible the sharing of transformative ideas, not just within a particular vendor but across communities of interest in key technology spaces. It’s more than just open source; it’s about applying thoughtful separation of key components to facilitate a distributed development model.
 
Extending this philosophy into the open source world and thinking about lifecycle management more holistically means that companies will be able to concentrate their resources on difference-making activities. How much collective effort is wasted in overlapping spaces simply because processes are not transparent? And what happens when this waste is eradicated?
 
It’s not inconceivable to imagine a not-far-off future where devices are merely containers for functionality that is completely disaggregated. This could lead to new functionality in days and weeks rather than quarters and years, led by automated integration testing leveraged across a much richer ecosystem than today.

