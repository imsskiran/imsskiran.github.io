---
layout: post
permalink: /time-series/forecasting-at-scale/
title: "Forecasting at Scale"
date:   2020-12-29 13:34:00 +0530
categories: time-series
published: false
---

<style>
/*body {font-family: Arial;}*/

/* Style the tab */
.tab {
  overflow: hidden;
  border: 0px solid #ccc;
  background-color: #f1f1f1;
  /*width: 723px;*/
}

/* Style the buttons inside the tab */
.tab button {
  background-color: inherit;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 12px 50px;
  transition: 0.3s;
  font-size: 17px;
  color: #2D59B7;
  font-family: "Courier New";
}

/* Change background color of buttons on hover */
.tab button:hover {
  background-color: #ddd;
}

/* Create an active/current tablink class */
.tab button.active {
  background-color: #282828;
  color: #E93223;
  font-weight: bold;
}

/* Style the tab content */
.tabcontent {
  display: none;
  padding: 10px 0px;
  /*border: 1px solid #ccc;*/
  border-top: none;
  -webkit-animation: fadeEffect 0.75s;
  animation: fadeEffect 0.75s;
  text-align: justify;
}

.tabcontent2 {
  display: none;
  padding: 10px 0px;
  /*border: 1px solid #ccc;*/
  border-top: none;
  -webkit-animation: fadeEffect 0.75s;
  animation: fadeEffect 0.75s;
}

@-webkit-keyframes fadeEffect {
  from {opacity: 0;}
  to {opacity: 1;}
}

@keyframes fadeEffect {
  from {opacity: 0;}
  to {opacity: 1;}
}
</style>

<h3>Prologue</h3>
Time-series forecasting is a widely adopted practice in many businesses that produce and store temporal measurements. Often, the scale of the use case causes a variety of problems in producing reliable and interpretable forecasts. Such problems include the volume, variety and quality of time-series data which makes it challenging to train intrepretable predictive models. Composers face a similar challenge due to the quantity, context and duration of scenes while producing music. Hence, data scientists can take inspiration from the framework followed by composers to build a robust framework for forecasting at scale. To understand how, continue reading by acknowledging that you are familiar with fundamentals of time-series. If you need a quick refresher on the same, go through our [Time-series 101](/time-series/time-series-101/).

