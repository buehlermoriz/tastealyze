<template>
  <div class="story_wrapper">
    <div class="grid grid-cols-6 gap-y-1">
      <div class="col-span-2">
        <img :src="loaderPath" autoplay loop class="illustration" />
        
      </div>
      <div class="col-span-4">
        <div class="description">
        {{ text }}
      </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        text: {
            type: String,
            required: true
        },
        img: {
            type: String,
            required: true
        }
    },
    computed: {
    loaderPath(){
        return "/img/story/"+this.img+".svg"
    }
  },
}
</script>
<style>
/* Background Color*/
.story_wrapper {
  padding-left: 20%;
  padding-right: 2%;
  background-color: #898381;
}
.description {
  font-weight: 600;
  font-style: italic;
  font-size: 15pt;
  color: #fff;
  padding-top: 15%;
  margin-left: 5%;
  margin-right: 32%;
}
.illustration{
  height: 220px;
}


</style>
