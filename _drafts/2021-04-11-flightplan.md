---
layout: post
title: "Flightplan: Dataplane Disaggregation and Placement for P4 Programs"
date: 2021-04-10
author: "Nik Sultana"
category: p4
header-img: assets/p4-background.png
---

## Introduction
The [Flightplan](https://flightplan.cis.upenn.edu/) project envisages
the next generation of dataplane programming tools.
It introduces the *Dataplane Disaggregation* problem---splitting up dataplane
programs into program pieces that are mapped to run on different, possibly
heterogeneous, network-connected hardware.
The choice of splits and hardware is done to optimize network and application
objectives beyond what could be achieved than if the original, monolithic
program were mapped to a single dataplane target.
The project also provides a design to solve this problem and evaluates a
prototype implementation for P4 programs.

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="https://flightplan.cis.upenn.edu/outline.png" alt="Main stages when deploying a Flightplanned program." width="500" /><strong>Figure 1: There are three main stages when deploying Flightplanned programs: (1) Splitting the program's logic, (2) Mapping to hardware according to the needs of each split and its contribution to system-level objectives, (3) Configuring, starting and monitoring the distributed dataplane program. The original dataplane program is disaggregated across several physical dataplane targets.</strong></p>


## Why Dataplane Disaggregation matters
Under current tooling, dataplane programs are mapped to single dataplane targets, one-to-one.
This has the undesirable consequence of coupling a program with the kind of target it can run on:
all of the resources or features needed by the program must be provided by the single target that it's mapped to.
This is undesirable because it burdens programmers with concerns beyond the program they are writing, requiring them to be aware of where the program will be executed.
Even if we assume that the programmer knows about the deployment setting, what if the entire program cannot be mapped to a desired target, such as a switch ASIC, because of the target's restricted computational abilities?
Opting for a more expressive target, such as a CPU, might not be possible because of the loosened bandwidth and latency expectations that would entail.
The one-to-one mapping places undesirable constraints on dataplane programs and their programmers.

By disaggregating the dataplane program we can run programs that cannot run
*entirely* on a single target, or cannot run at the desired performance.
Disaggregation turns the program into a distributed system that uses a range
of possibly-heterogeneous dataplane targets---including those offering more
computability and those offering more performance.
But how do we go about it?


## Why Dataplane Disaggregation is difficult
A programmer *could* manually adapt a dataplane program to have parts of it run
on suitable hardware, but this is laborious and error-prone.
This is made more difficult by the range of splits and mappings that the
programmer would need to explore.
This exploration is needed to determine whether disaggregation can help meet
objectives, and *which* disaggregation to use.

The programmer would need to reason about: the P4 program's resource needs,
resources made available by different targets, typical workloads to which the
program would be applied on those hardware targets, and how all of these
affect system-level objectives such as bounds on throughput and power use.
Since they're deriving a distributed system, the programmer also needs to
reason about combinations of partial and transient failures that can arise.
Moreover this effort must be redone if the available hardware changes.
And as we saw earlier, it burdens the programmer with knowing about the
specifics of target hardware.
The Flightplan paper [characterises Dataplane Disaggregation in more detail](https://flightplan.cis.upenn.edu/flightplan.pdf#section.2)
based on a detailed example in the form of [Crosspod.p4](https://github.com/eniac/Flightplan/blob/45bbe38e0bbcc13f7cdee738a95f53b20a3953a0/Wharf/splits2/ALV_Complete_1_hl3_unsplit/ALV_Complete_hl3_unsplit.p4#L359).

Dataplane Disaggregation is made difficult by the reasoning it entails---involving diverse information and several possible choices.
But it seems to be the type of "difficult" that can be mitigated by support from suitable tooling.
This tooling would reduce programmer burden by automating some of that reasoning and choice-exploration.
And by exploring a range of deployment options,
it would loosen the coupling between development-time and operations-time concerns and relax the need for programmers to have precise knowledge of deployment hardware and its loading.


## How does Flightplan work?
Flightplan provides a solution to the Dataplane Disaggregation problem.
Ultimately after using Flightplan the user will end up with a set of P4 programs, one for each target dataplane, each of which can be put through vendors' toolchains to program their hardware under the current one-to-one tooling.

Flightplan provides tools that:

* [analyse](https://flightplan.cis.upenn.edu/flightplan.pdf#subsection.4.1) P4 code to extract its flows and resource usage, and [split](https://flightplan.cis.upenn.edu/flightplan.pdf#subsection.6.4) it into segment-seperate P4 programs ([code](https://github.com/eniac/Flightplan/tree/master/flightplan)). Programmers need to annotate **segment** boundaries, as shown below (Figure 2). Segments provide the finest offloading granularity that Flightplan will consider.


* [generate plans](https://flightplan.cis.upenn.edu/flightplan.pdf#section.6) describing on which targets the different program parts could be executed, and how that allocation is expected to affect system-level objectives ([code](https://github.com/eniac/Flightplan/tree/master/flightplanner)). Flightplan can merge segments where this improves on objectives and if permitted by available hardware resources.

* [manage](https://flightplan.cis.upenn.edu/flightplan.pdf#section.5) running Flightplanned programs ([code](https://github.com/eniac/Flightplan/blob/master/Wharf/fpctl.py)), including [in-program runtime support](https://flightplan.cis.upenn.edu/flightplan.pdf#subsection.5.2) ([code](https://github.com/eniac/Flightplan/blob/master/Wharf/Sources/FPRuntime.p4)).

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="https://flightplan.cis.upenn.edu/highlightedsnippet.png" alt="(Code snippet)" width="500" /><strong>Figure 2: Example snippet of annotated Flightplan program, taken from <a href="https://github.com/eniac/Flightplan/blob/45bbe38e0bbcc13f7cdee738a95f53b20a3953a0/Wharf/splits2/ALV_Complete_1_hl3_unsplit/ALV_Complete_hl3_unsplit.p4#L359">Crosspod.p4</a>, showing segment annotations and resource-related program phrases.</strong></p>

Using these tools you start with an annotated monolithic P4 program, such as that shown above (Figure 2).
The monolithic program is reduced to [rules](https://flightplan.cis.upenn.edu/flightplan.pdf#subsection.4.1) that the planner will use in its analysis. This reduction is done automatically ([example output](https://github.com/eniac/Flightplan/blob/master/flightplan/analyser_scripts/flightplan_output/program20.json#L13)) by the code analyser---P4 programmers don't have to write rules.
The planner ingests these rules together with a
[device description](https://github.com/eniac/Flightplan/blob/45bbe38e0bbcc13f7cdee738a95f53b20a3953a0/flightplanner/examples/devices.json),
[topology description](https://github.com/eniac/Flightplan/blob/45bbe38e0bbcc13f7cdee738a95f53b20a3953a0/flightplanner/examples/network_tofino.json),
a [profile of resources]( https://github.com/eniac/Flightplan/blob/45bbe38e0bbcc13f7cdee738a95f53b20a3953a0/flightplanner/examples/performance_tclust.json),
and system-level [objectives](https://github.com/eniac/Flightplan/blob/master/flightplanner/planner_config.json#L36)---these are provided by the "operations" side of the organisation, without needing to involve the programmer.
From these, Flightplan produces plans that descibe an
allocation model ([example](https://github.com/eniac/Flightplan/blob/master/flightplanner/examples/program20/max_perf/stdout#L24))
and a possibly-coarsened segmentation ([example](https://github.com/eniac/Flightplan/blob/master/flightplanner/examples/program20/max_perf/stdout#L318)).
The program is split according to this segmentation to produce one P4 program for each target dataplane.
These can then be compiled and deployed using the current one-to-one paradigm.


## Evaluation and practical aspects

**Won't Dataplane Disaggregation incur latency?**
<br />
It depends: everything else being equal, adding extra dataplane hops would increase latency, but because of hetereogeneous hardware (and low-latency targets in particular) and workload distributions you can actually see a lowering of latency.
This can be seen for Memcached GETs in the graph below (Figure 3). The graph shows the measurement response to the incremental activation of parts of a disaggregated program and adding external loss to simulate corruption.
The Flightplan paper contains much more [evaluation detail](https://flightplan.cis.upenn.edu/flightplan.pdf#section.7).

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="https://flightplan.cis.upenn.edu/gradualactivation.png" alt="" width="500" /><strong>Figure 3: Measurements over disaggregated Crosspod.p4, appearing in the <a href="https://flightplan.cis.upenn.edu/flightplan.pdf#figure.caption.17">Flightplan's paper Figure 10</a> which details the graph's layout and contents. In outline, the graph shows the incremental activation of parts of the distributed program and how this affects system behaviour and measurements.</strong></p>

**Won't Dataplane Disaggregation incur network overhead?**
<br />
This depends on segmentation and workload.
In the case where the workload exercises several parts of the distributed system, you incur network overhead for two reasons: i) intermediate (cross-dataplane) traffic being put on the network, and ii) metadata overhead of the computation's context (e.g., variables' values synchronized across dataplanes).
The Flightplan prototype provides different runtime and tuning options, and the paper provides a [detailed analysis of overhead](https://flightplan.cis.upenn.edu/flightplan.pdf#subsubsection.7.1.3).
Even if this kind of overhead cannot be eliminated in all cases, it can be tuned to obtain a finer trade-off between disaggregation benefits against overhead.

**How do I start a Flightplan-disaggregated program?**
<br />
Use **fpctl**---the [control program](https://flightplan.cis.upenn.edu/flightplan.pdf#subsection.5.1) ([code](https://github.com/eniac/Flightplan/blob/master/Wharf/fpctl.py))---to configure, start and stop the system. It can also be used for [property testing](https://github.com/eniac/Flightplan/blob/master/Wharf/splits/ALV_split1/step2.sh) during routine checks or diagnosis.

**What if my program, network topology, or hardware change?**
<br />
Update the relevant description (program, topology, hardware catalogue) that's input to Flightplan, and rerun to obtain fresh plans.

**What if part of the distributed program becomes unresponsive?**
<br />
Flightplan's [runtime support](https://flightplan.cis.upenn.edu/flightplan.pdf#section.5) allows you to configure detection, tolerance, and action to take, in both the data- and control-plane.

**Can I only run a single disaggregated program in my network?**
<br />
You can run [several](https://flightplan.cis.upenn.edu/flightplan.pdf#figure.caption.13) disaggregated programs and they can interoperate. These can include different versions of the same program (e.g., to phase-in new program versions).


## Finding out more
In addition to the prototype's code and example programs, the
[repo](https://github.com/eniac/Flightplan) contains a host of other reusable
systems such as our experiment and measurement setup, and our network config
generator.
All of this is provided under a permissive license and can be cannibalised to
support your research or products.

The [Flightplan site](https://flightplan.cis.upenn.edu/) links to several
resources that can help understand how the system and its components work.
These resources include our
[online demo](https://flightplan.cis.upenn.edu/demo/),
[paper](https://flightplan.cis.upenn.edu/flightplan.pdf) and
accompanying [short video](https://flightplan.cis.upenn.edu/nsdi21_video).
