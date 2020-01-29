---
layout: default
permalink: /
---

{% assign PostsByDate = site.posts %}

<div class="wrapper">
<div id="smaller_left">
<h2 id="padded" style="color:gold">New:</h2>
<ul style="list-style: none;">
  <li>
    {% for post in PostsByDate limit:1 %}
    <hr class="fadinggrad">
    {% assign newest_post = post %}
    {% assign newest_tags = post.tags%}
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


<div id="smaller_left">
  <h2 id="padded" style="color:gold">Similar:</h2>
  <hr class="fadinggrad">
  <ul style="list-style: none;">
    <li>
    {% comment %}---> from https://stackoverflow.com/questions/25348389/jekyll-and-liquid-show-related-posts-by-amount-of-equal-tags-2 {% endcomment %}
    {% comment %}---> the maximum number of related to posts
                      to be printed {% endcomment %}
    {% assign maxRelated = 3 %}
    {% comment %}---> the minimum number of common tags
                      to have for a post to be considered
                      as a related post {% endcomment %}
    {% assign minCommonTags =  1 %}
    {% assign maxRelatedCounter = 0 %}

    {% for post in PostsByDate offset:1 %}
      {% assign sameTagCount = 0 %}
      {% assign commonTags = '' %}

      {% for tag in post.tags %}
        {% comment %}---> Only compare if post is
                          not same as current page {% endcomment %}
        {% if post.url != page.url %}
          {% if page.tags contains tag %}
            {% assign sameTagCount = sameTagCount | plus: 1 %}
            {% capture tagmarkup %} <span class="label label-default">{{ tag }}</span> {% endcapture %}
            {% assign commonTags = commonTags | append: tagmarkup %}
          {% endif %}
        {% endif %}
      {% endfor %}

      {% if sameTagCount >= minCommonTags %}
      {% comment %} <hr class="fadinggrad"> {% endcomment %}
          <a style="display:block;" href="{{ post.url }}">
            <p>
                <h2 style="color:gold">{{ post.title }}</h2>
                {%if post.excerpt%}
                  <p>{{post.excerpt}}</p>
                {%endif%}
                <p> Author: {{post.author}}, Published: {{post.date | date_to_long_string }}, common tags: {{commonTags}}</p>
                {% if post %}
                {% endif %}
            </p>
          </a>
      {% endif %}

      {% if maxRelatedCounter >= maxRelated %}
              {% break %}
      {% endif %}
      {% endfor %}

      {% assign NumSimilarMissing =  maxRelated| plus: -maxRelatedCounter %}
      {%if NumSimilarMissing != 0%}
      {% for post in PostsByDate limit: NumSimilarMissing offset:1 %}
      {% comment %} <hr class="fadinggrad"> {% endcomment %}
          <a style="display:block;" href="{{ post.url }}">
               <h2 style="color:gold">{{ post.title }}</h2>
                {%if post.excerpt%}
                  <p>{{post.excerpt}}</p>
                {%endif%}
                <p> Author: {{post.author}}, Published: {{post.date | date_to_long_string }}, most recent</p>
                {% if post %}
                {% endif %}
         </a>
      {% endfor %}
      {% endif %}
    </li>
  </ul>
  <hr class="fadinggrad">
</div>
</div>
