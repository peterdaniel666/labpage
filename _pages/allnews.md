---
title: "News | SynThera Group"
layout: textlay
excerpt: "News | SynThera Group"
sitemap: false
permalink: /allnews.html
---

# News

{% for article in site.data.news %}

<p>{{ article.date }} <br>
<em>{{ article.headline }}</em></p>
{% endfor %}
