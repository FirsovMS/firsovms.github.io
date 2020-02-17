---
layout: default
title: Home
---

> My name is Mikhail Firsov and this is my blog where I wrote about my small prjects, things and intrests,  programming languages and related topics.

{% for post in site.posts limit:5 %}
### {{ post.date | date_to_long_string }} <a href="{{ post.url }}">{{ post.title }}</a>
{{ post.excerpt }}
{% endfor %}

### [More...](/archives/)
