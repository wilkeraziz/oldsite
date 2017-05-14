---
layout: photolist
title: Teaching
menu: yes
---

# Courses

{% assign courses = (site.data.teaching.courses | where: "selected", "y") %}
{% for course in courses %}
{% include course.html course=course %}
{% endfor %}

# Projects

## Featurised EM

In the spring of 2016, I offered a BA project on [feature-rich unsupervised alignment models](resources/courses/BA-featurised-EM.pdf). My student [Guido Linders](//esc.fnwi.uva.nl/thesis/centraal/files/f1886233032.pdf) did a great job ([thesis](//esc.fnwi.uva.nl/thesis/centraal/files/f1886233032.pdf), [code](//github.com/wilkeraziz/lola))!

## Slice sampling from PCFGs

In the spring of 2015, I offered a BA project on [slice sampling from PCFGs](resources/courses/BA-slice-sampling.pdf). My student [Iason de Bondt](//nl.linkedin.com/in/iason-de-bondt-3676ba101) did a great job ([thesis](//esc.fnwi.uva.nl/thesis/centraal/files/f1550974112.pdf), [code](//github.com/wilkeraziz/pcfg-sampling))!



