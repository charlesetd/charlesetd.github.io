---
title: Posts
permalink: /posts/
---

<h1>Archive</h1>

{% assign postsByYear = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}
{% for year in postsByYear %}
  <h2>{{ year.name }}</h2>
  {% assign postsByMonth = year.items | group_by_exp:"post", "post.date | date: '%B'" %}
  {% for month in postsByMonth %}
  <h3>{{ month.name }}</h3>
  <ul>
    {% for post in month.items %}
      <li>
        <a href="{{ post.url }}">{{ post.date | date: '%Y-%M-%d' }}: {{ post.title }}</a>
        {{ post.excerpt }}
      </li>
    {% endfor %}
  </ul>
  {% endfor %}
{% endfor %}
