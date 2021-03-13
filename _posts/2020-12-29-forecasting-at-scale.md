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
Time-series forecasting is a widely adopted practice in many businesses that produce and store temporal measurements. Often, the scale of the business problem causes a variety of problems in producing reliable and interpretable forecasts. Such problems include the volume, variety and quality of time-series data which makes it challenging to train intrepretable predictive models. 
<br><br>
A similar challenge is faced during the production of cinematic music due to the variation in the number and duration of scenes. Composers use a clever technique to tackle this problem, which can be replicated by Data Scientists to build a robust forecasting framework at scale. To understand how, continue reading by acknowledging that you are familiar with fundamentals of time-series. If you need a refresher, go through my [time-series primer](/time-series/time-series-primer/).

![time series 101](/assets/stock_images/data_science/time-series/forecasting-at-scale/cover.jpg)
*Photo by [Vienna Reyes](https://unsplash.com/@viennachanges) on [Unsplash](https://unsplash.com/s/photos/solar-system?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
<br>

<h3>The Scale</h3>
---
<br>
Tackling the sheer volume of time-series variables and the associated variety and data quality issues remain as the significant challenge in forecasting problems. The number of time-series variables can range from tens of tens to tens of thousands to tens of millions. This post addresses the scale of devising an appropriate framework to train and interpret models for each variable when there are several variables. The scale of engineering a distributed computing system for fast and efficient model training shall be addressed in a different post in future.

The brute force approach is to use an AutoMLesque time-series forecasting package for all variables. Such a package would select the best performing model for each variable and doing so would have solved only half the problem. Often, accuracy alone is not sufficient to justify interpretability of models. A robust forecasting framework has to embody accuracy as well as interpretability. To build one, data scientists can replicate the cinematic music production technique. 

<h3>The technique</h3>
---
<br>
In cinematic music production, a theme song is composed to be the signature music associated to the overall story. Specific tracks are composed for prominent locations or characters in the story. For each scene, the music will be a mix of theme song and character/ location tracks. The duration of score will not scale proportionally with the duration of movie. To replicate this technique, Data Scientists need to identify the theme of the forecasting problem at hand and classify time-series variables as a few characters. 

The theme of the forecasting problem can be defined by answering the following questions:
<ul>
	<li>Meaningful history</li>
	<li>Zeroes vs Missing values</li>
	<li>Suitable validation rule book</li>
</ul> 
<br>
<div class="tab">
  <button class="tablinks2" onclick="showTabContent2(event, 'History')" id="defaultOpen2">History</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Zeroes & Missing values')">Zeroes vs Missing values</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Validation')">Validation</button>
</div>

<div id="History" class="tabcontent2" checked="true">
  <p>
  Meaningful history is the amount of historical data suitable and useful for training. This parameter can be determined using grid search. However, given the dynamic nature of most businesses, there can be multiple changepoints in the time-series. The frequency of changepoints needs to be assessed for determining an appropriate start. If there are multiple valid starts to choose from, then grid search can be applied to select one.  
  <br><br>
  Consider a stock-price prediction problem as an example. The time-series data shall be available for several years, but for most companies, prices before a few quarters into past would not have any relationship with those in the present day. The years of data is not useful for training. Consider user footprint volume prediction where the definition of user foot prints changes with time. The distribution of time-series changes everytime the definition changes, and not historical observations are useful for training.

  <br><br>
  These are the problems faced when data is abundant. But if it is not, the models cannot learn the true distributions and will be subject to heavy bias or variance. That's why interpretation of meaningful history from business is crucial and can guide data scientists in making better decisions in situations with varying data sizes. Also, it is a good practice to include a rule-based system or naive algorithms in addition to the traditional and sophisticated models in the AutoML package.

 
  </p>
</div>

<div id="Zeroes & Missing values" class="tabcontent2">
  <p>
  The rationale behind presence of missing values needs to be investigated to decide on the right treatment procedure. It is further more important to understand the difference between zeroes and missing values in the context of business. 
  <br><br>
  In weather forecasting, a value of zero is possible and different from missing values. The missing values would have appeared due to equipment failure or data loss among a multitude of reasons. In such cases, they have to be treated differently from zeroes. Consider a demand forecasting problem where zero demand indicates no demand. There may not be a difference between zeroes and missing values in such cases and they can be treated similarly.
  <br><br>
  Missing values represent the intermittency of time-series and how they are treated will alter the distribution of time-series. The models aren't trained with right data if zeroes and missing values are treated inappropriately.
  </p> 
</div>

<div id="Validation" class="tabcontent2">
  <p>
   A right validation procedure for a forecasting framework quantifies its potential to solve the business problem. The validation can be done right by approximating the business problem as a real-valued function of time-series variables. The uncertainity associated with the values of this function is derivable from the individual model errors.

  <br><br>
  For time-series variables, there are several metrics to evaluate accuracy. Sometimes, MAPE is more suitable if the error needs to be quantified on a relative basis. However, MABS can be more meaningful in situations where MAPE will be consistently larger due to the scale of values. A combination of traditional accuracy metrics shall be robust enough for any variable irrespective of its distribution. The uncertainity associated with the function of time-series variables can be estimated by applying the theory of random variables or simpler heuristics.

  <br><br>
   Consider a classical hierarchical forecasting problem where the volume of units sold is forecasted with an objective of estimating cumulative revenue. The errors made by the individual models can be small, but the error made on revenue estimation by adding the invidual predictions is unknown. Also, scale of unit-volumes might significantly differ from the scale of revenues. Traditional accuracy metrics like MAPE might get enlarged or shrunk in translation if the relationship between unit-volume and revenue is not linear. Unless computed, the performance of individual models cannot be correlated with the performance of forecasting system.
  </p> 
</div>

<script type="text/javascript">document.getElementById("defaultOpen2").click();</script><br> 
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

