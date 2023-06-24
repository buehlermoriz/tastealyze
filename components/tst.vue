<template>
  <div class="md:ml-[20%] mx-[5%]">
    <div class="grid md:gap-16 grid-cols-3 md:grid-cols-9">
      <div id="Weißwein" class="col-span-1 flex justify-center">
        <img
          :class="{ 'active-bottle': active === 'Weißwein' }"
          @click="updateActive('Weißwein')"
        />
      </div>
      ...
      <div class="col-span-6 mt-32 md:mt-0 mr-5 mb-20">
        <h2 class="text-2xl mb-5">{{ active }}</h2>
        <p class="mb-5">{{ getText(active) }}</p>
        <GrapeCarousel
          @updateGrape="handleUpdateGrape"
          :key="watchChanges"
          :wine-type="active"
        />
        <RadarChart
          @updateData="handleUpdateData"
          :key="watchChanges"
          :wine-type="active"
          :grape-type="grape"
          :lastData="lastRadarChart"
        />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      lastRadarChart: null,
      active: "Rotwein",
      grape: "",
      watchChanges: 0,
      textMap: {
        Rotwein: "text for Rotwein",
        Weißwein: "text for Weißwein",
        Roséwein: "text for Roséwein",
      },
    };
  },
  methods: {
    updateActive(id) {
      this.active = id;
    },
    getText(id) {
      return this.textMap[id] || "";
    },
    handleUpdateGrape(grape) {
      this.grape = grape;
    },
    handleUpdateData(lastRadarChart) {
      this.lastRadarChart = lastRadarChart;
    },
    newActive() {
      this.watchChanges++;
    },
  },
  watch: {
    active: newActive(),
    grape: newActive(),
  },
};
</script>
