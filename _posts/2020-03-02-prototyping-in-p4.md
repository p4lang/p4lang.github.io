---
layout: post
title: "Network Prototyping Made Easy with P4 and Python"
author: "Tomasz Osiński"
category: p4
date: 2020-03-02
header-img: assets/p4-background.png
---

*Editor Note: This post was originally written by Tomasz Osiński for
 his [personal blog](https://osinstom.github.io/en/network-prototyping-p4/). 
 We are re-publishing it here (with permission) as it gives a nice
 introduction to how P4 and Python can be used as rapid prototyping
 tools.*

## Introduction ##

Have you ever tried to understand deeply mechanisms of network
protocols? I mean network protocols used by computer networks like,
for example, Internet Protocol (IP), Transmission Control Protocol
(TCP) or Spanning Tree Protocol (STP). Students are taught at
university how network systems works. Next, they become network
administrators, developers or architects. They know how to configure
network devices, design complex systems or develop network algorithms.
However, it is likely that they got their knowledge from books and/or
administration courses, not from development practice! On the other
hand, I think the best way to understand network paradigms quickly and
deeply is to implement network mechanisms on your own. If as a student
you get the deep knowledge about networking basics, it will be easier
to understand novel technologies in the future. So far, it was
required to use some low-level programming languages (C/C++) with
thousands lines of code to build network’s prototype. And here comes
the P4 technology and Python as a solution to prototype networks in
the easy and fast way! Combining P4 with tools provided by Python such
as the Scapy library or Mininet gives unlimited possibilities to
implement, build and test complex network systems. Moreover, you can
prototype network protocols, which don’t even exist yet!

## P4, Python (Scapy) and Mininet – the toolset of network researcher ##

I assume you know already what the Python language is, but what is P4?
P4 stands for Programming Protocol-Independent Packet Processors. It
has been developed as a next step in the evolution of Software-Defined
Networking (SDN). As you may know, the classical telecommunications
architecture can be divided into data plane, control plane and
management plane. Data plane is the layer, where data packets are
being processed and forwarded, while the control plane decides how
these packets should be handled. **P4 has been designed to enable data
plane programming.** Thus, using the P4 language you can specify which
packet’s headers can be processed and which actions can be performed on
packets. The data plane programming was the missing link in the
software-based network systems, where control plane and management
plane are programmable already. Currently, a network
system can be defined completely using software and its behaviour can
be changed dynamically by updating the software version. It brings a
lot of flexibility to the networking world!

The main component of the P4 ecosystem is the P4 language. It is a
high-level Domain-Specific Language (DSL) dedicated for programming of
network devices. It allows to specify the format of packets
(protocol’s headers) to be recognized by network devices and actions
to be performed on incoming packets (forwarding, headers modification,
adding protocol header, etc). Nevertheless, the P4 language is not
consumed directly by the network device, but it must be compiled to
the source code for particular platform (some target-specific binary). These platforms are
hardware-based (e.g. Barefoot Tofino,
[FPGA](https://p4.org/p4/p4-netfpga-a-low-cost-solution-for-testing-p4-programs-in-hardware.html))
or software-based (e.g.
[BMv2](https://github.com/p4lang/behavioral-model),
[eBPF/XDP](https://github.com/vmware/p4c-xdp),
[PISCES](http://pisces.cs.princeton.edu/) or [P4rt-OVS](https://github.com/Orange-OpenSource/p4rt-ovs)). The goal of P4 is to
become the same what the CUDA language became for graphics cards
programming. The concept of the P4 language has been presented below.

![p4-program-structure.png]({{site.baseurl}}/assets/blog-p4-program-structure.png)

The P4 program is composed of three main sections: Protocols definition
(data declaration), Parser Logic (Parser & Deparser) and a number of
control blocks containing Match-Action tables. The first section
defines the protocols headers that the network device will be able to
recognize. For instance, defining IPv4 header is as simple as:

```
header ipv4_t {
    bit<4>    version;
    bit<4>    ihl;
    bit<8>    diffserv;
    bit<16>   totalLen;
    bit<16>   identification;
    bit<3>    flags;
    bit<13>   fragOffset;
    bit<8>    ttl;
    bit<8>    protocol;
    bit<16>   hdrChecksum;
    bit<32> srcAddr;
    bit<32> dstAddr;
}
```

The programmer just needs to declare header fields and their length.
That’s all. Now, these headers are used to parse incoming data and
recognize type of packets. The Parser Logic is a finite state machine
defining the steps to read and parse incoming packets. Visually, the Parser can be represented
as a cyclic graph, in which every node processes a protocol's header.  

The P4 code implementing the Parser for simple IPv4 router is as follows:

```
parser RouterParser(packet_in packet,
                    out headers hdr,
                    inout metadata meta,
                    inout standard_metadata_t standard_metadata) {
     state start {
         transition parse_ethernet;
     }
     state parse_ethernet {
         packet.extract(hdr.ethernet);
         transition select(hdr.ethernet.etherType) {
             TYPE_IPV4: parse_ipv4;
             default: accept;
          }
     }
     state parse_ipv4 {
         packet.extract(hdr.ipv4);
         transition accept;
     }
}
```

Furthermore, in the P4 program programmer must define a number of control
blocks, which contains Match-Action tables. The definition of simple
IPv4 forwarding table can be implemented as follows:

```
table routing_table {
    key = {
        hdr.ipv4.dstAddr: lpm;
    }
    actions = {
       ipv4_forward;
       drop;
       NoAction;
    }
    default_action = NoAction();
}
```

The above routing_table reads the IPv4 destination IP address and
matches it based on the Longest Prefix Match algorithm. Then, on
packets matching the rule there can be three actions performed:
ipv4_forward, drop or NoAction. 

The last part is to define the Deparser, which defines the order of packet's headers for outgoing packets.

```
control deparser(packet_out packet,
                 in headers hdr) {

    apply {
        packet.emit(hdr.ethernet);
        packet.emit(hdr.ipv4);
    }
}
```

If you would like to view the complete
example of IP router written in P4 visit [my GitHub
repository](https://github.com/osinstom/p4-demos/blob/master/ip-routing/p4include/router.p4).

So, as I pointed out, the P4 language can be used to implement any
type of data plane protocols. Although, [it has some
limitations](https://blogs.vmware.com/research/2017/04/07/programming-networks-p4/)
it is a powerful technology that can be used by network researchers to
prototype and test novel network protocols. Creativity is the limit!
To learn more on P4, let’s visit:

[What P4 programming is and why it’s such a big deal for
Software-Defined
Networking?](https://www.networkworld.com/article/3163496/cloud-computing/what-p4-programming-is-and-why-it-s-such-a-big-deal-for-software-defined-networking.html)

[P4 tutorial – presentation](https://p4.org/assets/P4_tutorial_01_basics.gslide.pdf)

[P4 tutorial from Stanford](https://cs344-stanford.github.io/deliverables/p4-mininet/)

[P4 tutorials – GitHub repo](https://github.com/p4lang/tutorials)

[P4: Programming Protocol-independent Packet Processors](https://www.sigcomm.org/sites/default/files/ccr/papers/2014/July/0000000-0000004.pdf)

Ok, P4 gives the tool to program the data plane, but what about a
control plane? In fact, you can use any language to listen to the
packets being sent from data plane. However, I believe the most simple
to use is Python. It comes with the library named scapy. Scapy allows
you to parse network packets received on sockets as well as construct
new packets as simply as in the below example:

```python
>>> p = IP()/TCP()/"AAAA"
>>> p
>>
>>> p.summary()
'IP / TCP 127.0.0.1:ftp-data > 127.0.0.1:www S / Raw'
```

From my experience Scapy is a user-friendly library that can be used
to implement a control plane applications or generate custom packets
from host devices. More on Scapy library you can read
[here](https://scapy.readthedocs.io/en/latest/introduction.html).

The P4 language allows us to program data plane and Python is the
recommended language to implement control plane of the prototyped
network. Voila! Now, the question is how to emulate the real network
at scale? The BMv2 switch, which is the reference P4 software switch,
is well-integrated with [Mininet](http://mininet.org/). Thus, you can
create a virtual network of any size on your local computer! I have
used Mininet for almost four years to experiment with SDN and OpenFlow
– it is a very powerful tool that make life of network researcher
easier!

## Summary

In this blog post I introduced useful tools for network researchers –
P4, Python (Scapy) and Mininet. These technologies make network
prototyping easier than ever before! P4 allows to program data plane
in tens or hundreds (instead of thousands) of lines of code. Python
comes with Scapy library that simplifies programming operations on
network packets. Finally, Mininet provides the tool to emulate a real
network on your local computer by writing a simple Python script.

### References

[1] W. L. Costa Cordeıro, J. A. Marques, and L. P. Gaspary, “Data Plane Programmability Beyond OpenFlow: Opportunities and Challenges for Network and Service Operations and Management,” J. Netw. Syst. Manage., vol. 25, no. 4, pp. 784–818, Oct. 2017.
