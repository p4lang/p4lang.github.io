---
layout: post
title: "Announcing the P4Runtime v1.0 release"
date: 2019-02-26
author: "Antonin Bas, Waqar Mohsin"
category: p4
header-img: assets/p4-background.png
---

We are delighted to announce the release of [P4Runtime
v1.0.0][p4runtime-spec]. Many thanks to everyone in the P4 API Working Group who
contributed to the specification. The v1.0.0 release includes:
 * RPC service definition: [Protocol Buffers][protobuf] ("Protobuf") files which
   define the format of the messages used to read and write from the data plane
   elements, along with a set of RPCs that can be used to transmit these
   messages between a remote client and server.
 * A comprehensive specification document which describes the semantics of the
   Protobuf messages.

## What is P4Runtime and why was it created?

The P4 programming language has become a popular way to specify and program the
forwarding plane behavior of networking devices. We created the P4Runtime API as
a standard way to control a running P4 forwarding element, for example to add
and delete entries to a switch's forwarding tables. Before the release of
P4Runtime, most P4 forwarding elements were controlled using custom and
proprietary control plane APIs. After all, the P4-language specification
declares the control plane API to be out of scope, leaving programmers and
vendors to come up with their own solution. This led inevitably to a wide
variety of incompatible APIs; control plane applications written for one API are
not portable to other systems, even if the underlying forwarding element is
defined in open, vendor-independent P4.

P4Runtime attempts to solve this problem by defining a **standard**, **open**
and **silicon-independent** (for both programmable and fixed-function devices)
API which enables runtime-control of arbitrary P4 forwarding planes.

P4Runtime is **equally well-suited to remote control planes and local ones**
(with or without RPC). The figure below shows what a typical SDN deployment of
P4Runtime can look like. In this example, the switch Operating System is
[Stratum][stratum], based on Open Networking Linux (ONL).

<center><img alt="P4Runtime with Stratum" width="800" src="{{ site.baseurl }}/assets/p4runtime-v1-blog-post/p4runtime_w_stratum.png" /></center>

P4Runtime is **pipeline-independent**: When new features are added to the P4
forwarding plane, the P4Runtime API does not change; there is no need to
recompile the control plane software (or even reboot it).

To achieve pipeline-independence, P4Runtime decouples the Protobuf interchange
message format from the format of the data carried by these messages, much like
[gNMI][gnmi] defines a fixed gRPC service and fixed Protobuf message
formats which can be used to carry any tree-structured data, often modeled using
YANG. In P4Runtime, the data model is itself described by a Protobuf message,
called P4Info, which is derived from the P4 program. The interface, on the other
hand, is fixed and does not depend on the P4 program, which promotes
extensibility (i.e. introduction of new protocols or actions), and streamlines
client and server implementations.

<center><img alt="P4Runtime messages" width="800" src="{{ site.baseurl }}/assets/p4runtime-v1-blog-post/p4runtime_msgs.png" /></center>

In the table above, the P4Info message (in the middle) is the data model which
dictates the contents of the P4Runtime messages (on the right). For example, in
this specific case, the P4Info entry for table `ipv4_lpm` dictates that every
match entry added to the table must provide properly formatted values for the 2
match fields (`hdr.ipv4.dstAddr` and `hdr.meta.vrf_id`) and must choose from 2
actions (`drop` or `set_nhop`).

## P4Runtime v1.0.0: the result of a collaboration between many industry professionals

