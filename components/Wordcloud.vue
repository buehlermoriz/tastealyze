<<<<<<< HEAD
<!--<template>
 Wordcloud 
<vue-word-cloud
  style="
    height: 480px;
    width: 640px;
  "
  :words="[['romance', 19], ['horror', 3], ['fantasy', 7], ['adventure', 3]]"
  :color="([, weight]) => weight > 10 ? 'DeepPink' : weight > 5 ? 'RoyalBlue' : 'Indigo'"
  font-family="Roboto"
/>
=======
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
      spacing=0.5
    />
</div>
>>>>>>> wordcloud
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
<<<<<<< HEAD
</script>-->
=======
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
>>>>>>> wordcloud
