---
layout: photolist
title: Albums
---

Some of the albums I cannot stop listening.

{% assign albums = (site.data.personal.albums | where: "selected", "y" | sort: "year") %}
{% for album in albums %}
{% include album.html album=album %}
{% endfor %}
