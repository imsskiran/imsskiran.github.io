---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---
<!-- <meta name="viewport" content="width=device-width, initial-scale=1"> -->
<style>
/** {box-sizing: border-box}*/
body {font-family: Verdana, sans-serif; margin:0}
.mySlides {display: none}
/*img {vertical-align: middle;}*/

/* Slideshow container */
.slideshow-container {
  /*max-width: 1000px;*/
  position: relative;
  margin: auto;
}

/* Next & previous buttons */
.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  padding: 16px;
  margin-top: -22px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

/* Position the "next button" to the right */
.next {
  right: 0;
  border-radius: 3px 0 0 3px;
}

/* On hover, add a black background color with a little bit see-through */
.prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.5);
}

/* Caption text */
.text {
  color: #ffffff;
  font-size: 2vw;
  padding: 8px 12px;
  position: absolute;
  bottom: 8px;
  width: 100%;
  text-align: left;
}

/* Number text (1/3 etc) */
.numbertext {
  color: #f2f2f2;
  font-size: 15px;
  padding: 8px 12px;
  position: absolute;
  top: 0;
}

/* The dots/bullets/indicators */
.dot {
  cursor: pointer;
  height: 15px;
  width: 15px;
  margin: 0 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.active, .dot:hover {
  background-color: #717171;
}

/* Fading animation */
.fade {
  -webkit-animation-name: fade;
  -webkit-animation-duration: 2s;
  animation-name: fade;
  animation-duration: 2s;
}

@-webkit-keyframes fade {
  from {opacity: .4} 
  to {opacity: 1}
}

@keyframes fade {
  from {opacity: .4} 
  to {opacity: 1}
}

/* On smaller screens, decrease text size */
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
  padding: 0 3.5px;
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

<!-- Slideshow container -->


<div class="slideshow-container">
<a href="/about/">
<div class="mySlides fade">
  <!-- <div class="numbertext">Trending</div> -->
  <img src="/assets/logo_chop.png" style="width:100%">
  <!-- <div class="text">Welcome</div> -->
</div></a>

<a href="/time-series/time-series-primer/">
<div class="mySlides fade">
  <div class="numbertext">New</div>
  <img src="/assets/stock_images/data_science/time-series/time-series-101/thumbnail.png" style="width:100%">
  <div class="text"><strong>Time-series fundamentals explained like never before</strong></div>
</div></a>

<a href="/time-series/forecasting-at-scale/">
<div class="mySlides fade">
  <div class="numbertext">New</div>
  <img src="/assets/stock_images/data_science/time-series/forecasting-at-scale/thumbnail.png" style="width:100%">
  <div class="text"><strong>The art of composing time-series music</strong></div>
</div></a>

<a href="/running-your-first-business/">
<div class="mySlides fade">
  <div class="numbertext">New</div>
  <img src="/assets/stock_images/ryfb/thumbnail.png" style="width:100%">
  <div class="text"><strong>Discover the measurement way of life</strong></div>
</div></a>

<a class="prev" onclick="plusSlides(-1)">&#10094;</a>
<a class="next" onclick="plusSlides(1)">&#10095;</a>
<a class="next" onclick="plusSlides(1)">&#10095;</a>
<a class="next" onclick="plusSlides(1)">&#10095;</a>



</div>
<br>

<div style="text-align:center">
  <span class="dot" onclick="currentSlide(1)"></span> 
  <span class="dot" onclick="currentSlide(2)"></span> 
  <span class="dot" onclick="currentSlide(3)"></span>
  <span class="dot" onclick="currentSlide(4)"></span> 
</div>

<script>
var slideIndex = 0;
showSlides();

function showSlides() {
  var i;
  var slides = document.getElementsByClassName("mySlides");
  var dots = document.getElementsByClassName("dot");
  for (i = 0; i < slides.length; i++) {
    slides[i].style.display = "none";  
  }
  slideIndex++;
  if (slideIndex > slides.length) {slideIndex = 1}    
  for (i = 0; i < dots.length; i++) {
    dots[i].className = dots[i].className.replace(" active", "");
  }
  slides[slideIndex-1].style.display = "block";  
  dots[slideIndex-1].className += " active";
  setTimeout(showSlides, 5000); // Change image every 2 seconds
}

function currentSlide(n) {
  showSlides2(slideIndex = n);
}

function plusSlides(n) {
  showSlides2(slideIndex += n);
}

function showSlides2(n) {
  var i;
  var slides = document.getElementsByClassName("mySlides");
  var dots = document.getElementsByClassName("dot");
  if (n > slides.length) {slideIndex = 1} 
  if (n < 1) {slideIndex = slides.length}
  for (i = 0; i < slides.length; i++) {
      slides[i].style.display = "none"; 
  }
  for (i = 0; i < dots.length; i++) {
      dots[i].className = dots[i].className.replace(" active", "");
  }
  slides[slideIndex-1].style.display = "block"; 
  dots[slideIndex-1].className += " active";
}
</script>


<!-- <br>
<h3>Trending</h3>
<ul class="post-list"><li><span class="post-meta">Dec 18, 2020</span>
        <h3>
          <a class="post-link" href="/running-your-first-business/">
            Running Your First Business
          </a>
        </h3></li>
</ul>
<br>

<!-- --- -->
<br>
<h3>Explore the posts</h3>
<div class="row"> 
  <div class="column">
    <a href="/data-science/"><img src="/assets/stock_images/data_science.png"></a>
    <a href="/automobiles/"><img src="/assets/stock_images/automobiles.png"></a>
    <a href="/personal-tech/"><img src="/assets/stock_images/personal_tech.png"></a>
  </div>
  <div class="column">
    <a href="/lorgs/"><img src="/assets/stock_images/lorgs.png"></a>
    <a href="/wildlife/"><img src="/assets/stock_images/wildlife.png"></a>
    <a href="/posts/"><img src="/assets/stock_images/browse_all.png"></a>
  </div> 
</div>
<!-- <p float="centre">
  <a href="/data-science/"><img src="/assets/stock_images/data_science.png" width="367" height="166" hspace="0.75" object-fit="contain"/></a>
  <a href="/indian-railways/"><img src="/assets/stock_images/indian_railways.png" width="367" height="166" hspace="0" object-fit="contain"/></a>
</p>
<p float="centre">
  <a href="/wildlife/"><img src="/assets/stock_images/wildlife.png" width="367" height="166" hspace="0.75"/></a>
  <a href="/personal-tech/"><img src="/assets/stock_images/personal_tech.png" width="367" height="166" hspace="0"/></a> 
</p>
<p float="centre">
  <a href="/automobiles/"><img src="/assets/stock_images/automobiles.png" width="367" height="166" hspace="0.75"/></a>
  <a href="/posts/"><img src="/assets/stock_images/browse_all.png" width="367" height="166" hspace="0"/></a> 
</p> -->

