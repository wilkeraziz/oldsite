---
layout: photolist
title: Publications
---

{% assign years = (site.data.papers) %}
{% for year in years reversed %}
## {{ year[0] }}
{% assign papers = (year[1] | where: "selected", "y") %}
{% for paper in papers %}
{% include paper.html paper=paper %}
{% endfor %}
{% endfor %}
