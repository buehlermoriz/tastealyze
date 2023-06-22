<template>
    <div class="grid grid-cols-6 gap-y-1 pl-[20%] pr-[15%] bg-stone-500		">
      <div class="col-span-2">
        <img :src="loaderPath" autoplay loop class="illustration" />
      </div>
      <div class="col-span-4 flex">
        <div class="my-auto text-white font-bold	 italic	text-2xl">
            {{ text }}
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
.illustration{
  height: 220px;
}


</style>
