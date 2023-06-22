<template>
  <div class="mx-[5%] md:ml[20%] mt-28 pb-28">
    <div class="md:grid md:grid-cols-6 md:gap-y-1">
      <div class="md:col-span-2">
        <h1 class="text-2xl md:text-5xl">Wie heißt ein guter Wein?</h1>
        <p>
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
      <div class="md:col-span-4">
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

.disclosure {
  font-size: 0.7rem;
  font-style: italic;
  color: #6e7b90;
}
</style>
