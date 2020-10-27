---
layout: default
permalink: /
---

{% assign PostsByDate = site.posts %}
{% for post in PostsByDate limit:1 %}
{% assign FirstPost = post %}
{% endfor %}

<div class="wrapper">
<div>
        <a style="display:block;" href="{{site.url}}{{ post.url }}">
          <p style="text-align:right; font-style:italic; font-size: 90%"></p>
          <div class="left">
          <br>
          <hr class="fadinggrad">
          </div>
          <div>
            <div>
              {% for post in PostsByDate%}
              <h1>{{post.headline}}</h1>
                {% if post.thumbnail %}
                <img src="{{ post.thumbnail }}" />
                {% else %}
                <img src="assets/images/thumb.png" />
                {% endif %}
              </div>
              <div>
                {%if post.excerpt%}
                  <p>{{post.excerpt}}</p>
                  <p> . . . </p>
                {%endif%}
                <p> Author: {{post.author}}, Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
                <hr class="fadinggrad">
              </div>
            {% endfor %}
          </div>
        </a>
        <br>
        <br>

</div>
