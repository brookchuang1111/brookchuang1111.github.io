---
layout: page
title: Blog Posts
---

<!--<a href="/archive-date.html">Sort by date</a>-->

{% for tag in site.tags %}
<h3>{{- tag[0] -}}</h3>
<ul>
  {%- for post in tag[1] %}
  <li><a href="{{ post.url }}">{{ post.date | date: "%b %Y" }} - {{ post.title }}</a></li>
  {%- endfor %}
</ul>
{%- endfor %}

<!-- Commented out until there are posts under the 'personal' tag
<h3>Personal</h3>
<ul>
  {%- for post in site.personal %}
  <li><a href="{{ post.url }}">{{ post.date | date: "%b %Y" }} - {{ post.title }}</a></li>
  {%- endfor %}
</ul>
-->
