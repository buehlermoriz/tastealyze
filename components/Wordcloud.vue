<template>
<!-- Wordcloud-->
<div class="wordcloud">
    <vue-word-cloud
      style="
        height: 480px;
        width: 640px;
        "
      :words=keywords
      :color="([, weight]) => weight > 0.4 ? 'DeepPink' : weight > 0.2 ? 'RoyalBlue' : 'Indigo'"
      font-family="Roboto"
      :spacing = 0.5
    />
</div>
</template>
<script>
import VueWordCloud from 'vuewordcloud';
export default {
  components: {
    [VueWordCloud.name]: VueWordCloud,
  },
  props: [
    'keywords'
],
};
</script>
<style>
.wordcloud {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
</style>