The design of P4Runtime started in mid-2016 and picked up momentum in 2017 with
the creation of the P4 API Working Group. Multiple implementations on different
platforms were developed in parallel with the design work, and progress was
showcased at multiple networking events since 2017 such as:
 * In November 2017, Google Cloud, Barefoot Networks and ONF demonstrated the
   first physical network running P4Runtime at the SDN NFV World Congress. You
   can watch the video [here](https://youtu.be/BE_y-Sz0WnQ).
 * In February 2018 at MWC, the ONF showcased a multi-vendor switch fabric
   controlled by their ONOS controller through P4Runtime.
 * In March 2018 at the OCP summit, Google showed a video of a P4Runtime
   implementation running on an ONL-based white-box switch controlled by a
   P4-based SDN controller. You can watch the video
   [here](https://youtu.be/g_aPC1x4_cA?t=7m45s).
 * In November 2018 at ONS Europe and in December 2018 at ONF Connect, the ONF
   showcased a multi-vendor switch fabric controlled by their ONOS controller
   using both P4Runtime and OF-DPA The white-box switches controlled by
   P4Runtime were running the Stratum switch OS.

After two years of design and prototyping work, we are confident that release
1.0.0 of P4Runtime is production-ready. This release comes with strong
backward-compatibility guarantees: all releases from now one will be
backward-compatible with this one, unless the major version number is bumped up
(from 1 to 2). We expect major version bumps to be rare and, following
best-practices for [cloud APIs versioning from Google][api-versioning], the
major version number is encoded in the Protobuf package name to remove the
possibility of version mismatch between client and server, as well as enable
endpoints to support multiple major versions simultaneously should the need
arise.

We pride ourselves in having delivered an unambiguous API, with a comprehensive
specification, to facilitate implementation by control plane application writer
and silicon vendors, and to guarantee interoperability.

## What are some interesting features in P4Runtime?

 * **Master-arbitration**: the P4Runtime interface allows multiple controllers
   to be connected to the P4Runtime server running on the device at the same
   time for redundancy and fault-tolerance. Supporting multiple controllers
   allows having one or more standby controllers, to take over in case the
   master controller goes offline.

 * **Role partitioning**: P4Runtime supports sharding the P4 forwarding plane,
   with a different master controller (and possibly standby controllers) for
   each shard. This enables heterogeneous deployments with a combination of a
   local control plane and one or more remote control plane (e.g. local for L2
   and remote for L3).

 * **Data plane reconfigurability**: the pipeline-independent nature of
   P4Runtime enables "pushing" a completely new forwarding plane (with a
   different P4Info) through the interface itself. This enables the control
   plane to leverage data plane programmability when supported.

 * **Packet IO**: P4Runtime supports streaming packets between the client and
   server thanks to a bi-directional gRPC stream. Arbitrary metadata (as per the
   P4Info) can be attached to packets.

 * **Batching**: P4Runtime supports batching for read and write data at the
   protocol level, which means the client and server can amortize the RPC cost
   in the remote control plane case, and achieve high-throughput. Different
   atomicity modes are supported for write batches, enabling applications to
   leverage advanced capabilities of the network device, such as transactions,
   when available.

 * **Error-reporting**: P4Runtime provides a comprehensive mechanism to report
   error back to the client. Each error report combines a [canonical error
   code][error-codes] and an optional device-specific error code. The
   specification provides detailed guidance on which canonical error code to use
   in every situation, which may be leveraged by the application to take the
   appropriate response in case of error and can facilitate debugging of control
   plane software.

 * **Extensibility to new architectures**: P4Runtime leverages the [`Any`
   protobuf message][any-proto] to support arbitrary vendor-specific
   extensions, which can remain proprietary. New Protobuf messages can be
   defined to configure externs or stream notifications between the server and
   client(s).

## Can P4Runtime and SAI complement each other?

The difference between [SAI][sai] and P4Runtime was explained in a previous
[p4.org blog
post][p4runtime-putting-the-control-plane-in-charge-of-the-forwarding-plane]. SAI
was introduced for local control of switches and, unlike P4Runtime, assumes an
underlying forwarding plane running a fixed set of protocols. SAI's main value
proposition is that by exposing a uniform, vendor-independent, semantic API to
local control plane applications it makes it easy to integrate with standard
protocol stacks such as [FRRouting][frrouting]. The tradeoff is that while SAI
is simpler to use than P4Runtime, it is less extensible.

We believe that SAI and P4Runtime are very complementary. There has already been
good progress in the [flexsai][flexsai] project towards using a P4 description
of the SAI API to create a strong "contract" between the control plane and the
forwarding plane. But flexsai relies on API generation, instead of exposing a
pipeline-independent interface to applications, and does not support RPC
functionality.

We think the complementary nature of SAI and P4Runtime can be taken further, to
introduce the extensibility features of P4Runtime into SAI, and we'd welcome
working with others to make this happen. Please let us know if you are
interested in contributing to such a project.

<center><img alt="P4Runtime with SAI" width="800" src="{{ site.baseurl }}/assets/p4runtime-v1-blog-post/p4runtime_w_SAI.png" /></center>


[p4runtime-spec]: https://p4.org/specs/
[protobuf]: https://developers.google.com/protocol-buffers/
[stratum]: https://stratumproject.org/
[gnmi]: https://github.com/openconfig/gnmi
[api-versioning]: https://cloud.google.com/apis/design/versioning
[error-codes]: https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto
[any-proto]: https://developers.google.com/protocol-buffers/docs/proto3#any
[sai]: https://github.com/opencomputeproject/SAI
[p4runtime-putting-the-control-plane-in-charge-of-the-forwarding-plane]: https://p4.org/api/p4-runtime-putting-the-control-plane-in-charge-of-the-forwarding-plane.html
[frrouting]: https://frrouting.org/
[flexsai]: https://github.com/opencomputeproject/SAI/tree/master/flexsai/p4
