---
layout: posthome
permalink: /machine-learning/
comments: false
---
<h2 class="post-list-heading">Machine Learning</h2>
---
<br>
<div>
{% assign ps = 0 %}
{% for post in site.categories.machine-learning %}
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
      {% assign ps = 1 %}
  {%- endif -%}
 
{% endfor %}
</div>

{%- if ps == 0 -%}
    No posts yet!
{%- endif -%}

<br><br>
<h3 class="post-list-heading">Upcoming</h3>
---
<br>
<div>
{% assign upc = 0 %}
{% for post in site.categories.machine-learning %}
  {%- if post.hidden -%}
      <div>
      <p class="post-meta">
        <time class="dt-published" datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">
          {%- assign date_format = site.minima.date_format | default: "%Y" -%}
          {{ post.date | date: date_format }}
        </time>
        {%- if post.author -%}
          • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span class="p-author h-card" itemprop="name">{{ post.author }}</span></span>
        {%- endif -%}</p>
      <h3 class="post-title p-name" itemprop="name headline"><a href="">{{ post.title | escape }}</a></h3>
      </div>
      {% assign upc = 1 %}
  {%- endif -%}

{% endfor %}
</div>

{%- if upc == 0 -%}
    None yet!
{%- endif -%}

