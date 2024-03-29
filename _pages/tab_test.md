---
layout: page
permalink: /tab-test/
---

<style>
/*body {font-family: Arial;}*/

/* Style the tab */
.tab {
  overflow: hidden;
  border: 0px solid #ccc;
  background-color: #f1f1f1;
  width: 723px;
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
  -webkit-animation: fadeEffect 1s;
  animation: fadeEffect 1s;
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
