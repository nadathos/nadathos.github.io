---
layout: page
permalink: /projects/
title: Projects
ProjectTag: "project"
---

<div id="smaller" class="wrapper">
<ul style="list-style: none;">
  <li>
    {% for post in site.posts %}
        {% if post.categories contains "project" %}
            <a style="display:block;" href="{{ post.url }}">
              <div>
                <div>
                  <h2 style="color:gold">{{ post.title }}</h2>
                  <p> Author: {{post.author}}, Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
                  <hr class="fadinggrad">
                </div>
              </div>
            </a>
        {% endif %}
    {% endfor %}
  </li>
</ul>
</div>
