---
layout: post
title: "How P4 Benefits the Router for Academia, Research, and Education (RARE) Project"
category: p4
date: 2020-10-29
header-img: assets/p4-background.png
---

*Editor Note: In this interview, Frédéric Loui discusses how P4 is being used in the GÉANT RARE Project.*

## Introduction ##

The Router for Academia, Research and Education (RARE) project aims to create a full featured router running on open, commodity networking hardware. RARE is being developed under the auspices of [GÉANT](http://www.geant.org/), which is Europe’s leading collaboration on network and related infrastructure and services for research and education. As such, the project focuses on research and education (R&E) institutions as well as national research and education networks (NRENs), which often require features that are not supported by commercial vendors. Another target audience is institutions that want to customize their networks to support new protocols.

Building on an earlier effort that produced [freeRouter](http://freerouter.nop.hu/), an open-source router, the RARE project uses P4 to program the data plane, resulted in a platform that combines an open source IP router with a rich set of additional protocols and advanced features.

## Interview ##

### How does the project fit within the goals of GÉANT? ###
GÉANT is an association whose founding members are from the European Union and around 40 countries in Europe. Within this community, the members have different organizational structures and funding schemes—e.g., some are government-owned companies, some are pure associations, and some can be perceived almost as private companies. 

Each member has a national research and education network (NREN), but the size of those NRENs are different; which means that each member has a different mindset. Some smaller NRENs have a strong do it yourself (DYI) strand in their DNA. They have no choice but to innovate, because if they do not, they will disappear. Other NRENs are larger and have more accountability for delivering strong service level support. So for these NRENs, innovation takes a back seat to network systems that are backed by robust support.

Wearing my GÉANT hat, I strongly feel that RARE is about empowering the NREN users. Nowadays, network innovation is pushed by the over the top (OTT) companies that can embrace new technologies such as WebRTC, Kubernetes and Docker at a level and pace that I have ever seen before.

But keep in mind one important thing, all of these innovative products are sharing the same roots—that is, software code coming from the open source world that originated from research and education (R&E) labs. The Internet (with a capital I) is an example of innovation coming from R&E and academia. IPv6 also!

In a sense, RARE is bringing back innovation into the R&E world, at least from the networking perspective.

### What are the use cases that RARE is developed for? ###
RARE is a platform that aims to provide solutions for a wide variety of R&E use cases, including:

Schools/small office/home office: Since 2004, we have seen a massive move by governments to interconnect schools at all levels just like universities have been connected historically.  Many of these schools don’t have significant budgets, so our vision is that there should be networking equipment that is able to provide the same required features whether it is used to connect a primary school or a core backbone router. Of course the feature set used by each institution will be different, but all these features should be accessible for even the smallest budgets. 

Medium-sized/regional/metropolitan network: In some regions with small budgets, intermediate transit networks are used to connect the schools to an R&E institution for access to their backbone. RARE is designed to be a robust solution for these networks. Some of them might interconnect local data centers. So the solution provided must be versatile in terms of bandwidth capacity supporting speeds from 1 Gbps to 100 Gbps with the entire data center interconnect and provider edge feature set.

Core network: RARE is designed provide N x 100 Gbps core facing link capacity. And N x 10 Gbps for smaller, lower budget networks.

### What is the impact of P4 on this project? ###
The RARE project is possible because of the convergence of various innovative technologies. To be honest, RARE is just an opportunity to "democratize" networking using open source and programmable technologies.

P4 unlocks the door to a hardware data plane that can work at unprecedented traffic rates. Users can now create applications (open source or not) that can work at multiple Tbps traffic rates. In the past, access to this flexible, high-performance data plane was only available from big commercial vendors—and it wasn’t programmable.

The consequence is that the RARE/freeRouter platform that we’ve developed, can power a number of different P4-enabled whitebox switches with performance up to 6.4 Tbps using the Tofino switch – and double that with Tofino 2. This is amazing for the open networking community!

During the [P4 Expert Roundtable Series](https://p4.org/events/2020-p4-summit/) in April, Changhoon Kim, Intel Fellow and CTO of Applications in the Barefoot Switch Division, gave an insightful presentation where he mentioned P4 in 2020 has opened data plane programmability to the user and this is paving the way to new applications powered by a rock-solid P4 data plane. I fully share this vision and I'm pretty sure that data plane programmability will unlock exciting innovative solutions. 

A unique and exciting feature that is a consequence of our design choice is that freeRouter/RARE benefits from a modular data plane. In some use cases we can use Tofino programmable switch ASIC and in other cases we can use P4DPDK. There’s also the BMv2 software switch, but that is mostly used in training of new programmers and for testing out new protocols and applications. 

### Specifically, what does network programmability let you do now that you couldn't do before? ###
P4 allowed us to develop RARE as a "hackable router"—not insecure, but customizable and open to developments by clever programmers. For example, a freeRouter core developer developed two new versions of IGP for an internal network: Path Vector Routing Protocol (PVRP) and Link State Routing Protocol (LSRP). They are both available for freeRouter users.

### When do you use BMv2 vs. Tofino? ###
We initially started working on P4 programming using BMv2. We did our homework and decided not only to understand P4 but we also needed to understand all P4Lang building blocks. Once we had a good understanding of the language and packet processing algorithms, we ported our code to Tofino. So if you look carefully into the RARE GitHub, BMv2 has all the RARE features without any compromises. In fact, I started a RARE blog to publish content such as the blog series called: "P4Lang P4 for dummies." My objective is to give back all the knowledge we acquired from the community to the community.

In Tofino, we have to make sure that all the packet processing algorithm fits into hardware. Obviously, not all algorithms can be compiled to Tofino, but for programs that can be, we know they will run at line rate.  In that context, we introduced the concept of profiles. Each profile has a set of features. For example, why activate MPLS packet processing when you would like to activate SRv6 ? Why activate bridging/NAT/GRE tunneling if you plan to use your P4 box as a pure label switch router?

With the approval of Intel/Barefoot, RARE Tofino code has been open sourced. As I said, RARE is about providing the community a set of solutions that can fit their R&E use cases.

### What is the status of the project? ###
In just 18 months, I consider that we have achieved the following great results:

RARE/freeRouter offers a fantastic set of routing solutions that fit SOHO, MAN, DC/IXP, and WAN R&E use cases. The feature set is incredible and includes OSPF, IS-IS IGP, two custom designed IGPs, PVRPLSRP, MPLS, MPLS/L3VPN, MPLS/L2VPN (Xconnect/VPLS/EVPN), and SR extension to OSPF/IS-IS. Last but not least, it is both IPv4 and IPv6 compliant.

We are now ready to assist anyone that would like to implement our solution. Our idea is to create a RARE community to back up this project.

A lot of work still has to be done, with documentation and knowledge dissemination. The idea is to start implementing the use cases mentioned above and keep on learning as we discover new problems to solve. 

We have a long way to go before reaching “community trust status.” One of the things that would greatly help with collaboration, sharing of ideas, and addressing the R&E use cases would be for those developing on the platform to be able to talk to each other without unnecessary non-disclosure restrictions. 


