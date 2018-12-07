---
layout: post
title: "Member Spotlight: Netcope"
date: 2018-12-14
author: "P4.org"
category: members
header-img: assets/p4-background.png
---

<center><img alt="Netcope logo" src="{{ site.baseurl }}/assets/netcope-logo.png" /></center>
    
*Editor's note: This post is a part of our "member spotlight" series
that highlights the P4-related activities of various [P4 Language
Consortium][p4] members. It is based on an interview with Netcope's
CTO [Viktor Puš](https://twitter.com/viktorpus/).

# Please tell us a bit about Netcope.

[Netcope][netcope] is a group of FPGA enthusiasts on a mission to
bring the performance and power efficiency of FPGAs to developers who
are not FPGA experts. Netcope’s main product is a cloud-hosted
P4-to-FPGA compiler that enables [P4][p4] developers to run their code
efficiently on a variety of FPGA platforms including 10/25/40/100 Gbps
smart NICs and embedded architectures.

# Can you tell us more about your P4 product?

The Netcope [P4][p4] compiler is a cloud service with an easy-to-use
web interface. To compile a [P4][p4] program, the user simply uploads
their code and selects a hardware target. When synthesis completes,
the user downloads the generated bitstream, and loads it onto the
FPGA. That's it! They get fully custom packet processing at line rate
and interoperability with existing control planes via a P4 Runtime
management interface.

# What was Netcope's motivation for joining the P4 Language Consortium?

When we started working on a [P4][p4] compiler backend for FPGAs, it
was natural for us to join the consortium and work with other members
to deliver programmability across as many hardware targets as
possible.

# What are some of the benefits you see for increased network programmability?

We believe that putting network architects in charge of the data plane
rather than vendors is a game changer for the networking industry. The
innovation cycle gets shorter and the lifetime of hardware is
increased, since it can be easily repurposed for different
applications. In addition, there are new use cases that are being
enabled by programmability of forwarding plane, such as inband network
telemetry.

# How is Netcope involved with P4 community efforts?

Netcope continues to work closely with the [P4][p4] community. Our
primary effort is to demonstrate various use cases using
[P4][p4]-programmable FPGA platforms and contribute code of such use
case to the community. Netcope is also a regular attendee and sponsor
of [P4][p4] workshops. During the last [P4 workshop in May
2018][p4-workshop-2018], Netcope participated in three different demos
showing the great flexibility and fitness of [P4][p4] to different use
cases including server-side segment routing, [OvS][ovs] acceleration,
and inband network telemetry.

[p4]: https://p4.org
[p4-workshop-2018]: https://p4.org/events/2018-06-05-p4-workshop/
[ovs]: https://www.openvswitch.org/
