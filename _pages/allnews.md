---
title: "Josephs Lab - News"
layout: textlay

excerpt: "Josephs Lab at Michigan State University."
sitemap: false
permalink: /allnews.html
---

# News

{% for article in site.data.news %}
<p>{{ article.date }} <br>
<em>{{ article.headline }}</em></p>
{% endfor %}
