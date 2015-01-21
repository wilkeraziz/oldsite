---
layout: photolist
title: People
---

I have the great pleasure to work with very smart people.
Here are some of them.


{% for person in site.people %}
{% if person.selected == "y" and person.relation != "PhD candidate" %}
{% include person.html person=person %}
{% endif %}
{% endfor %}

## My students

{% for person in site.people %}
{% if person.selected == "y" and person.relation == "PhD candidate" %}
{% include person.html person=person %}
{% endif %}
{% endfor %}
