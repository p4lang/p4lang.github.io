---
layout: post
title: "Member Spotlight: Xilinx"
date: 2018-07-30
author: "P4.org"
category: members
header-img: assets/p4-background.png
---

<center><img alt="Xilinx logo" src="{{ site.baseurl }}/assets/exilinx-logo.png" /></center>
    
*Editor's note: This post is the first in a new "member spotlight"
series that will highlight the P4-related activities of various [P4
Language Consortium][p4] members. It is based on an interview with
[Gordon Brebner](https://www.linkedin.com/in/gordonbrebner/), who was
recently awarded the inaugural [P4.org][p4] Service Award for his
contributions to the community as inaugural co-chair of the [P4
Language Design Working Group][ld-wg].*
        
# Please tell us a bit about Xilinx.

[Xilinx][xilinx] pioneered Field Programmable Gate Array (FPGA) technology, and
is the current market leader. As FPGA has evolved, with the embedding
and integration of other programmable functions, [Xilinx][xilinx] has recently
revealed itself as pioneering a new category: Adaptive Compute
Acceleration Platform (ACAP) technology. The important words here are
“programmable”, “adaptive”, and “acceleration”, all key attributes of
[Xilinx][xilinx] products. This resonates with increasing programmability of
networks, at increasingly high speeds.

# What was Xilinx's motivation for joining the P4 Language Consortium?
    
[Xilinx][xilinx] was one of the first companies to join [P4.org][p4]. [Xilinx][xilinx]
already had its [SDNet][sdnet] programming environment (launched as a
product in early 2014), for compiling the [Xilinx Labs][xilinx-labs]-created PX
language to FPGA. PX had a similar level of abstraction to P4 and
indeed a considerable intersection with P4. [Xilinx][xilinx] felt that the value
of [SDNet][sdnet] would be increased if P4 was to become a standard
packet processing language and [Xilinx][xilinx] adopted it, initially alongside
PX and ultimately to replace PX. [Xilinx][xilinx] also felt that its past
experience with PX, including customer feedback, would be of benefit
to active participation in defining and working on the new
[P4.org][p4] activities.

# What are some of the benefits you see for increased network programmability?

[Xilinx][xilinx]'s customer base is primarily in communications (wired and
wireless) and data centers. In these areas, there is an increasing
customer demand for network programmability, whether on the line card,
in the NIC or SmartNIC, or on the network switch.  With [SDNet][sdnet], [Xilinx][xilinx]
is catering for this demand at the packet forwarding and switching
level. Further, especially in NFV appliances and in network-attached
data center functions, this programmability is coupled with
acceleration of programmable L4-L7 and payload processing in the data
fast path.  Beyond the conventional networking markets, [Xilinx][xilinx] also
sees interest in programmable networking more broadly: for example, in
aerospace, defense, and industrial, markets.  Here, customization of
protocols is often important.

# How is Xilinx involved with P4 community efforts?

[Xilinx][xilinx] has been involved in P4 community efforts from the very
beginning.  This started with a presentation and a 100Gb/s rate
demonstration at the first P4 Workshop in June 2015, and has continued
at the subsequent events. As a leader and pioneer with P4, [Xilinx][xilinx] has
contributed to the Developer Days, as well as tutorials at other
high-profile conferences for differing types of experts, such as FPGA,
Hot Chips, and SIGCOMM. Together with Stanford and Cambridge
Universities, [Xilinx][xilinx] has founded the [P4->NetFPGA][p4-netfpga] community, centered
around providing a “big green button” tool flow for compiling P4 to
the NetFPGA SUME platform much used by networking researchers working
on high line-rate systems.  [Xilinx][xilinx] has been part of the [P4 Language
Design Working Group][ld-wg] since its inception, indeed co-chairing
it, and has been following three other [P4 Working Groups][wgs] since
their establishment.  In particular, [Xilinx][xilinx] recently showcased
an Inband Network Telemetry (INT) inter-operability demonstration with
Barefoot Networks at the MWC and OFC conferences, based on the draft
[INT specification][int-spec] from the [P4 Applications Working
Group][app-wg], which [Xilinx][xilinx] has also made contributions to.

# Does Xilinx have any products based on P4?

The May 2017 release of [SDNet][sdnet] included support for
P4<sub>16</sub>, which had just been released. Various improvements
have been made in subsequent releases.  For example, [Xilinx][xilinx]
has recently demonstrated a prototype [Xilinx][xilinx] SmartNIC
platform---comprising NIC card with FPGA, P4 programming environment,
and DPDK runtime software---developed in
[Xilinx-Labs][xilinx-labs]. This is being further developed by
[Xilinx][xilinx] as a new board-level product, to be launched in 2019.

[p4]: https://p4.org
[sdnet]: http://www.xilinx.com/sdnet
[app-wg]: {{ site.baseurl }}/working-groups/#applications-working-group
[ld-wg]: {{ site.baseurl }}/working-groups/#language-design-working-group
[int-spec]: {{ site.baseurl}}/specs/
[xilinx]: https://xilinx.com/
[xilinx-labs]: https://xilinx.com/about/research-labs.html
[p4-netfpga]: https://github.com/NetFPGA/P4-NetFPGA-public/wiki