![time series 101](/assets/stock_images/data_science/time-series/forecasting-at-scale/cover.jpg)
*Photo by [Vienna Reyes](https://unsplash.com/@viennachanges) on [Unsplash](https://unsplash.com/s/photos/solar-system?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
<br>

<h3>The Scale</h3>
---
<br>
In our forecasting setup, volume is the main culprit with the number of time-series variables ranging from tens of tens to tens of thousands to tens of millions. With volume, comes the variety and quality issues that cause ambiguity in model selection. While producing score, the composers first create a few character specific tracks, and then mix multiple variations of the same for all the scenes having those characters. Each character can be thought of a class of time-series variables with similar characteristics. The character specific tracks are the class-suitable forecasting algorithms. Let's look at one of the popular time-series classification methods, the set of forecasting algorithms that are suitable for the classes, and finally the framework having variants of those algorithms which is capable of producing reliable forecasts at scale.
<br>
<h3>Time-series classification</h3>
---
<br>
There are many advanced ways of accurately grouping or clustering time-series, some of which involve black-box unsupervised algorithms. However, the problem at hand is to handle volume and variety without compromising on the interpretability. One of the best suited methods for this situation is the super intuitive and computationally nimble classification method published in Croston et al.

The classification is based on the attendance and variance of the time-series. In techincal terms, the quantities are:
* <text style="color: #606060;">Average demand interval</text>
* <text style="color: #606060;">Coefficient of variation</text>

Average demand interval is the ratio of total number of periods to the number of periods with non-zero (and non-null) values.

Coefficient of variation is the squared ratio of standard deviation to the mean of non-zero (and non-null) values of time-series
<br>
<!-- ![\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}](https://latex.codecogs.com/svg.latex?x%3D%5Cfrac%7B-b%5Cpm%5Csqrt%7Bb%5E2-4ac%7D%7D%7B2a%7D) -->

Croston and second scientist have formulated their own forecasting techniques for intermittent time-series. They wanted to verify if one of their models out-perform the others as the intermittency of time-series changes. To do so quantitatively, they have formulated an inequality that the theoritical mean squared error for one of the models is smaller than the others. The inequality has ADI and CV<sup>2</sup> as parameters and the boundary condition to hold the inequality resulted in ADI and CV taking the values 1.32 and 0.49 respectively.

They have also conducted a statistical test by considering 3000 time-series. The time-series were classified based on ADI and CV<sup>2</sup> boundaries and the MSEs were computed for all three models. They have also verified the hypothesis by performing a chi-squared test with a null hypothesis that in a given class, the proportion of time-series with model 1 producing better forecast is significantly larger than model 2 producing better forecasts. 

The paper classifies time-series into the following four classes:
* <text style="color: #606060;">Smooth</text>
* <text style="color: #606060;">Intermittent</text>
* <text style="color: #606060;">Erratic</text>
* <text style="color: #606060;">Lumpy</text>


<div class="tab">
  <button class="tablinks" onclick="showTabContent(event, 'Smooth')" id="defaultOpen">SMOOTH</button>
  <button class="tablinks" onclick="showTabContent(event, 'Intermittent')">INTERMITTENT</button>
  <button class="tablinks" onclick="showTabContent(event, 'Erratic')">ERRATIC</button>
  <button class="tablinks" onclick="showTabContent(event, 'Lumpy')">LUMPY</button>

</div>
<div id="Smooth" class="tabcontent">
  <p>A time-series is classified as smooth if the ADI <= 1.32 and CV<sup>2</sup> <= 0.49. These are the time-series with good attendance and relatively little variance making forecasting techniques produce reliable forecasts. An example of a smooth time-series is <-smooth-> visualised in the plot below:</p>
</div>

<div id="Intermittent" class="tabcontent">
  <p>A time-series is classified as intermittent if the ADI > 1.32 and CV<sup>2</sup> <= 0.49. These are the time-series with bad attendance but relatively little variance making it slightly difficult for forecasting techniques to produce reliable forecasts. An example of an intermittent time-series is <-intermittent-> visualised in the plot below:</p> 
</div>

<div id="Erratic" class="tabcontent">
 <p>A time-series is classified as erratic if the ADI <= 1.32 and CV<sup>2</sup> > 0.49. These are the time-series with good attendance but relatively high variance making it tough for forecasting techniques to produce reliable forecasts. An example of an erratic time-series is <-erratic-> visualised in the plot below:
</p>
</div>
<div id="Lumpy" class="tabcontent">
 <p>A time-series is classified as lumpy if the ADI > 1.32 and CV<sup>2</sup> > 0.49. These are the time-series with bad attendance and relatively high variance making it extremely difficult and sometimes nearly impossible for forecasting techniques to produce reliable forecasts. An example of a lumpy time-series is <-lumpy-> visualised in the plot below:</p>
</div>

<script type="text/javascript" src="/assets/js/main.js"></script>
<script type="text/javascript">document.getElementById("defaultOpen").click();</script>
<br>
The classification looks simple but results in efficient segregation of time-series. A forecasting technique with great accuracy over smooth time-series might perform poorly over the remaining classes. An erratic time-series would need advanced deep learning architectures for getting better acccuracy but such models would most likely overfit a smooth time-series with fewer observations. Hence, this classification helps to straight-away eliminate a few algorithms (or variants) for each class thereby bringing down the ambiguity in model selection.

With the time-series characters now being introduced, let's look at the suitable soundtracks (algorithms) for each character.

<h3>The Algorithms</h3>
---
<br>
<div class="tab">
  <button class="tablinks2" onclick="showTabContent2(event, 'Smooth2')" id="defaultOpen2">SMOOTH</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Intermittent2')">INTERMITTENT</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Erratic2')">ERRATIC</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Lumpy2')">LUMPY</button>

</div>

<div id="Smooth2" class="tabcontent2" checked="true">
  <p>
  Algorithms for Smooth:
  <li>Prophet (weak seasonal effects)</li>
  <li>ARIMA</li>
  <li>Exponential smoothing</li>
  </p>
</div>

<div id="Intermittent2" class="tabcontent2">
  <p>
  Algorithms for Intermittent:
  <li>Prophet (strong seasonal and holiday effects)</li>
  <li>Croston</li>
  <li>Holt Winters' model</li>
  </p> 
</div>

<div id="Erratic2" class="tabcontent2">
  <p>
  Algorithms for Erratic:
  <li>Prophet (strong seasonal and holiday effects)</li>
  <li>LSTM (subject to size of data)</li>
  </p> 
</div>

<div id="Lumpy2" class="tabcontent2">
  <p>
  Algorithms for Lumpy:
  <li>Moving Average</li>
  <li>Prophet (strong seasonal and holiday effects)</li>
  <li>LSTM (subject to size of data)</li>
  <li>Exponential smoothing</li>
  </p> 
</div>
<script type="text/javascript">document.getElementById("defaultOpen2").click();</script><br> 
<h3>The Framework</h3>
---
<br>
The figure below illustrates the process flow of a forecasting framework with time-series classification and the corresponding suitable variants of algorithms. 
<br>
<h3>Epilogue</h3>
<em>This is the framework our use case deserves,</em><br>
<em>but not the one it needs right now.</em><br>

<em>So, we have kept it to a blog post,</em><br>
<em>so that someone will use it</em><br>

<em>because it's not just a framework,</em><br>
<em>it's a silent predictor, a watchful detector,</em><br>
<em><strong>A Dark Knight!</strong></em>

