---
layout: page
permalink: /data-science/
---
<style type="text/css">

@media only screen and (max-width: 300px) {
	.prev, .next,.text {font-size: 11px}
}
.row {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}

/* Create four equal columns that sits next to each other */
.column {
  flex: 25%;
  max-width: 50%;
  padding: 0 4px;
}

.column img {
  margin-top: 8px;
  vertical-align: middle;
  width: 100%;
}

/* Responsive layout - makes a two column-layout instead of four columns */
@media screen and (max-width: 800px) {
  .column {
    flex: 100%;
    max-width: 50%;
  }
}

/* Responsive layout - makes the two columns stack on top of each other instead of next to each other */
@media screen and (max-width: 600px) {
  .column {
    flex: 100%;
    max-width: 100%;
  }
}
</style>

<h2 class="post-list-heading">Data Science</h2>
---
<br>
There is an ocean of content on the concepts from Data Science and AI on the internet. What gets published here is the knowledge and perspectives gained from our experience of leaning and applying these concepts, by living up to the objective of Data Sapien. More importantly, we aim to publish content on some of the untouched topics that are not easily found with a straight-forward Stackoverflow or Google search. These untouched topics are the problems that we face while working on devising an ML-powered framework to solve a real-world problem. Hence, this category is generally more suited for interns or working professionals who are familiar with basics of Python programming, Statistics, Machine Learning and ML engineering. With that being said, we will always mention the road to learning the prerequisites for understand our posts.
<br>
<h2>Browse through sub-categories</h2>
---
<br>

<div class="row"> 
  <div class="column">
    <a href="/statistics/"><img src="/assets/stock_images/data_science/statistics.png"></a>
    <a href="/python/"><img src="/assets/stock_images/data_science/python.png"></a>
    <a href="/deep-learning/"><img src="/assets/stock_images/data_science/deep_learning.png"></a>
  </div>
  <div class="column">
    <a href="/time-series/"><img src="/assets/stock_images/data_science/time_series.png"></a>
    <a href="/spark/"><img src="/assets/stock_images/data_science/spark.png"></a>
    <a href="/machine-learning/"><img src="/assets/stock_images/data_science/machine_learning.png"></a>
  </div> 
</div>

<br>
<h3>Recently Published</h3>
---
<br>
<div>
{% for post in site.categories.data-science %}
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
      </div><br>
          
  {%- endif -%}
 
{% endfor %}
</div>
<!-- p float="left">
  <a href="/blog/"><img src="/assets/stock_images/data_science/deep_learning.png" width="355" height="70"/></a>
  <a href="/data-science/"><img src="/assets/stock_images/data_science/machine_learning.png" width="355" height="70" hspace="0" object-fit="contain"/></a>
</p>
<p float="centre">
  <a href="/blog/"><img src="/assets/stock_images/data_science/statistics.png" width="355" height="70" hspace="0.75"/></a>
  <a href="/time-series/"><img src="/assets/stock_images/data_science/time_series.png" width="355" height="70" hspace="0"/></a> 
</p>
<p align="centre">
  <a href="/blog/"><img src="/assets/stock_images/data_science/python.png" width="355" height="70"/></a>
  <a href="/blog/"><img src="/assets/stock_images/data_science/spark.png" width="355" height="70"/></a> 
</p> -->

<!-- <br>
<h2 class="post-list-heading">Recently published</h2>
---
<br>
<ul class="post-list"><li><span class="post-meta">Mar 24, 2021</span>
    <h3>
      <a class="post-link" href="/time-series/forecasting-at-scale/">
        Forecasting at Scale
      </a>
    </h3></li></ul>

<ul class="post-list"><li><span class="post-meta">Mar 10, 2021</span>
    <h3>
      <a class="post-link" href="/time-series/time-series-primer/">
        Time-series Primer
      </a>
    </h3></li></ul>

<br>
<h2 class="post-list-heading">Upcoming</h2>
---
<br>
<ul class="post-list"><li><span class="post-meta">Early 2021 | Statistics</span>
        <h3>
          <a class="post-link">
            Applying Entropy on the left, right and centre of data discovery
          </a>
        </h3></li><li><span class="post-meta">Early 2021 | Python | Spark</span>
        <h3>
          <a class="post-link">
            Exploring the world of parallel processing from Py...to...Spark 
          </a>
        </h3></li>
        <li><span class="post-meta">Early 2021 | Time-series | Statistics</span>
        <h3>
          <a class="post-link">
            Deep dive des Algorithmus | Facebook's Prophet 
          </a>
        </h3></li>
        </ul>
 -->


