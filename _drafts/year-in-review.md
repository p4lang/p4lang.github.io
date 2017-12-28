---
layout: post
title: "Year in Review"
date: 2017-12-23
author: "Nate Foster"
category: p4
header-img: assets/p4-background.png
---

As 2017 winds down, we wanted to take a look back and reflect on all
of the progress made by the P4 community over the past year.

## New Version of the P4 Language

In May, the [Language Design Working
Group](https://p4.org/working-groups/) released [version
1.0.0](https://p4.org/p4-spec/docs/P4-16-v1.0.0-spec.html) of the
P4<sub>16</sub> language. P4<sub>16</sub> retains the core features of
the original version of the language, now called P4<sub>14</sub>, and
adds new primitives designed to make it easy to write safe, portable,
and modular data plane programs. See the [blog
post](https://p4.org/technical-steering-committee/get-involved-with-shaping-p4s-future.html)
announcing P4<sub>16</sub> for more details.
 
## Portable Switch Architecture

One of key innovations in P4<sub>16</sub> is the notion of "architecture," which
separates the logical functionality needed to express a given program
from the components used to implement it. In November, the
[Architecture Working Group](https://p4.org/working-groups) released a
[draft specification](https://p4.org/p4-spec/docs/PSA.html) of the
Portable Switch Architecture (PSA). It defines a collection of
portable "extern" primitives as well as a standard packet-processing
pipeline that can be mapped to different underlying hardware and
software targets.

## Flexible Control-Plane API

To date, much of the focus in the P4 community has been on designing
constructs for data plane programming. But in any practical
deployment, P4 programmers will also need to write control-plane
software. In November, the [API Working
Group](https://p4.org/working-groups) announced the initial
implementation of [P4 Runtime](https://github.com/p4lang/PI). It
provides a new way for control plane software to manage a huge variety
of different programmable and fixed-function switches. See the [blog
post](https://p4.org/api/p4-runtime-putting-the-control-plane-in-charge-of-the-forwarding-plane.html)
on P4 Runtime for more details.

## Emerging Applications

As P4 continues to mature, there is growing interest in applications
that change the way people design, build, and run their networks.  To
help nurture a P4 software ecosystem that is well aligned with the
needs of applications, we launched the [Applications Working
Group](https://p4.org/working-groups) in November. The goal of this
working group is to develop specifications and open-source
implementations of novel data plane applications enabled by
P4. Initially, the working group plans to focus on data plane
telemetry but it may broaden its scope to include other applications
as they emerge. See the [blog
post](https://p4.org/members/announcing-the-p4-applications-working-group.html)
announcing the Applications Working Group for more details.

## Community Events

The P4 community came together several times over the past year at these events:
* A [workshop](https://p4.org/events/2017-05-09-p4-workshop/) and [developer day](https://p4.org/events/2017-05-11-p4-developer-day/) at Stanford in May,
* Tutorials at [PLDI](https://pldi17.sigplan.org/track/pldi-2017-workshops-and-tutorials#program), [HotChips](https://www.hotchips.org/archives/2010s/hc29/), and [SIGCOMM](http://conferences.sigcomm.org/sigcomm/2017/tutorial-p4.html),
* A [Developer Day](https://p4.org/events/2017-10-16-p4-developer-day/) at Stanford in November.

## P4 Targets

This year also saw the announcement of several new P4-enabled targets including;

* [Xilinx P4-SDNet](https://forums.xilinx.com/t5/Xcell-Daily-Blog/The-P4-has-landed-SDNet-2017-1-gets-P4-to-FPGA-compilation/ba-p/766361)
* [Barefoot Tofino](https://barefootnetworks.com/technology/)

# Looking Ahead to 2018

In the coming year we are excited to continue growing the momentum
behind P4. We are looking forward to seeing the release of PSA and P4
Runtime, and the development of novel applications built using P4. We
invite you to get involved. If you are not already a member of P4.org,
please [join us](http://p4.org/join-us) and help shape the future of
networking!
