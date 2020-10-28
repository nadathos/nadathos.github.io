---
layout: default
permalink: /
---

{% assign PostsByDate = site.posts %}
{% for post in PostsByDate limit:1 %}
{% assign FirstPost = post %}
{% endfor %}


  <div>
        <p style="text-align:right; font-style:italic; font-size: 90%"></p>
        <div class="left">
        <br>
        <br>
        <hr class="fadinggrad">
        </div>
        {% for post in PostsByDate%}
        <a style="display:block;" href="{{site.url}}{{ post.url }}">
          <biglink>
          <div>
            <h2>{{post.title}}</h2>
            <br>
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
              <p> Tags: {% for tag in post.tags limit: 3 %} {{tag}}{% endfor %} Published: {{post.date | date_to_long_string }}</p>
              <hr class="fadinggrad">
          </div>
          </biglink>
        </a>
        <br>
        <br>
          {% endfor %}
  </div>

