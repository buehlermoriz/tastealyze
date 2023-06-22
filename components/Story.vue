<template>
    <div class="grid grid-cols-6 pl-[5%] md:pl-[20%] pr-[5%] bg-stone-500		">
      <div class="col-span-2">
        <img :src="loaderPath" autoplay loop class="illustration" />
      </div>
      <div class="col-span-4 flex">
        <div class="my-auto ml-5 md:ml-0 text-white md:font-bold	 italic text-lg	md:text-2xl">
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
