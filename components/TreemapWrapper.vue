<template>
  <div class="mx-[5%] md:ml-[20%] my-8 flex intems-center justify-center">
        <Treemap
          @treemap_select="handleTreemapSelect"
          url="https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/treemap_points.csv "
          :key="treemap_select"
          :keyword="treemap_select"
        />
        <TreemapDetail
        @treemap_select="handleTreemapSelect"
          url="https://raw.githubusercontent.com/buehlermoriz/tastealyze/treemap_detail/assets/treemap_detail.json"
          :keyword="treemap_select"
          :key="treemap_select"
        />
  </div>
</template>
<script>
export default {
  data() {
    return {
      treemap_select: null,
    };
  },
  methods: {
    handleTreemapSelect(select) {
      this.treemap_select = select;
    },
  },
};
</script>
<style>

.disclosure {
  font-size: 0.7rem;
  font-style: italic;
  color: #6e7b90;
}
</style>
