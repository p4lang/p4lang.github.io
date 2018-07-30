---
layout: post
title: "NetCache: Balancing Key-Value Stores with Fast In-Network Caching"
date: 2018-07-30
author: "Xin Jin"
category: p4
header-img: assets/p4-background.png
---

*Editor's note: This guest post by [Xin
Jin](https://www.cs.jhu.edu/~xinjin/) (The Johns Hopkins University)
describes a next-generation in-network key-value cache implemented
using P4. It is based on a
[paper](https://dl.acm.org/citation.cfm?id=3132747.3132764) orginally
published at [ACM SOSP ’17](https://www.sigops.org/sosp/sosp17/), the
premier venue for systems research.*
    
## Introduction
    
The emergence of P4 and programmable data planes enables new use
cases, some of which go beyond traditional packet-processing to
application-level functionality. This post presents NetCache, a
next-generation cloud system built with P4 that shows how co-design of
networks and distributed systems can lead to significant performance
benefits.

## What is NetCache?

NetCache is an in-network key-value cache that leverages the power and
flexibility of programmable switches to cache query results and
balance load for frequently-accessed items. Because switches are
optimized for data input-output, they offer orders of magnitude better
performance compared to storage servers, making them an ideal solution
for load balancing and caching. While traditional caches usually
require a high cache hit ratio (>90%) to absorb most queries, NetCache
uses switches primarily for load-balancing, so it provides significant
benefits even with a modest cache hit ratio (<50%). Specifically,
NetCache provides high aggregate throughput and low latency, even
under skewed and rapidly-changing workloads.

## What is the problem?

**Load balancing for performance guarantees.** Key-value stores are a critical building block for large-scale Internet services. As such, they are expected to provide high performance guarantees and meet strict service level agreements (SLAs). Ideally, if the throughput of each storage node is T, a key-value store with N nodes should be able to guarantee an aggregate throughput of N*T. Moreover, if we assume that each node handles no more load than T, then query latency is also bounded. These performance guarantees make it easy for service providers to scale out a storage system to meet specific SLAs.
 
Unfortunately, the skewed, dynamic nature of real-world workloads make
it difficult to provide these guarantees in practice. Popular items
are queried far more often than other items, leading to severe
imbalances—some servers are over-utilized, other servers are
under-utilized, throughput is reduced, and response times suffer due
to long tail latencies.

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/netcache-image1.png" alt="Cache performance analysis" width="500" /><strong>Figure 1: Comparison of different caching approaches. NetCache caches data on programmable switches, which provide orders of magnitude more throughput than in-memory caches.</strong></p>
     
**Load balancing with small, fast caches.** Caching is an effective
technique for addressing load imbalance (Figure 1). Using a
theoretical analysis, one can prove that a cache only needs to store
O(N log N) items to balance the load for a hash-partitioned key-value
cluster with N storage nodes, regardless of the number of key-value
items. As O(N log N) is relatively small, hot items can be replicated
to all cache nodes in order to avoid circular load balancing issues in
the caching layer. To handle skewed workloads, the caching layer must
provide an aggregate throughput comparable to the storage layer. Given
M caching nodes with per-node throughput T', we need M >= N * T /
T’. If T' is close to T, then M would be close to N, which implies
that we would need to build a caching layer with a similar number of
nodes as the storage layer. This has (i) high cost, as it uses too
many caching nodes, and (ii) high overhead, as M nodes must be
modified for each cache update. Therefore, it requires T' >> T—i.e.,
orders of magnitude difference—to build a cost-effective, low-overhead
caching layer.
 
**In-network caching for key-value stores.** In-memory caches are
effective for flash-based and disk-based key-value stores since DRAMs
are orders of magnitude faster than SSDs and HDDs. However, as
key-value stores themselves are being moved to the main memory,
in-memory caches lose their performance advantage and are no longer
effective. Building the caching layer into the network is a natural
solution for balancing in-memory key-value stores (Figure 1). Switches
are optimized for I/O—e.g., current ASICs such as Barefoot Tofino and
Broadcom Tomahawk II are able to process several billion packets per
second. This means that we can build the caching layer with a single
box for high-performance, in-memory key-value stores. Furthermore, if
we use the ToR switch as the cache for a key-value storage rack, it
incurs no latency penalties and no additional hardware costs.

## The design of NetCache

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/netcache-image2.png" alt="NetCache architecture" width="500" /><strong>Figure 2: NetCache architecture.</strong></p>

NetCache leverages in-network caching to provide dynamic load
balancing for key-value storage. NetCache focuses on dedicated,
hash-partitioned key-value storage racks. It uses the ToR switch that
is directly connected to the servers as a load-balancing cache for a
key-value storage rack. Figure 2 shows the architecture overview of a
NetCache storage rack, which consists of a ToR switch, a controller,
and storage servers.
 
**Switch.** The switch is the core component of NetCache. It is responsible for
implementing on-path caching for key-value items and routing packets
using standard L2/L3 protocols. We reserve an L4 port to distinguish
NetCache packets (Figure 2) from other packets. Only NetCache packets
are processed by the NetCache modules in the switch, which makes
NetCache fully compatible with other protocols and functions.
 
**Key-value cache.** The key-value cache module stores the most
frequently-accessed items. Read queries are handled directly by the
switch while write queries are forwarded to the storage servers. Cache
coherence is guaranteed with a light-weight write-through
mechanism. We leverage match-action tables and register arrays to
index, store, and serve key-value items.
 
**Query statistics.** The query statistics module provides key-access
statistics to the controller for cache update. This is critical for
enabling NetCache to handle dynamic workloads where the popularity of
each key changes over time. It contains (i) per-key counters for the
cached items and (ii) a heavy hitter (HH) detector to identify hot
keys that are not present in the cache. The HH detector uses a
Count-Min sketch to report HHs and a Bloom filter to remove duplicate
HH reports, both of which are space-efficient data structures and can
be implemented in programmable switches with minimal hardware
resources.
 
**Controller.** The controller is responsible for updating the cache
with hot items. It receives HH reports from the switch data plane, and
compares them with per-key counters of the items already in the
cache. It then decides which items to insert into the cache and which
ones to evict. Note that the NetCache controller is different from the
network controller in Software-Defined Networking (SDN): the NetCache
controller does not manage network protocols or distributed routing
state. The network operator uses existing mechanisms (e.g., an SDN
controller or a traditional distributed routing protocol) to manage
routing tables and other network functions. The NetCache controller
does not interfere with these existing systems and is only responsible
for managing its own state—i.e., the key-value cache and the query
statistics in the switch data plane. It can reside as a process in the
switch OS or on a remote server as it communicates with the switch
ASIC through a driver in the switch OS. All queries are handled by the
switch and storage servers, so the controller only handles cache
updates and thus is not a performance bottleneck.
 
**Storage servers.** NetCache servers run a simple shim that provide
two important pieces of functionality: (i) mapping NetCache query
packets to API calls for the key-value store; (ii) implementing a
cache coherence mechanism that guarantees consistency between the
caching and storage layers, hiding this complexity from the key-value
stores. This shim layer makes NetCache easy to integrate with existing
in-memory key-value stores.

**Clients.** NetCache provides a client library that applications can
use to access the key-value store. The library provides an interface
similar to existing key-value stores such as Memcached and Redis—i.e.,
Get, Put, and Delete. It translates API calls to NetCache query
packets and also generates replies for applications.

## How well does NetCache perform?

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/netcache-image3.png" alt="System throughput" width="500" /><strong>Figure 3: System throughput.</strong></p>

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/netcache-image4.png" alt="Load on individual servers" width="500" /><strong>Figure 4: Load on individual servers.</strong></p>
    
We have implemented a NetCache prototype with one 6.5 Tbps Barefoot
Tofino switch and multiple commodity servers. Figure 3 shows the
system throughput with read-only queries and 10,000 items in the cache
under several different workloads. In the experiment, we use one
server as a client to generate queries, and use two servers to emulate
a rack of 128 key-value storage servers. We compare NetCache with
NoCache which does not have an in-network cache. In addition, we also
show the portion of the throughput that is provided by NetCache and
the storage servers respectively. We observe that NoCache performs
poorly when the workload is skewed. Specifically, with Zipf 0.95
(0.99) distribution, the NoCache throughput drops down to only 22.5%
(15.6%), compared to the throughput under the uniform workload. By
introducing only a small cache, NetCache effectively reduces the load
imbalances and thus improves the throughput. Figure 4 shows the
throughput breakdown on the individual storage servers when caching is
disabled (top three) and enabled (bottom). NetCache uses the switch
cache to absorb queries on the hottest items and effectively balances
the load on the storage servers.  Overall, NetCache improves the
throughput by 3.6X, 6.5X, and 10X over NoCache, under Zipf 0.9, 0.95
and 0.99, respectively.

## Conclusion

In summary, NetCache is a new key-value store design that provides
billions of queries per second throughput with bounded latency even
under highly-skewed and rapidly-changing workloads. To do this,
NetCache leverages new-generation programmable switches to build an
on-path caching layer to effectively balance the load for the storage
layer and guarantees cache coherence with minimal overhead. We believe
that NetCache is only one example of ultra-high performance
distributed systems enabled by high-speed programmable switches. You
can learn more technical details about NetCache in the
[paper](https://dl.acm.org/citation.cfm?id=3132747.3132764) published
at [ACM SOSP ’17](https://www.sigops.org/sosp/sosp17/).
