---
layout: photolist
title: Talks
---

{% assign hashes = (site.data.talks) %}
{% capture years %}
{% for hash in hashes %}
{{ hash[0] }}
{% endfor %}
{% endcapture %}

{% assign sortedyears = years | split:' ' | sort | reverse %}
{% for year in sortedyears %}
### {{ year }}
{% for talk in hashes[year] %}
{% include talk.html talk=talk %}
{% endfor %}
{% endfor %}
