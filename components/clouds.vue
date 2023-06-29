<template>
  <div id="wordcloud" class="pb-14 pt-8  md:ml-[20%] md:mt-20 md:grid text-center">
    <div class="md:grid md:grid-cols-6 md:gap-y-1 mt-5">
      <div class="md:col-span-3 my-5">
        <h3 class="font-semibold uppercase text-2xl md:text-3xl">
          Wein <span class="text-red-800">unter </span> 80 Punkte:
        </h3>
        <!-- Wordcloud =80 Points -->
        <Wordcloud :key="componentKey" :color="'red'" :cloudnr="0" :keywords="badWines" />
      </div>
      <div class="md:col-span-3 my-5">
        <h3 class="font-semibold uppercase text-2xl md:text-3xl">
          Wein <span class="text-green-900">über </span> 80 Punkte:
        </h3>
        <!-- Wordcloud >80 Points-->
        <Wordcloud :key="componentKey" :color="'green'" :cloudnr="1" :keywords="goodWines" />
      </div>
    </div>
  </div>
</template>
<script>
import { badWines } from "@/assets/badwines.js";
import { goodWines } from "@/assets/goodwines.js";

export default {
  data() {
    return {
      badWines: badWines,
      goodWines: goodWines,
      componentKey: 0,
    };
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  methods: {
    handleResize() {
      this.componentKey += 1;
    },
  },
};
</script>
