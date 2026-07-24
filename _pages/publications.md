---
title: "Josephs Lab - Publications"
layout: gridlay
excerpt: "Josephs Lab -- Publications."
sitemap: false
permalink: /publications/
---


# Publications


For a full list see <a href="https://scholar.google.ca/citations?user=LeLjAToAAAAJ&hl=en" target="_blank" rel="noopener noreferrer">Google Scholar<span class="sr-only"> (opens in a new tab)</span></a>.

{% assign number_printed = 0 %}
{% for publi in site.data.publist %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if publi.highlight == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
 <div class="well">
  <h3 class="pub-title">{{ publi.title }}</h3>
  <img src="{{ site.url }}{{ site.baseurl }}/images/pubpic/{{ publi.image }}" alt="Publication figure for {{ publi.title | escape }}" class="img-responsive" width="33%" style="float: left; padding-right: 15px;" />
  <p>{{ publi.authors }}</p>
  <p><em>{{ publi.journal }}</em></p>
  <p>{{ publi.description }}</p>
  <p><strong><a href="{{ publi.link.url }}" aria-label="{{ publi.link.display }} for publication: {{ publi.title | escape }}">{{ publi.link.display }}</a></strong></p>
  {% if publi.news1 %}<p class="text-danger"><strong> {{ publi.news1 }}</strong></p>{% endif %}
  {% if publi.news2 %}<p> {{ publi.news2 }}</p>{% endif %}
 </div>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}





