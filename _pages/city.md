---
title: "The Urban Plant Evolution Project"
layout: textlay
excerpt: "Josephs Lab at Michigan State University."
sitemap: false
permalink: /city.html
---

# News

{% for article in site.data.cityWriteUp %}
<p>{{ article.date }} <br>
<em>{{ article.headline }}</em></p>
{% endfor %}
