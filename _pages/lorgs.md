---
layout: page
permalink: /lorgs/
---
<h2>LORGs</h2>

LORG is an acronym for large organization. Such humungous organizations came into existence and continue to survive by solving some of the most challenging problems. In this category, the posts shall highlight the disruptive and fascinating approaches taken by LORGs in solving such unprecedented problems at scale.

<br>

<h3 class="post-list-heading">Posts</h3>
---
<br>
{% for post in site.categories.lorgs %}
  {%- if post.hidden -%}
      <p></p>
  {%- else -%}
      <div>
      <h3 class="post-title p-name" itemprop="name headline"><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3>
      <p class="post-meta">
        <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
          {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
          {{ post.date | date: date_format }}
        </time>
        {%- if post.author -%}
          • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ post.author }}</span></span>
        {%- endif -%}</p>
      </div>
  {%- endif -%}
 
{% endfor %}
<br>
<h3 class="post-list-heading">Upcoming</h3>
---
<br>
{% for post in site.categories.lorgs %}
  {%- if post.hidden -%}
      <div>
      <h3 class="post-title p-name" itemprop="name headline"><a href="">{{ post.title | escape }}</a></h3>
      <p class="post-meta">
        <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
          {%- assign date_format = site.minima.date_format | default: "%Y" -%}
          {{ post.date | date: date_format }}
        </time>
        {%- if post.author -%}
          • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ post.author }}</span></span>
        {%- endif -%}</p>
      </div>
  {%- else -%}
      <div><p>None yet!</p></div>
  {%- endif -%}
 
{% endfor %}

{% if site.categories.lorgs %}
{% else %}
   <div><p align="centre">No posts yet!</p></div>
{% endif %}



<!-- {% if site.categories.LORGs %}
    {% for post in site.categories.LORGs %}
   <h3 class="post-title p-name" itemprop="name headline"><a class="u-url" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3>
   <p class="post-meta">
        <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
          {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
          {{ post.date | date: date_format }}
        </time>
        {%- if post.author -%}
          • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ post.author }}</span></span>
        {%- endif -%}</p>
  {% endfor %}
{% else %}
   <div><p align="centre">No posts yet!</p></div>
{% endif %} -->

<!-- <h2 class="post-list-heading">Upcoming</h2>
---
<br>
<ul class="post-list"><li><span class="post-meta">Early 2021</span>
        <h3>
          <a class="post-link">
            Need for Speed: Indian Railways
          </a>
        </h3></li><li><span class="post-meta">Mid 2021</span>
        <h3>
          <a class="post-link">
            Creating a world class experience at the world's richest temple 
          </a>
        </h3></li>
        </ul> -->