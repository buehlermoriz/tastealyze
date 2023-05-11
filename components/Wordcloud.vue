<template>
<!-- Wordcloud-->
<div class="wordcloud pt-8">
    <vue-word-cloud
      style="
        height: 576px;
        width: 1024px;
      "
      :words=keywords
      :color="([, weight]) => weight > 0.4 ? '#7C0A02' : weight > 0.2 ? '#c4c0b9' : '#7e6c65'"
      font-family="Roboto"
      spacing=0.5
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
 /* height: 100%; */
  width: 100%;
}
</style>