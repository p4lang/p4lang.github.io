---
layout: post
title: Publications
permalink: publications/
header-img: assets/p4-background.png    
---

The research community has published a growing number of papers on the design and implementation of networked systems built using P4.
    
{% for paper in site.data.publications %}
<ul>
<li class="paper">
<span class="title">
{% if paper.url %}<a href="{{ paper.url | replace: 'BASE', site.base }}">{% endif %}&ldquo;{{ paper.title }}.&rdquo;{% if paper.url %}</a>{% endif %}
</span>
<span class="authors">{{ paper.authors }}.</span>
{% if paper.venue %}
<span>
{{ paper.date | date: "%B %Y" }}. In <i>{{ paper.venue }}</i>. 
</span>
{% endif %}
</li>
</ul>    
{% endfor %}
