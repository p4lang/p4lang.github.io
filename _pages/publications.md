---
layout: post
title: Publications
permalink: publications/
header-img: assets/p4-background.png    
---

The research community has published a growing number of papers on the design and implementation of networked systems built using P4.
    
{% assign journals = site.data.publications | where:'type','journal' | sort:'date' | reverse %}
{% assign conferences = site.data.publications | where:'type','conference' | sort:'date' | reverse %}
{% assign workshops = site.data.publications | where:'type','workshop' | sort:'date' | reverse %}
{% assign posters = site.data.publications | where:'type','poster' | sort:'date' | reverse %}
{% assign dissertations = site.data.publications | where:'type','dissertation' | sort:'date' | reverse %}

<h1>Journals</h1>
<ul>        
{% for paper in journals %}
{% include publication.html %}
{% endfor %}
</ul> 

<h1>Conferences</h1>
<ul>        
{% for paper in conferences %}
{% include publication.html %}
{% endfor %}
</ul> 

<h1>Workshops</h1>
<ul>        
{% for paper in workshops %}
{% include publication.html %}
{% endfor %}
</ul> 

<h1>Posters</h1>
<ul>        
{% for paper in posters %}
{% include publication.html %}
{% endfor %}
</ul> 
    
<h1>Dissertations</h1>
<ul>
{% for paper in dissertations %}
{% include publication-dissertation.html %}
{% endfor %}
</ul>