---
layout: page
title: All Posts
---

<div class="posts">
  <ul>
    {% for post in site.posts %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a> - <i>{{ post.date | date_to_string }}</i>
      </li>
    {% endfor %}
  </ul>
</div>