---
layout: photolist
title: Events
menu: yes
---

<iframe src="https://calendar.google.com/calendar/embed?showTitle=0&amp;height=600&amp;wkst=1&amp;bgcolor=%23FFFFFF&amp;src=c752525tganmcbvhfl1tu2b9vo%40group.calendar.google.com&amp;color=%2329527A&amp;src=5l9p71c5fd0gse4ibtrks0170k%40group.calendar.google.com&amp;color=%232952A3&amp;src=4qveld4kb4i5sa9t3ev55bmk10%40group.calendar.google.com&amp;color=%23AB8B00&amp;src=d5etdgvg97ajfnbetjebkmbdis%40group.calendar.google.com&amp;color=%235F6B02&amp;src=aci7h1ua23taamdbat5hu73h14%40group.calendar.google.com&amp;color=%23AB8B00&amp;src=oa6cmu8nbg8iet2j07d9tobs1c%40group.calendar.google.com&amp;color=%23711616&amp;src=iuesktj5bg3jmil7kjjtpplju4%40group.calendar.google.com&amp;color=%23182C57&amp;ctz=Europe%2FAmsterdam" style="border-width:0" width="600" height="300" frameborder="0" scrolling="no"></iframe>

<br/>

**Reading groups**

{% assign groups = (site.data.reading | where: "selected", "y") %}
{% for group in groups %}
{% include group.html group=group %}
{% endfor %}

<br/>

**Reading lists**

* [Optimisation](pages/opt)
* [Bayesian NLP](pages/bayesiannlp)
* [Statistics](pages/stat)

**Retired reading groups**

* [SLPL](pages/slpl)
* [DL](pages/deeplearning)

**Other events**

* March 22, 2018: I am co-organising a [DGM day at UvA](//uva-slpl.github.io/dgmday) where we will be presenting our VI tutorial as well as a bunch of interesting DGMs in NLP
