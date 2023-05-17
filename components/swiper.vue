<template>
    <div class="slider">
  <div class="slides">
    <div class="slide">
      <img src="https://swiperjs.com/demos/images/nature-1.jpg">
      <div class="text">
        <h2>Slide 1</h2>
        <p>This is the text for slide 1.</p>
      </div>
    </div>
    <div class="slide">
      <img src="https://swiperjs.com/demos/images/nature-2.jpg">
      <div class="text">
        <h2>Slide 2</h2>
        <p>This is the text for slide 2.</p>
      </div>
    </div>
    <div class="slide">
      <img src="https://swiperjs.com/demos/images/nature-3.jpg">
      <div class="text">
        <h2>Slide 3</h2>
        <p>This is the text for slide 3.</p>
      </div>
    </div>
  </div>
  <div class="dots">
    <span class="dot"></span>
    <span class="dot"></span>
    <span class="dot"></span>
  </div>
</div>
  </template>
  <script>
  
  // /pages/payment-page.vue

export default {
  mounted() {

  const slides = document.querySelector('.slides');
const slide = document.querySelectorAll('.slide');
const dots = document.querySelectorAll('.dot');

let currentSlide = 1;

// Clone the first and last slide
const firstClone = slide[0].cloneNode(true);
const lastClone = slide[slide.length - 1].cloneNode(true);

// Append the clones to the beginning and end of the slides
slides.appendChild(firstClone);
slides.insertBefore(lastClone, slide[0]);

// Set the initial position of the slides
slides.style.transform = `translateX(-${currentSlide * 33.33}%)`;

// Add event listeners to the dots
dots.forEach((dot, index) => {
  dot.addEventListener('click', () => {
    currentSlide = index + 1;
    setSlidePosition();
    setActiveDot();
  });
});

// Set the position of the slides based on the current slide
function setSlidePosition() {
  slides.style.transform = `translateX(-${currentSlide * 33.33}%)`;
}

// Set the active dot based on the current slide
function setActiveDot() {
  dots.forEach(dot => {
    dot.classList.remove('active');
  });
  dots[currentSlide - 1].classList.add('active');
}
  }
}
  </script>
    <style>
    .slider {
  position: relative;
  width: 100%;
  height: 500px;
  overflow: hidden;
}

.slides {
  display: flex;
  width: 300%;
  height: 100%;
  transition: transform 0.5s ease-in-out;
}

.slide {
  width: 33.33%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.text {
  position: absolute;
  top: 0;
  right: 0;
  width: 50%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  padding: 20px;
  transition: opacity 0.5s ease-in-out;
  opacity: 0;
}

.slide:hover .text {
  opacity: 1;
}

.dots {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #bbb;
  margin: 0 5px;
  cursor: pointer;
}

.dot.active {
  background-color: #fff;
}
  </style>