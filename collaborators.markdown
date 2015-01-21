---
layout: photolist
title: Collaborators
---

I have the great pleasure to work with very smart people.
Here are some of them.


{% for post in site.people %}
{% include person.html person=post %}
{% endfor %}
