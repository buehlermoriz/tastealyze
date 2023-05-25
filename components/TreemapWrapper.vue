<template>
  <div class="Treemap_wrapper">
    <div class="grid grid-cols-6 gap-y-1">
      <div class="col-span-2">
        <h1 class="headline-treemap">Wie heißt ein guter Wein?</h1>
        <p id="description">
          "Lisa" sucht als nächstes nach einer passenden Flasche Wein. Doch was
          steht eigentlich auf einer guten Flasche Wein? Die hier dargestellte
          Grafik zeigt die 40 besten Begriffe, welche laut den ausgewerteten
          Reviews auf einem Etikett stehen können.
        </p>
      </div>
      <div class="col-span-4">
        <Treemap
          url="https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/treemap_points.csv"
        />
      </div>
    </div>
  </div>
</template>
<style>
/* Background Color*/
.Treemap_wrapper {
  margin-top: 100px;
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
</style>
