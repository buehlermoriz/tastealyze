<template>
    <div class="slider-container">
      <div class="slider">
        <div class="slide" v-for="(slide, index) in slides" :key="index">
          <img :src="slide.image" @click="wipeSlide(index)" :class="{ wiped: slide.wiped }" />
        </div>
      </div>
      <div class="text-container">
        <div class="text" v-for="(slide, index) in slides" :key="index" :class="{ active: slide.wiped }">
          {{ slide.text }}
        </div>
      </div>
    </div>
  </template>
  
  <script>
    export default {
  data() {
    return {
      slides: [
        { image: require('../assets/redwine.png'), wiped: false, text: 'Text for Image 1' },
        { image: require('../assets/whitewine.png'), wiped: false, text: 'Text for Image 2' },
        { image: require('../assets/rosewine.png'), wiped: false, text: 'Text for Image 3' }
      ]
    };
  },
    methods: {
      wipeSlide(index) {
        this.slides[index].wiped = true;
      }
    }
  };
  </script>
  
  <style scoped>
  .slider-container {
    display: flex;
  }
  
  .slider {
    width: 50%;
    overflow: hidden;
  }
  
  .slide {
    width: 100%;
    height: 100%;
  }
  
  .slide img {
    width: 100%;
    height: 100%;
    cursor: pointer;
    transition: opacity 0.3s;
  }
  
  .slide img.wiped {
    opacity: 0.5;
  }
  
  .text-container {
    width: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  
  .text {
    display: none;
  }
  
  .text.active {
    display: block;
  }
  </style>