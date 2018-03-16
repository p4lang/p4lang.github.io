---
layout: page
title: "Language Design Working Group"
description: "Language Design Working Group"
permalink: ldwg/
---

## Charter

The Language Design Working Group is responsible for developing and
maintaining the P4 language specification and accompanying software
artifacts.
    
## Co-Chairs

* Gordon Brebner (Xilinx)
* Nate Foster (Cornell)

## Mailing Lists

* [Sign up](http://lists.p4.org/mailman/listinfo/p4-design_lists.p4.org)
* [Archive](http://lists.p4.org/pipermail/p4-design_lists.p4.org/)

## Code

* Specifications [https://github.com/p4lang/p4-spec/](https://github.com/p4lang/p4-spec/)    
* P4 Compiler [https://github.com/p4lang/p4c/](https://github.com/p4lang/p4c/)
* Behavioral Model version 2 [https://github.com/p4lang/bmv2/](https://github.com/p4lang/bmv2/)
    
## Meeting Minutes
<ul>
{% for minutes in site.minutes %}
{% if minutes.category == 'ldwg' %}
<li>
  <a href="{{ minutes.url | prepend: site.baseurl }}">{{ minutes.title }}</a>
</li>
{% endif %}
{% endfor %}
</ul>

&nbsp;