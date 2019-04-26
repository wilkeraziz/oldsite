---
layout: photolist
title: Events
menu: yes
---

<iframe src="https://calendar.google.com/calendar/b/1/embed?showTitle=0&amp;showPrint=0&amp;mode=WEEK&amp;height=600&amp;wkst=2&amp;hl=en_GB&amp;bgcolor=%23FFFFFF&amp;src=ld3i6i6l47vkidf162nb95u8oo%40group.calendar.google.com&amp;color=%23853104&amp;src=n7ae5iuqjqpfc40h212k8ouib8%40group.calendar.google.com&amp;color=%238D6F47&amp;src=bata2v5fen3ep9f2kvnns6ioh8%40group.calendar.google.com&amp;color=%2329527A&amp;src=376p89h9h5c3k0pj10li8qpm1o%40group.calendar.google.com&amp;color=%235F6B02&amp;src=g83o6vkuchrpm4i2iel7ls7dag%40group.calendar.google.com&amp;color=%2323164E&amp;ctz=Europe%2FAmsterdam" style="border-width:0" width="600" height="300" frameborder="0" scrolling="no"></iframe>

<br/>

**Reading groups**

{% assign groups = (site.data.reading | where: "selected", "y") %}
{% for group in groups %}
{% include group.html group=group %}
{% endfor %}

<br/>

**Reading lists**

* [Deep generative models](pages/landscape)
* [Optimisation](pages/opt)
* [Bayesian NLP](pages/bayesiannlp)
* [Statistics](pages/stat)

**Retired reading groups**

* [SLPL](pages/slpl)
* [DL](pages/deeplearning)

**Other events**

* March 22, 2018: I am co-organising a [DGM day at UvA](//uva-slpl.github.io/dgmday) where we will be presenting our VI tutorial as well as a bunch of interesting DGMs in NLP
