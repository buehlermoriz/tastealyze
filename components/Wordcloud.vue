<template>
  <!-- Wordcloud-->
  <div id="wordcloud" class="wordcloud pt-8">
    <vue-word-cloud
      style="
        height: 576px;
        width: 600px;
      "
      :words="keywords"
      :color="color_scheme"
      font-family="Roboto"
      :spacing="0.5"
    />
  </div>
</template>

<script>
import VueWordCloud from 'vuewordcloud';

export default {
  components: {
    [VueWordCloud.name]: VueWordCloud,
  },
  data() {
    return {
      color_scheme: null,
    };
  },
  mounted() {
    if (this.color === 'red') {
      this.color_scheme = ([, weight]) =>
        weight > 0.4 ? '#800000' : weight > 0.2 ? '#B80F0A' : '#555555';
    }

    if (this.color === 'green') {
      this.color_scheme = ([, weight]) =>
        weight > 0.4 ? '#0f4336' : weight > 0.2 ? '#556B2F' : '#555555';
    }
  },
  props: ['keywords', 'color'],
};
</script>

<style>
.wordcloud {
  display: flex;
  justify-content: center;
  align-items: center;
  /* height: 100%; */
  width: 100%;
}
</style>
