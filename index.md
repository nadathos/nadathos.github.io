---
layout: default
permalink: /
---

{% assign PostsByDate =
    site.posts | group_by_exp:"post", "post.date | date: '%s'" %}

<h2 id="left"> Newest post: </h2>
<div id="postbox">
<ul style="list-style: none;">
  <li>
    {% for post in PostsByDate limit:1 %}
    <hr class="fadinggrad">
    {% assign newest_post = post %}
        <a style="display:block;" href="{{ post.url }}">
          <div>
            <div>
              {% if post.thumbnail %}
              <img src="{{ post.thumbnail }}" />
              {% else %}
              <img src="assets/images/thumb.png" />
              {% endif %}
            </div>
            <div>
              <h2 style="color:gold">{{ post.title }}</h2>
              {%if post.excerpt%}
                <p>{{post.excerpt}}</p>
              {%endif%}
              <p> Author: {{post.author}}, Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
              <hr class="fadinggrad">
            </div>
          </div>
        </a>
    {% endfor %}
  </li>
</ul>
</div>

<div style="padding-top:3%">
<h2 id="left"> similar: </h2>
<ul style="list-style: none;">
  <li>
    {% for post in PostsByDate limit:3 offset:1 %}
    {% if post != newest_post %}
    {% if post %}
    <hr class="fadinggrad">
    {% endif %}
        <a style="display:block;" href="{{ post.url }}">
          <div>
            <div>
              <h2 style="color:gold">{{ post.title }}</h2>
              {%if post.excerpt%}
                <p>{{post.excerpt}}</p>
              {%endif%}
              <p> Author: {{post.author}}, Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
              {% if post %}
              <hr class="fadinggrad">
              {% endif %}
            </div>
          </div>
        </a>
    {% endif %}
    {% endfor %}
  </li>
</ul>
</div>
