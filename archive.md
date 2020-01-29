---
layout: default
permalink: /archive/
---

{% assign PostsByDate =
    site.posts | group_by_exp:"post", "post.date | date: '%s'" %}

<div id="postbox">
<ul style="list-style: none;">
  <hr class="fadinggrad">
  <li>
    {% for post in site.posts %}
        <a style="display:block;" href="{{ post.url }}">
          <div>
            <div>
              <h2 style="color:gold">{{ post.title }}</h2>
              <p> Author: {{post.author}}, Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
              <hr class="fadinggrad">
            </div>
          </div>
        </a>
    {% endfor %}
  </li>
</ul>
</div>
