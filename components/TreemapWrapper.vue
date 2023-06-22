<template>
  <div id="titles" class="Treemap_wrapper mt-28 pb-28">
    <div class="grid grid-cols-6 gap-y-1">
      <div class="col-span-2">
        <h1 class="headline-treemap">Wie heißt ein guter Wein?</h1>
        <p id="description">
          "Lisa" sucht als nächstes nach einer passenden Flasche Wein. Doch was
          steht eigentlich auf einer guten Flasche Wein? Die hier dargestellte
          Grafik zeigt die 30 beliebtesten Begriffe, welche laut den
          ausgewerteten Reviews auf einem Etikett stehen können.
          <span class="disclosure">
            <br /><br />
            Für die Darstellung wurden nur die 120 Begriffe, welche am
            häufigsten auf Weinetiketten vorkommen ausgewertet, um keine Namen
            einzelner (herausragender) Weine zu verwenden. Darüber hinaus wurden
            Füllwörter und Rebsorten aussortiert.
          </span>
        </p>

      </div>
      <div class="col-span-4">
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
    </div>
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
/* Background Color*/
.Treemap_wrapper {
  padding-left: 20%;
  padding-right: 2%;
}
#description {
  height: 100%;
  padding: 1rem;
  margin-bottom: 1rem;
}
.headline-treemap {
  padding-top: 20px;
  padding-bottom: 20px;
  line-height: 1;
  font-size: 4rem;
  font-weight: bold;
}
.disclosure {
  font-size: 0.7rem;
  font-style: italic;
  color: #6e7b90;
}
</style>
