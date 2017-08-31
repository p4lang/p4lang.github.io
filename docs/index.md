---
layout: single
---

<table>
<tr><td>    
# Protocol Independent

P4 programs specify how a switch processes packets.

# Target Independent

P4 is suitable for describing everything from high- performance forwarding ASICs to software switches.

# Field Reconfigurable

P4 allows network engineers to change the way their switches process packets after they are deployed.
</td></tr>
<tr><td>
```p4
control ingress() {
  table routing {
    key = {
      ipv4.dstAddr : lpm;
    }
    actions = { do_drop;
      route_ipv4;
    }
    size = 2048; 
  }
  apply {   
    routing.apply();
  }
}    
```    
</td></tr>
<table>    
       