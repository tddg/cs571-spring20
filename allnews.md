---
title: "Announcements"
layout: page
excerpt: "temp."
sitemap: false
permalink: /allnews.html
---

{% for article in site.data.news limit:6 %}
<p>{{ article.date }} <br>
<em>{{ article.headline }}</em></p>
{% endfor %}
