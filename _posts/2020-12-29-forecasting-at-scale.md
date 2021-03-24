---
layout: post
permalink: /time-series/forecasting-at-scale/
title: "Forecasting at Scale"
date:   2021-03-24 13:34:00 +0530
categories: time-series
<!-- published: false -->
---

<style>
/*body {font-family: Arial;}*/

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
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
  padding: 10px 10px;
  border: 1px solid #ccc;
  border-top: none;
  -webkit-animation: fadeEffect 0.75s;
  animation: fadeEffect 0.75s;
  text-align: justify;
}

.tabcontent2 {
  display: none;
  padding: 10px 10px;
  border: 1px solid #ccc;
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

![forecasting at scale](/assets/stock_images/data_science/time-series/forecasting-at-scale/cover.jpg)
*Photo by [Vienna Reyes](https://unsplash.com/@viennachanges) on [Unsplash](https://unsplash.com/s/photos/solar-system?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*
<br>

<h3>The Scale</h3>
---
<br>
Tackling the sheer volume of time-series variables and the associated variety and data quality issues remain as the significant challenge in forecasting problems. The number of time-series variables can range from tens of tens to tens of thousands to tens of millions. This post addresses the scale of devising an appropriate framework to train and interpret models for each variable when there are several variables. The scale of engineering a distributed computing system for fast and efficient model training shall be addressed in a different post in future.

The brute force approach is to use an AutoMLesque time-series forecasting package for all variables, given one has the luxury of hardware. Such a package would select the best performing model for each variable and doing so would have solved only half the problem. Often, accuracy alone is not sufficient to justify interpretability of models. A robust forecasting framework has to embody accuracy as well as interpretability. To build one, data scientists can replicate the cinematic music production technique. 

<h3>The technique</h3>
---
<br>
In cinematic music production, a theme song is composed to be the signature music associated to the overall story. Specific tracks are composed for prominent locations or characters in the story. For each scene, the music will be a mix of theme song and character/ location tracks. The duration of score will not scale proportionally with the duration of movie. To replicate this technique, Data Scientists need to identify the theme of the forecasting problem at hand and map time-series variables into few relatable characters. 

The theme of the forecasting problem can be defined by answering the following questions:
<ul>
	<li>Meaningful history</li>
	<li>Zeroes vs Missing values</li>
	<li>Suitable validation rule book</li>
</ul> 
<br>
Select a tab to view relevant information
<div class="tab">
  <button class="tablinks2" onclick="showTabContent2(event, 'History')" id="defaultOpen2">History</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Zeroes & Missing values')">Zeroes vs Missing values</button>
  <button class="tablinks2" onclick="showTabContent2(event, 'Validation')">Validation</button>
</div>

<div id="History" class="tabcontent2" checked="true">
  <p>
  Meaningful history is the amount of historical data suitable and useful for training. This parameter can be determined using grid search which will be computationally expensive at scale. However, given the dynamic nature of most businesses, there can be multiple changepoints in the time-series. The frequency of changepoints needs to be assessed for determining an appropriate start. If there are multiple valid starts to choose from, then grid search can be applied to select one.  
  <br><br>
  A classic example is a stock-price prediction problem with years of data available but not useful in entirety for predicting future prices. In another situation with an objective of predicting user footprint volume, the definition of user footprints could change with time, implying not all historical observations are useful for training.
  <br><br>
  <img src="/assets/stock_images/data_science/time-series/forecasting-at-scale/history.png">
  <br><br>
  These are the problems faced when data is abundant. If it is not, the models will be subject to high bias or variance. To prove or disprove that, business-driven definition of meaningful history can be helpful. Also, it is a good practice to include a few rule-based and naive algorithms in the AutoML package to deal with varying data sizes.

 
  </p>
</div>

<div id="Zeroes & Missing values" class="tabcontent2">
  <p>
  The rationale behind the presence of missing values needs to be investigated to decide on the right treatment procedure. It is further more important to differentiate zeroes from missing values in the context of business. 
  <br><br>
  In weather forecasting, a value of zero is possible and different from missing values. The missing values would have appeared due to equipment failure or data loss among a multitude of reasons. In such cases, they have to be treated differently from zeroes. Consider a demand forecasting problem where zero demand indicates no demand. Here, zeroes may have the same meaning as the missing values do and they can be treated similarly.
  <br><br>
  Missing values represent the intermittency of time-series and their treatment will alter its distribution. The models aren't trained with right data if zeroes and missing values are treated inappropriately.
  <br><br>
  <img src="/assets/stock_images/data_science/time-series/forecasting-at-scale/zeroes.png">
  </p> 
</div>

<div id="Validation" class="tabcontent2">
  <p>
   A right validation procedure for a forecasting framework quantifies its potential to solve the business problem. The validation can be done right by approximating the business problem as a real-valued function of time-series variables. The uncertainity associated with the values of this function is derivable from the individual model errors.

  <br><br>
  For time-series variables, there are several metrics to evaluate accuracy. Sometimes, MAPE is more suitable if the error needs to be quantified on a relative scale. However, MABS can be more meaningful in situations where MAPE will be consistently larger due to the scale of values. A combination of traditional accuracy metrics shall be robust enough for any variable irrespective of its distribution. The uncertainity associated with the function of time-series variables can be estimated by applying the theory of random variables or simpler heuristics.

  <br><br>
   Consider a hierarchical forecasting problem where the volume of units sold is forecasted with an objective of estimating cumulative revenue. The errors made by the individual models can be small, but the error made on revenue estimation by adding the individual predictions is unknown. Also, scale of unit-volumes might significantly differ from the scale of revenues. Traditional accuracy metrics like MAPE might get enlarged or shrunk in translation if the relationship between unit-volume and revenue is not linear. Unless computed, the performance of individual models cannot be correlated with the performance of forecasting system.
  
  <br><br>
  Moreover, the validation procedure is not straight-forward in time-series forecasting, with the notion of k-fold cross validation being invalid. There will be a few data transformation steps to be done before training and validation, depending on the model. A detailed post on the model validation in time-series forecasting shall be published soon.
  <br><br>
  <img src="/assets/stock_images/data_science/time-series/forecasting-at-scale/validation.png"> 
  </p>

</div>

<script type="text/javascript">document.getElementById("defaultOpen2").click();</script><br> 
The answers to these three questions signify the action plan for treatment of historical data and validation of forecast accuracy. This is the act of composing the theme song. The next step is the composition of character specific tunes.

<h3>Time-series classification</h3>
---
<br>
Before unleashing the AutoML, the time-series variables can be classified into a few characters based on their properties. Time-series clustering is a paradigm with ample scope for application of sophisticated algorithms. But the grounded approach presented in Croston et al (2004) is practical in a lot of situations, runs in a flash and comprehensible for business leaders. Let's fire up the hardware during model training, shall we?

<a href="https://www.researchgate.net/profile/Rob-Hyndman/publication/222105798_A_note_on_the_categorization_of_demand_patterns/links/53eb3d2c0cf28f342f452219/A-note-on-the-categorization-of-demand-patterns.pdf">Croston et al (2004)</a> classifies the time-series variables based on their intermittency and variance. The metrics to quantify intermittency and variance are:
* <text style="color: #606060;">Average demand interval (ADI)</text>
* <text style="color: #606060;">Coefficient of Variation squared (CV<sup>2</sup>)</text>

Average demand interval is the ratio of total number of timestamps in the observation period to the number of timestamps with non-null values. Coefficient of Variation (squared) is the squared ratio of standard deviation to the mean of observations that are not nulls. 

Null values are present in time-series when no real-value has been observed at certain timestamps. The presence of missing values due to data loss or observational failure is a different situation that has to be dealt through imputation.

The time-series variables shall be classified as illustrated below:

![framework](/assets/stock_images/data_science/time-series/forecasting-at-scale/ts_classification.png)

The boundary conditions on ADI and CV<sup>2</sup> are mathematically dervied and stastically tested with 3000 time-series. They can be modified to have fewer time-series classified smooth or intermittent. The following tabs describe the practicality of this classification: 

<div class="tab">
  <button class="tablinks" onclick="showTabContent(event, 'Smooth')" id="defaultOpen">SMOOTH</button>
  <button class="tablinks" onclick="showTabContent(event, 'Intermittent')">INTERMITTENT</button>
  <button class="tablinks" onclick="showTabContent(event, 'Erratic')">ERRATIC</button>
  <button class="tablinks" onclick="showTabContent(event, 'Lumpy')">LUMPY</button>

</div>
<div id="Smooth" class="tabcontent">
  <p>A time-series is smooth if its ADI <= 1.32 and CV<sup>2</sup> <= 0.49. The conditions imply the small variance and presence of nearly no null values in the time-series. Traditional forecasting models can achieve high prediction accuracy over smooth time-series. The plot below shows a time-series which is smooth:</p>
  <iframe width="718" height="450" frameborder="0" scrolling="no" src="//plotly.com/~imsskiran/6.embed"></iframe>

  <p>The AutoML can be configured to have predominatly more traditional algorithms for smooth time-series. As a step further, smooth can classified into "very smooth", "quite smooth" and "barely smooth" sub-classes based on CV<sup>2</sup>. This sub-classification enhances the model selection further as superior forecasting models with capability to learn strong seasonal effects are only ever required for the last two sub-classes.
  <br><br>
  Facebook's Prophet with its seasonality and holiday components is a flexible formulation to tackle a range of predictable seasonal/ cyclic effects. A combination of STL decomposition, Auto-ARIMA and variants of Prophet (mild, moderate and strong seasonal effects) shall be robust enough to tame the variances in smooth time-series.
  </p> 
</div>

<div id="Intermittent" class="tabcontent">
  <p>A time-series is intermittent if the ADI > 1.32 and CV<sup>2</sup> <= 0.49. The conditions imply the small variance but presence of significant number of null values in the time-series. Traditional forecasting models capable of dealing intermittency can achieve reasonable prediction accuracy. The plot below shows a time-series which is intermittent:</p>
  <iframe width="718" height="450" frameborder="0" scrolling="no" src="//plotly.com/~imsskiran/12.embed"></iframe>
  <br><br>
  <p>Even for intermittent time-series, the AutoML can be configured to have more traditional algorithms than sophisticated ones. The sub-classification into "very intermittent", "quite intermittent" and "barely intermittent" shall be based on ADI. Superior traditional algorithms are required only for the first two sub-classes. A combination of Croston's model and variants of Prophet shall be sufficient for intermittent time-series.
  </p> 
</div>

<div id="Erratic" class="tabcontent">
 <p>A time-series is erratic if its ADI <= 1.32 and CV<sup>2</sup> > 0.49. The conditions imply the high variance and presence of nearly no null values in the time-series. The high variance could not be explainable by time dimension alone and hence it is generally not possible to achieve a reasonable prediction accuracy with traditional forecasting models. The plot below shows a time-series which is erratic:</p>
 <iframe width="718" height="450" frameborder="0" scrolling="no" src="//plotly.com/~imsskiran/18.embed"></iframe>

 <p>For erratic time-series, advanced time-series clustering algorithms are required for further sub-classification. The AutoML package can be configured to activate several neurons. This is the paradigm to unleash the RNNs, autoencoders and the likes. Moreover, the varinace may not be largely explainable by time and usage of external regressors can improve accuracy further. The next section briefly explains the addition of external regressors to forecasting models. 
 <br><br>
 Google debuted a time-series AutoML package in 2020 backed with a tall claim that it outperforms 92% of hand-crafted models for several kaggle datasets. Facebook debuted NeuralProphet, the gen-next update to the proven Prophet model. Given the availability of hardware, a combination of Google AutoML and NeuralProphet shall be a force to reckon with for erratic time-series. 
 <br><br>
 Although, Google and Facbook termed the compute costs to be moderate, such claims will always remain subjective. But selective application of AutoML and NeuralProphet for erratic time-series will reduce the hardware requirement further.</p>
</div>
<div id="Lumpy" class="tabcontent">
 <p>A time-series is lumpy if its ADI > 1.32 and CV<sup>2</sup> > 0.49. The conditions imply the high variance but presence of significant number of null values in the time-series. There is too much variation and too little data to achieve a reasonable prediction accuracy. The plot below shows a time-series which is lumpy:</p>
 <iframe width="718" height="450" frameborder="0" scrolling="no" src="//plotly.com/~imsskiran/10.embed"></iframe>

 <p>For lumpy time-series, it's either the rule-based/naive or the black-box algorithms that can learn some pattern from the sparse observations. A combination of Croston's model, Google AutoML and NeuralProphet shall be robust enough for this class.</p>
</div>

<script type="text/javascript" src="/assets/js/main.js"></script>
<script type="text/javascript">document.getElementById("defaultOpen").click();</script>
<br>

All in all, time-series classification is a divide and conquer design pattern for forecasting at scale. It not only optimizes runtime & memory but also enhances the overall interpretability of the forecasting framework. The classification of time-series variables is the act of associating them with 4-10 characters. Configuration of AutoML for each sub-class is the act of composing tunes for each character. 

<h3>The Framework</h3>
---
<br>
The illustration below summarises the framework for mixing the theme song and the character tracks. This forecasting framework is scalable along its length and breadth. It is applicable for any number of time-series variables and its robustness shall be further enhanced with selective addition of more suitable algorithms without raising the compute costs on a disproportionate scale. 

![framework](/assets/stock_images/data_science/time-series/forecasting-at-scale/the_framework.png)

<br>
<h3>Epilogue</h3>
<em>This is the framework my use case deserves,</em><br>
<em>but not the one it needs right now.</em><br>

<em>So, I have pinned it to a blog post,</em><br>
<em>so that someone will use it</em><br>

<em>because it's not just a framework,</em><br>
<em>it's a silent predictor, a watchful detector,</em><br>
<em><strong>A Dark Knight!</strong></em>

