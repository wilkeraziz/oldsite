---
layout: photolist
title: People
menu: yes
---


I have the great pleasure to work with very smart people.
Here are some of them.


{% assign students = (site.data.people.colleagues | where: "selected", "y") %}
{% for person in students %}
{% include person.html person=person %}
{% endfor %}


## My students

{% assign students = (site.data.people.students | where: "selected", "y") %}
{% for person in students %}
{% include person.html person=person %}
{% endfor %}


## Former students

{% assign students = (site.data.people.former | where: "selected", "y") %}
{% for person in students %}
{% include person.html person=person %}
{% endfor %}
