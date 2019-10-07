---
layout: post
title: "Getting Started with P4"
author: "Bruno Rijsman"
category: p4
header-img: assets/p4-background.png
---

*Editor Note: This post was originally published by Bruno Rijsman on his [personal blog](https://hikingandcoding.wordpress.com/). We are re-publishing it here with permission as it provides an excellent introduction to using the P4 open-source softare tools.*

# Introduction

I recently got serious about learning P4, a programming language for
the data plan in networking devices such as routers, switches, and
Network Interface Cards (NICs).

It took me a while to figure out the exact sequence of steps for
writing a minimal P4 program, compiling it, actually getting it to run
on a simulated software switch, injecting some packets, and observing
how the P4 program forwards the injected packets. To save you the
aggravation of figuring it out for yourself, I’ve documented the
equivalent of “hello world” for P4. 

# Create the server

I will use an Amazon Web Services (AWS) instance to host the P4 switch
and I assume that you already have an AWS account.

Create an AWS t2.large instance running Ubuntu 18.04 LTS and assign it
20GB of disk storage. Smaller instances are not sufficient: they will
run out of disk space and/or out of memory.

Use an SSH client to log in to your newly created AWS instance (here I
use the macOS ssh client). Replace `<private-key>` with the name of your
SSH private key file and replace `<aws-instance>` with the IPv4 address
of your AWS instance.
```
ssh -i ~/.ssh/<private-key> ubuntu@<aws-instance>
```
Once logged in to the AWS instance, update it:
```
sudo apt-get update
```

# Install the P4 compiler

Clone the GitHub repo for the P4 compiler:
```
git clone --recursive https://github.com/p4lang/p4c.git
```
Install the dependencies:
```
sudo apt-get install -y cmake g++ git automake libtool libgc-dev bison flex libfl-dev libgmp-dev libboost-dev libboost-iostreams-dev libboost-graph-dev llvm pkg-config python python-scapy python-ipaddr python-ply tcpdump doxygen graphviz texlive-full
```
Install dependency protobuf 3.2.0 from source code:
```
git clone https://github.com/protocolbuffers/protobuf.git
cd protobuf
git checkout v3.2.0
git submodule update --init --recursive
./autogen.sh
./configure
make
make check
sudo make install
sudo ldconfig
```
In the make step there are some warning (not errors), for example:
```
google/protobuf/compiler/java/java_message_lite.cc:1054:6: warning: ‘bool google::protobuf::compiler::java::{anonymous}::CheckHasBitsForEqualsAndHashCode(const google::protobuf::FieldDescriptor*)’ defined but not used [-Wunused-function]
 bool CheckHasBitsForEqualsAndHashCode(const FieldDescriptor* field) {
      ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```
In the make check step there are also warnings, for example:
```
./google/protobuf/compiler/plugin.pb.h:723:13: error: In the GNU C Library, "minor" is defined
 by <sys/sysmacros.h>. For historical compatibility, it is
 currently defined by <sys/types.h> as well, but we plan to
 remove this soon. To use "minor", include <sys/sysmacros.h>
 directly. If you did not intend to use a system-defined macro
 "minor", you should undefine it after including <sys/types.h>. [-Werror]
 inline ::google::protobuf::int32 Version::minor() const {
             ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  
```
And since warnings are being treated as errors, this causes make check to fail (we ignore this):
```
cc1plus: all warnings being treated as errors
Makefile:3978: recipe for target 'no_warning_test-no_warning_test.o' failed
make[3]: *** [no_warning_test-no_warning_test.o] Error 1
make[3]: Leaving directory '/home/ubuntu/protobuf/src'
Makefile:7666: recipe for target 'check-am' failed
make[2]: *** [check-am] Error 2
make[2]: Leaving directory '/home/ubuntu/protobuf/src'
Makefile:7669: recipe for target 'check' failed
make[1]: *** [check] Error 2
make[1]: Leaving directory '/home/ubuntu/protobuf/src'
Makefile:1384: recipe for target 'check-recursive' failed
make: *** [check-recursive] Error 1
```
Build the P4 compiler:
```
cd ~/p4c
mkdir build
cd build
cmake ..
make -j4
make -j4 check
```
In the make -j4 step, there are some warnings, for example:
```
/home/ubuntu/p4c/ir/type.def: In member function ‘virtual bool IR::Type_InfInt::equiv(const IR::Node&) const’:
/home/ubuntu/p4c/ir/type.def:175:15: warning: unused variable ‘a’ [-Wunused-variable]
```
In the make -j4 check step, multiple test cases fail, for example. The test failures are all related to eBPF, which we will not be using.
```
The following tests FAILED:
	  2 - ebpf-kernel/testdata/p4_16_samples/action_call_ebpf.p4 (Failed)
	  3 - ebpf-kernel/testdata/p4_16_samples/action_call_table_ebpf.p4 (Failed)
	  4 - ebpf-kernel/testdata/p4_16_samples/bool_ebpf.p4 (Failed)
	  5 - ebpf-kernel/testdata/p4_16_samples/count_ebpf.p4 (Failed)
	  6 - ebpf-kernel/testdata/p4_16_samples/hit_ebpf.p4 (Failed)
	  7 - ebpf-kernel/testdata/p4_16_samples/init_ebpf.p4 (Failed)
	  8 - ebpf-kernel/testdata/p4_16_samples/issue870_ebpf.p4 (Failed)
	  9 - ebpf-kernel/testdata/p4_16_samples/key-issue-1020_ebpf.p4 (Failed)
	 10 - ebpf-kernel/testdata/p4_16_samples/key_ebpf.p4 (Failed)
	 11 - ebpf-kernel/testdata/p4_16_samples/lpm_ebpf.p4 (Failed)
	 12 - ebpf-kernel/testdata/p4_16_samples/stack_ebpf.p4 (Failed)
	 13 - ebpf-kernel/testdata/p4_16_samples/switch_ebpf.p4 (Failed)
	 14 - ebpf-kernel/testdata/p4_16_samples/test_ebpf.p4 (Failed)
	 15 - ebpf-kernel/testdata/p4_16_samples/two_ebpf.p4 (Failed)
	 16 - ebpf-kernel/testdata/p4_16_samples/valid_ebpf.p4 (Failed)
	 32 - ebpf/testdata/p4_16_samples/action_call_ebpf.p4 (Failed)
	 33 - ebpf/testdata/p4_16_samples/action_call_table_ebpf.p4 (Failed)
	 34 - ebpf/testdata/p4_16_samples/bool_ebpf.p4 (Failed)
	 35 - ebpf/testdata/p4_16_samples/count_ebpf.p4 (Failed)
	 36 - ebpf/testdata/p4_16_samples/hit_ebpf.p4 (Failed)
	 37 - ebpf/testdata/p4_16_samples/init_ebpf.p4 (Failed)
	 38 - ebpf/testdata/p4_16_samples/issue870_ebpf.p4 (Failed)
	 39 - ebpf/testdata/p4_16_samples/key-issue-1020_ebpf.p4 (Failed)
	 40 - ebpf/testdata/p4_16_samples/key_ebpf.p4 (Failed)
	 41 - ebpf/testdata/p4_16_samples/lpm_ebpf.p4 (Failed)
	 42 - ebpf/testdata/p4_16_samples/stack_ebpf.p4 (Failed)
	 43 - ebpf/testdata/p4_16_samples/switch_ebpf.p4 (Failed)
	 44 - ebpf/testdata/p4_16_samples/test_ebpf.p4 (Failed)
	 45 - ebpf/testdata/p4_16_samples/two_ebpf.p4 (Failed)
	 46 - ebpf/testdata/p4_16_samples/valid_ebpf.p4 (Failed)
```
Install the P4 compiler:
```
sudo make install
```
# Install the P4 software switch

We will now install a P4 software switch to run our P4 program. This
switch is also known as the "behavioral model version 2 (BMV2)" or as
"simple_switch". The P4 architecture file for this switch is
`v1model.p4`.

Clone the P4 behavioral model model GitHub repo:
```
cd
git clone https://github.com/p4lang/behavioral-model.git
```
Install the dependencies:
```
cd behavioral-model
./install_deps.sh
```
Build the software switch:
```
./autogen.sh
./configure
make
```
Install the software switch:
```
sudo make install
sudo ldconfig
```
The steps up until now are pretty time consuming, so it is worthwhile
taking a snapshot of your AWS instance for future P4 projects.

# Write a P4 program

Our minimal P4 program will only process IPv4 over Ethernet packets
and it will contain only a single table that does a
longest-prefix-match lookup on the destination IP address to decide
the outgoing port. That’s it. The focus is not on producing a useful
or interesting P4 program. Instead the focus is on documenting the
steps required to get started with P4 programming.

Create a directory for the P4 program:
```
mkdir ~/test
cd ~/test
```
Use an editor (e.g. vim, which is installed by default on the AWS instance) to create a ~/test/test.p4 program with the following contents:
```
#include <core.p4>
#include <v1model.p4>

typedef bit<48> EthernetAddress;
typedef bit<32> IPv4Address;

header ethernet_t {
    EthernetAddress dst_addr;
    EthernetAddress src_addr;
    bit<16>         ether_type;
}

header ipv4_t {
    bit<4>      version;
    bit<4>      ihl;
    bit<8>      diffserv;
    bit<16>     total_len;
    bit<16>     identification;
    bit<3>      flags;
    bit<13>     frag_offset;
    bit<8>      ttl;
    bit<8>      protocol;
    bit<16>     hdr_checksum;
    IPv4Address src_addr;
    IPv4Address dst_addr;
}

struct headers_t {
    ethernet_t ethernet;
    ipv4_t     ipv4;
}

struct metadata_t {
}

error {
    IPv4IncorrectVersion,
    IPv4OptionsNotSupported
}

parser my_parser(packet_in packet,
                out headers_t hd,
                inout metadata_t meta,
                inout standard_metadata_t standard_meta)
{
    state start {
        packet.extract(hd.ethernet);
        transition select(hd.ethernet.ether_type) {
            0x0800:  parse_ipv4;
            default: accept;
        }
    }

    state parse_ipv4 {
        packet.extract(hd.ipv4);
        verify(hd.ipv4.version == 4w4, error.IPv4IncorrectVersion);
        verify(hd.ipv4.ihl == 4w5, error.IPv4OptionsNotSupported);
        transition accept;
    }    
}

control my_deparser(packet_out packet,
                   in headers_t hdr)
{
    apply {
        packet.emit(hdr.ethernet);
        packet.emit(hdr.ipv4);
    }
}

control my_verify_checksum(inout headers_t hdr,
                         inout metadata_t meta)
{
    apply { }
}

control my_compute_checksum(inout headers_t hdr,
                          inout metadata_t meta)
{
    apply { }
}

control my_ingress(inout headers_t hdr,
                  inout metadata_t meta,
                  inout standard_metadata_t standard_metadata)
{
    bool dropped = false;

    action drop_action() {
        mark_to_drop(standard_metadata);
        dropped = true;
    }

    action to_port_action(bit<9> port) {
        hdr.ipv4.ttl = hdr.ipv4.ttl - 1;
        standard_metadata.egress_spec = port;
    }

    table ipv4_match {
        key = {
            hdr.ipv4.dst_addr: lpm;
        }
        actions = {
            drop_action;
            to_port_action;
        }
        size = 1024;
        default_action = drop_action;
    }

    apply {
        ipv4_match.apply();
        if (dropped) return;
    }
}

control my_egress(inout headers_t hdr,
                 inout metadata_t meta,
                 inout standard_metadata_t standard_metadata)
{
    apply { }
}

V1Switch(my_parser(),
         my_verify_checksum(),
         my_ingress(),
         my_egress(),
         my_compute_checksum(),
         my_deparser()) main;
```
This is an extremely simple program. It has a single lookup table,
which does a longest-prefix-match (LPF) on the destination IP address
in the received packet. The action is either drop the packet, or
forward the packet to a specific output port.

Note: Personally, instead of editing the files directly on the AWS
instance, I prefer to run the Visual Studio Code editor locally on my
MacBook and use it to remotely edit the files on the AWS instance:

* Install the [Visual Studio Code remote development extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
* In Visual Studio Code, press F1 to open the command palette
* Enter the command Remote-SSH: Connect to Host
* Enter ubuntu@x.x.x.x where x.x.x.x is the IP address of the AWS instance

# Compile the P4 program

Compile the P4 program. The `-b` option selects `bmv2` (Behavioral
Model Version 2) as the target, which is the software switch that we
will use to run the P4 program.
```
p4c -b bmv2 test.p4 -o test.bmv2
```
This compiler generates a directory test.bmv2 which contains a file
test.json which the generated “executable” code which is run by the
software switch.

# Create virtual Ethernet interfaces

We will now create three pairs of virtual Ethernet (`veth`) interfaces.

A veth interface is a virtual (i.e. fake) Ethernet interface on which
an application (the software switch in our case) can send and receive
Ethernet packets in the same way a a real Ethernet interface. However,
in the case of a veth interface the packets do not go out a real
Ethernet port. Instead, veth interfaces are always created in pairs.
We will create three pairs: `veth0-veth1`, `veth2-veth3`, and `veth4-veth5`.
When the application sends packet on one veth interface it arrives on
the other `veth` interface of the pair.

Create the three pairs of virtual Ethernet interfaces. We set the
Message Transfer Unit (MTU) of each interface to 9500 to allow us to
send and receive jumbo packets. And we disable IPv6 on each interface
to stop the kernel from sending router solicitation and multicast
listener reports (this does not prevent the software switch from
sending IPv6 packets over the interface).
```
# First pair: veth0-veth1
sudo ip link add name veth0 type veth peer name veth1
sudo ip link set dev veth0 up
sudo ip link set dev veth1 up
sudo ip link set veth0 mtu 9500
sudo ip link set veth1 mtu 9500
sudo sysctl net.ipv6.conf.veth0.disable_ipv6=1
sudo sysctl net.ipv6.conf.veth1.disable_ipv6=1

# Second pair: veth2-veth3
sudo ip link add name veth2 type veth peer name veth3
sudo ip link set dev veth2 up
sudo ip link set dev veth3 up
sudo ip link set veth2 mtu 9500
sudo ip link set veth3 mtu 9500
sudo sysctl net.ipv6.conf.veth2.disable_ipv6=1
sudo sysctl net.ipv6.conf.veth3.disable_ipv6=1

# Second pair: veth4-veth5
sudo ip link add name veth4 type veth peer name veth5
sudo ip link set dev veth4 up
sudo ip link set dev veth5 up
sudo ip link set veth4 mtu 9500
sudo ip link set veth5 mtu 9500
sudo sysctl net.ipv6.conf.veth4.disable_ipv6=1
sudo sysctl net.ipv6.conf.veth5.disable_ipv6=1
```

# Start the software switch and execute the P4 program

In the following steps we will be opening multiple SSH sessions, so you will need to open multiple terminal windows or tabs.

In the first SSH session, start the software switch as a background process:
```
sudo simple_switch --interface 0@veth0 --interface 1@veth2 --interface 2@veth4 test.bmv2/test.json &
```
In the same SSH session, start the Command Line Interface (CLI) for the software switch:
```
simple_switch_CLI
```
You should get a RunTimeCmd prompt:
```
Obtaining JSON from switch...
Done
Control utility for runtime P4 table manipulation
RuntimeCmd:
```
At this point we have a running P4 software switch with 3 interfaces as shown in Figure 1.

<p style="text-align:center;"><img style="display:block; margin:0 auto;" src="{{ site.baseurl }}/assets/getting-started-with-p4.png" alt="Emulated network architecture" width="600" /><strong>Figure 1: Emulated network architecture.</strong></p>
 
# Some CLI commands

In the software switch CLI enter the `help` command to see what commands are available:
```
RuntimeCmd: help

Documented commands (type help <topic>):
========================================
act_prof_add_member_to_group       set_crc16_parameters                   
act_prof_create_group              set_crc32_parameters                   
act_prof_create_member             set_queue_depth                        
act_prof_delete_group              set_queue_rate                         
act_prof_delete_member             shell                                  
act_prof_dump                      show_actions                           
act_prof_dump_group                show_ports                             
act_prof_dump_member               show_tables      
[...]
```

The `show_tables` command reports that there is a `my_ingress.ipv4_match` table:
```
RuntimeCmd: show_tables
my_ingress.ipv4_match          [implementation=None, mk=ipv4.dst_addr(lpm, 32)]
tbl_test87                     [implementation=None, mk=]
```
The `table_info` command reports more details about the table:
```
RuntimeCmd: table_info ipv4_match
my_ingress.ipv4_match          [implementation=None, mk=ipv4.dst_addr(lpm, 32)]
********************************************************************************
my_ingress.drop_action         []
my_ingress.to_port_action      [port(9)]
```

# Add routes to the route table

In the software switch CLI use the `table_add` command to add four routes to the route table:
* All traffic to prefix 10.10.0.0/16 is sent to port 0
* All traffic to prefix 11.11.0.0/16 is sent to port 1
* All traffic to prefix 12.12.0.0/16 is sent to port 2
* All traffic to prefix 20.20.20.0/24 is dropped
* All traffic that doesn’t match any of the above prefixes is dropped as well because the default action for the table is drop.

```
RuntimeCmd: table_add ipv4_match to_port_action 10.10.0.0/16 => 0
Adding entry to lpm match table ipv4_match
match key:           LPM-0a:0a:00:00/16
action:              to_port_action
runtime data:        00:00
Entry has been added with handle 0

RuntimeCmd: table_add ipv4_match to_port_action 11.11.0.0/16 => 1
Adding entry to lpm match table ipv4_match
match key:           LPM-0b:0b:00:00/16
action:              to_port_action
runtime data:        00:01
Entry has been added with handle 1

RuntimeCmd: table_add ipv4_match to_port_action 12.12.0.0/16 => 2
Adding entry to lpm match table ipv4_match
match key:           LPM-0c:0c:00:00/16
action:              to_port_action
runtime data:        00:02
Entry has been added with handle 2

RuntimeCmd: table_add ipv4_match drop_action 20.20.20.0/24 =>
Adding entry to lpm match table ipv4_match
match key:           LPM-14:14:14:00/24
action:              drop_action
runtime data:        
Entry has been added with handle 3
```
The `table_dump` command shows the entries that we added to the table:
```
RuntimeCmd: table_dump ipv4_match
==========
TABLE ENTRIES
**********
Dumping entry 0x0
Match key:
* ipv4.dst_addr       : LPM       0a0a0000/16
Action entry: my_ingress.to_port_action - 00
**********
Dumping entry 0x1
Match key:
* ipv4.dst_addr       : LPM       0b0b0000/16
Action entry: my_ingress.to_port_action - 01
**********
Dumping entry 0x2
Match key:
* ipv4.dst_addr       : LPM       0c0c0000/16
Action entry: my_ingress.to_port_action - 02
**********
Dumping entry 0x3
Match key:
* ipv4.dst_addr       : LPM       14141400/24
Action entry: my_ingress.drop_action - 
==========
Dumping default entry
Action entry: my_ingress.drop_action - 
==========
```

# Observe the behavior of the software switch

In a separate Terminal window and SSH session, issue the following command to dump packets that arrive on interface veth1:
```
sudo tcpdump -n -i veth3
```
The initial output is:
```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on veth3, link-type EN10MB (Ethernet), capture size 262144 bytes
```
# Inject some packets into the software switch:

In yet another separate Terminal window and SSH session, start scapy, which we will use to inject packets into the software switch:
```
sudo scapy
```
You get a welcome message, some warnings, and a prompt:
```
INFO: Can't import matplotlib. Won't be able to plot.
INFO: Can't import PyX. Won't be able to use psdump() or pdfdump().
WARNING: No route found for IPv6 destination :: (no default route?)
INFO: Can't import python ecdsa lib. Disabled certificate manipulation tools
Welcome to Scapy (2.3.3)
>>> 
```
Using Scapy, inject a packet with destination IP address 11.11.1.1 into interface veth1:
```
>>> p = Ether()/IP(dst="11.11.1.1")/UDP()
>>> sendp(p, iface="veth1")
.
Sent 1 packets.
```
The packet arrives in the software switch on port 0 (interface `veth0`). It matches route 11.11.0.0/16 and is forwarded to port 1 (interface veth2, which is connected to interface veth3).

In the second SSH session, where tcpdump is running, we can see that the packet arrived:
```
10:48:52.746999 IP 172.31.41.253.53 > 11.11.1.1.53: [|domain]
```
Back in the third SSH session, where scapy is running, send a packet with destination IP address 12.12.1.1 on interface veth0:
```
>>> p = Ether()/IP(dst="12.12.1.1")/UDP()
>>> sendp(p, iface="veth1")
.
Sent 1 packets.
```
This time, the packet is forwarded to port 2 (interface veth4, which is connected to interface veth5). Tcpdump does not report any received packet because it is monitoring interface veth3 and not interface veth5.

# Why am I interested in P4?

Given my general interest in Software Defined Networking (SDN) and
network programmability, learning P4 has been on my TODO list for
quite a while.

But the specific trigger for rolling up my sleeves and getting my
hands dirty writing an actual P4 program was a [series of
seminars](https://github.com/brunorijsman/qutech-seminars) that I
presented at [QuTech](https://qutech.nl/) at the [Delft University of
Technology](https://www.tudelft.nl/en/) (my alma mater) in the
Netherlands.

I presented these seminars to the physicists and mathematicians
working on the [Quantum
Internet](https://qutech.nl/roadmap/quantum-internet/). Most of the
professors, postdocs, PhDs, and students working in this group have a
very strong background in physics and quantum mechanics, but less
practical experience in the field of networking (they call it
"classical networks" to distinguish it from "quantum networks"). The
purpose of these seminars was to bring them up to speed with basic
concepts and recent developments in the field of classical networking.

In [one of these
seminars](https://github.com/brunorijsman/qutech-seminars/blob/master/qutech-seminar-4---data-plane-p4---2019-09-12---v1.pdf)
I discussed the data plane in general and the possibility of using P4
to program quantum networks (the short answer is that it looks
promising). 

# Further reading

* [The P4-16 specification](https://p4.org/p4-spec/docs/P4-16-v1.1.0-spec.html)
* [The Portable Switch Architecture (PSA) specification](https://p4.org/p4-spec/docs/PSA-v1.1.0.html)
* [P4 tutorials](https://github.com/p4lang/tutorials/)
* [Simple switch tutorial](https://github.com/jafingerhut/p4-guide/blob/master/README-using-bmv2.md)
* [Scapy documentation](https://scapy.readthedocs.io/en/latest/)
