---
layout: post
title: "P4 Gains Broad Adoption, Joins Open Networking Foundation (ONF) and Linux Foundation (LF) to Accelerate Next Phase of Growth and Innovation"
date: 2018-03-16
author: "P4.org"
category: p4
header-img: assets/p4-background.png
---

* P4 continues to gain rapid adoption and support across the networking industry.

* [P4.org](https://p4.org) currently has more than 100 member organizations spanning industry and academia and continues to grow, adding new members and developers

__San Jose, Calif., March 16, 2018__ -- The P4 Language Consortium ([P4.org](https://p4.org)), creator of the P4 programming language, today announced that it will become a project of the Open Networking Foundation ([ONF](https://www.opennetworking.org/)) and become part of the Linux Foundation ([LF](http://www.linuxfoundation.org/)) portfolio for the purposes of strategic alignment across the open source ecosystem. Since its creation in 2013, P4 has been gaining adoption at an exponential rate, rapidly becoming the standard way to describe how packets are forwarded by networking devices including NICs, switches and routers. To better meet the needs of a growing and vibrant open-source developer community, [P4.org](https://p4.org) is delighted to join forces with ONF and LF -- the two largest open-source umbrella organizations in networking.

“SDN has transformed the networking industry and P4 takes SDN to the next level by bringing programmability to the forwarding plane,” said Guru Parulkar, Executive Director at Open Networking Foundation. “We are excited to have [P4.org](https://p4.org) join ONF and are looking forward to seeing our synergy bring incredible benefits to the P4 and the larger SDN community.”

“Linux Foundation is thrilled to welcome the P4 community,” said Jim Zemlin, Executive Director at Linux Foundation. “Networking is a major focus at the foundation and the addition of the thriving P4 community combined with Linux Foundation Networking Projects in similar domains will drive innovation in networking to the next level.”

The P4 language was originally created by a group of engineers and researchers from Google, Intel, Microsoft Research, Barefoot, Princeton and Stanford. The goal was simple: To create an easy-to-use language that a software developer can learn in a day, and use to precisely describe how packets are forwarded in a network. From the outset, P4 was designed to be target-independent (i.e. a program written in P4 could be compiled, without modification, to run on a variety of targets, such as ASICs, FPGAs, CPUs, NPUs, and GPUs), and protocol-independent (i.e. a P4 program can describe existing standard protocols, or be used to specify innovative, new, customized forwarding behaviors).

“A group of us decided on May 19, 2013 that we needed an industry-standard, open language for specifying forwarding behaviors,” said Nick McKeown, Professor of Computer Science at Stanford University, and P4 Board Member. “We created a language that students are studying in our universities, and using to prototype and publish new research ideas at the best networking conferences. Industry has adopted P4 to program devices and capture existing behaviors. In the future, we hope that Internet RFCs and IEEE Standards will include a clear, unambiguous P4 specification too, paving the way for interoperability by design.”

P4 can be used for both programmable and fixed-function devices alike. For example, it is used to accurately capture the switch pipeline behavior under the Switch Abstraction Interface (SAI) APIs, used by the SONiC open-source switch OS. P4 is also used by the ONF Stratum project to describe forwarding behavior across a variety of fixed and programmable devices.

Describing the forwarding behavior of switch and NIC devices makes it possible, for the first time, to build a packet-accurate, executable model of an entire network prior to deployment. Large cloud providers can test and debug a network entirely in software, greatly reducing the time and expense of interoperability testing in the lab, without requiring expensive hardware.

Using P4, networking equipment vendors, with a broad product offering, can settle upon a common base forwarding behavior across its products, allowing reuse of testing frameworks, making it easier to develop control plane software, and eventually guaranteeing interoperability by design.

P4 can, of course, be used to write programs to describe entirely new packet forwarding behaviors. For example, P4 is widely used for telemetry and measurement in data-centers, enterprise and service-provider networks. For example, the open-source INT.p4 (In-band Network Telemetry), allows fine-grained per-packet measurement to be placed in any location in a packet header.

The research community has stepped up too. Several of the top academic networking research groups have published exciting new applications based on P4 programs, including load-balancing, consensus protocols and key-value caching. As always happens when a new programming paradigm is created, innovation is moved from hardware into software, allowing a multitude of unexpected, novel and ingenious ideas to appear.

The thriving developer community has made significant code contributions spanning compilers, pipeline programs, behavioral models, APIs, test frameworks, applications and much more. Contributions have come from a group of committed developers at companies including Alibaba, AT&T, Barefoot, Cisco, Fox Networks, Google, Intel, IXIA, Juniper Networks, Mellanox, Microsoft, Netcope, Netronome, VMware, Xilinx and ZTE; from universities including BUPT, Cornell, Harvard, MIT, NCTU, Princeton, Stanford, Technion, Tsinghua, UMass, and USI; and Open Source projects including CORD, FD.io, OpenDaylight, ONOS, OvS, SAI, and Stratum, underscoring the fact that P4 is a broad-based independent community-owned project.

### Executive Perspectives

#### Hyperscale Data Centers
“Tencent is at the forefront of using a wide range of innovative technologies to better scale its infrastructure delivering new and exciting services to its customers,” said Tom Bie, Vice President, Technology & Engineering Group at Tencent. “P4 and programmable forwarding planes are examples of cutting-edge technologies we are using in our new network architecture design. As a member of [P4.org](https://p4.org), we are pleased to see the continued growth in P4 community and are looking forward to seeing new breakthroughs come forth as it becomes part of ONF and Linux Foundation.”

“As one of the creators of P4, Google is proud to see the rapid adoption of P4 across the networking industry,” said Amin Vahdat, Engineering Fellow, Vice President and Technical Lead for Networking at Google. “Seeing  [P4.org](https://p4.org) become a project under ONF/Linux Foundation will help the community better scale to meet the needs of a growing set of P4 developers and adopters around the world. Google looks forward to continuing to innovate with P4 technologies on behalf of the community and our customers.”

#### Enterprises
“As a member of ONF and the Linux Foundation, we at Goldman Sachs recognize the benefits of working with the open source community and developing common standards and solutions,” said Joshua Matheus, Managing Director and head of Network Engineering at Goldman Sachs. “We expect that P4 will bring additional innovation and transparency to our networking infrastructure, ultimately helping us deliver better solutions to our clients and the broader developer community.”

#### OEMs
“Our whole networking industry stands to benefit from a language like P4 that unambiguously specifies forwarding behavior, with dividends paid in software developer productivity, hardware interoperability, and furthering of open systems and customer choice,” said Tom Edsall, SVP and CTO, Data Center Networking at Cisco. “These are all values that Cisco has a long history of being committed to – and we endorse initiatives such as this one.”

“Juniper Networks is committed to disaggregation as a natural extension of simple engineering design. We’ve incorporated P4 and P4 Runtime into a number of our products, allowing for uniform programmatic access to both Juniper built and merchant network processing silicon. We believe that programmatic access at all layers in the networking stack will drive flexibility and stokes competition, both of which benefit our customers. We are thrilled to work together with the P4 community to advance open standards for forwarding and control plane architectures as P4 becomes a project under ONF and The Linux Foundation,” said Bikash Koley, CTO & Executive Vice President at Juniper Networks.

“Ruijie is a strong supporter of P4 and the benefits it brings to networking,” said Wang Xiaojun, Software Director of Switch Product Line at Ruijie Networks. “With P4 and programmable forwarding planes we are able to create and deliver best-in-class solutions to a wide range of customers. It is great to see [P4.org](https://p4.org) joining ONF and LF as it will help P4 gain more traction and adoption accelerating innovation in networking.”

#### Service Providers
“AT&T was an early supporter of P4, having been one of the first to use P4 to specify the behavior we want in our networks and using P4’s programmable forwarding plane devices in our network,” said Andre Fuetsch, Chief Technology Officer and President, AT&T Labs. “As one of the operator members at ONF, and as a member of [P4.org](https://p4.org)., we look forward to using and contributing to the synergies created by [P4.org](https://p4.org) joining ONF and Linux Foundation.”

“At Deutsche Telekom we use P4 for prototyping key network functions as part of our Access 4.0 program,” said Jochen Appel, Vice President of Access Network Engineering, Deutsche Telekom. “We are quite excited about the potential P4 holds for driving innovation in the networking space and its role in a growing ecosystem of open programmable hardware and associated programming models.”

#### Semiconductor
“Barefoot is passionate about bringing the power of software to the forwarding plane of the network and P4 has enabled this new paradigm to be possible,” said Craig Barratt, CEO of Barefoot Networks. “[P4.org](https://p4.org) becoming a part of ONF and LF is welcome news to us as this will bolster the P4 community to scale and accelerate to even broader adoption of P4 as the programming language for networking.”

“Xilinx was one of the founding members of [P4.org](https://p4.org), and has taken an active part in the development of the P4 language,” said Salil Raje, SVP of Software and IP Products Group at Xilinx. “We are very enthusiastic about the rapid adoption of P4 across the data center and telecommunications networking industry, and have adopted it in our programmable FPGA-based platforms for SmartNIC and NFV equipment, releasing one of the first P416 compilers as part of our SDNet design environment in 2017.  We are very pleased to see [P4.org](https://p4.org) joining LF and ONF, both noted open source organizations, which will further stimulate the P4 community to evolve and grow.”

#### Software
“P4 is creating massive energy, innovation and community that is driving a meaningful and necessary transformation in networking,” said Pere Monclus, chief technology officer, networking and security business at VMware. “VMware is excited to be a part of this industry movement as a new wave of innovation is unleashed by programmatic approaches that extend capabilities of infrastructure runtime.”

P4 is a target-independent and protocol-independent programming language which is used by industry and academia to unambiguously express packet forwarding behaviour as a P4 program, which in turn can be compiled to multiple targets. Today the targets include hardware and software switches, hypervisor switches, NPUs, GPUs, FPGAs, SmartNICs and ASICs.

### About [P4.org](https://p4.org)
The P4 Language Consortium is a non-profit organization building a thriving open source community dedicated to the use and improvement of the P4 language. It helps promote standardization and improvement of the P4 language and enables participants to develop new technologies that function in accordance with the P4 language specification. [P4.org](https://p4.org) has over 100 members from industry and academia.

### About Linux Foundation
The Linux Foundation is the organization of choice for the world’s top developers and companies to build ecosystems that accelerate open technology development and industry adoption. Together with the worldwide open source community, it is solving the hardest technology problems by creating the largest shared technology investment in history. Founded in 2000, The Linux Foundation today provides tools, training and events to scale any open source project, which together deliver an economic impact not achievable by any one company. More information can be found at [www.linuxfoundation.org](http://www.linuxfoundation.org).

The Linux Foundation has registered trademarks and uses trademarks. For a list of trademarks of The Linux Foundation, please see our trademark usage page: [https://www.linuxfoundation.org/trademark-usage](https://www.linuxfoundation.org/trademark-usage). Linux is a registered trademark of Linus Torvalds.

### About ONF
The Open Networking Foundation (ONF) is an operator led consortium spearheading disruptive network transformation. Now the recognized leader for open source solutions for operators, the ONF first launched in 2011 as the standard bearer for Software Defined Networking (SDN). Led by its operator partners AT&T, China Unicom, Comcast, Deutsche Telekom, Google, NTT Group and Turk Telekom, the ONF has now merged operations with ON.Lab to create a single organization driving vast transformation across the operator space. For further information visit [https://www.opennetworking.org](https://opennetworking.org).

VMware is a registered trademark of VMware, Inc. in the United States and other jurisdictions.

    
    