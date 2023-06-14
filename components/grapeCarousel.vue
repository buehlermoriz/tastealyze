<template>
  <Carousel v-bind="settings" :breakpoints="breakpoints">
    <Slide v-for="slide in names" :key="slide">
      <div class="carousel__item my-10">
        <div class="flex justify-center">
          <img
            :src="loaderPath(slide)"
            class="mx-auto my-auto max-h-[100px]"
            @click="emitValue(slide)"
            @mouseenter="handleMouseEnter"
          @mouseleave="handleMouseLeave"
          />
        </div>
        <!-- send value to top component -->
        <p class="hidden absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center text-xl text-gray-800">
            {{ slide }}</p>
      </div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>

<script>
import { Carousel, Navigation, Slide } from "vue3-carousel";

import "vue3-carousel/dist/carousel.css";

export default {
  props: {
    wineType: {
      type: String,
      required: true,
      validator: (value) => ["Weißwein", "Rotwein", "Roséwein"].includes(value),
    },
  },
  name: "Breakpoints",
  components: {
    Carousel,
    Slide,
    Navigation,
  },
  data() {
    return {
      names: [],
      isHovered: false,
      // carousel settings
      settings: {
        itemsToShow: 1,
        snapAlign: "center",
      },
      breakpoints: {
        // 700px and up
        700: {
          itemsToShow: 3,
          snapAlign: "center",
        },
        // 1024 and up
        1024: {
          itemsToShow: 5,
          snapAlign: "start",
        },
      },
    };
  },
    computed: {

  },
  methods: {
    loaderPath(slide){
        return "/img/grapes/"+slide+".jpg"
    },
    emitValue(value) {
      this.$emit("updateGrape", value);
    },
    handleMouseEnter() {
      this.isHovered = true;
    },
    handleMouseLeave() {
      this.isHovered = false;
    },
  },
  mounted() {
    switch (this.wineType) {
      case "Weißwein":
        this.names = [
          "Chardonnay",
          "Sauvignon blanc",
          "Andere Weine",
          "Riesling",
          "Moscato",
          "Semillon",
          "Blend",
          "Viognier",
          "Trebbiano",
          "Pinot Grigio",
          "Gewurztraminer",
          "Garganega",
          "Pinot Gris",
          "Grenache Blanc",
          "Chenin Blanc",
          "Vermentino",
          "Cortese",
          "Marsanne",
          "Airen",
          "Rousaanne",
          "Viura",
          "Macabeo",
          "Verdejo",
          "Vidal",
          "Aligote",
          "Gruner Veltliner",
          "Furmint",
          "Muscat",
          "Malvasia",
          "Zinfandel",
          "Grenache",
          "Pinot Noir",
          "Cabernet Sauvignon",
          "Carignan",
          "Merlot",
          "Garnacha",
          "Corvina",
        ];
        break;
      case "Rotwein":
        this.names = [
          "Cabernet Sauvignon",
          "Merlot",
          "Pinot Noir",
          "Syrah & Shiraz",
          "Sangiovese",
          "Andere Weine",
          "Tempranillo",
          "Nebbiolo",
          "Blend",
          "Grenache",
          "Malbec",
          "Carmenere",
          "Barbera",
          "Zinfandel",
          "Montepulciano",
          "Nero d'Avola",
          "Corvina",
          "Monastrell",
          "Gamay",
          "Cabernet Franc",
          "Dolcetto",
          "Bordeaux Blend Red",
          "Sangiovese Grosso",
          "Carignan",
          "Garnacha",
          "Malvasia",
          "Furmint",
          "Chardonnay",
          "Muscat",
          "Andere Weine",
        ];
        break;
      case "Roséwein":
        this.names = [
          "Andere Weine",
          "Grenache",
          "Zinfandel",
          "Syrah & Shiraz",
          "Pinot Noir",
          "Cabernet Sauvignon",
          "Blend",
          "Merlot",
          "Moscato",
          "Tempranillo",
          "Sangiovese",
          "Garnacha",
          "Cabernet Franc",
          "Montepulciano",
          "Malbec",
          "Pinot Grigio",
          "Monastrell",
          "Malvasia",
          "Muscat",
          "Carmenere",
          "Corvina",
          "Gamay",
          "Pinot Gris",
          "Nebbiolo",
          "Sauvignon blanc",
          "Carignan",
          "Chardonnay",
        ];
        break;
    }
  },
};
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap');
.carousel__item {
  position: relative;
}

.carousel__item img {
  transition: opacity 0.3s ease;
}

.carousel__item:hover img {
  opacity: 0.4;
}

.carousel__item:hover p {
  display: block;
}
.font-dancing-script {
  font-family: 'Dancing Script', cursive;
}
</style>