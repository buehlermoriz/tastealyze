<template>
    <div class="ml-[20%] py-10 bg-gray-500 text-center">
        {{ text }}
        <div class="ml-[20%]"></div>
        <img :src="loaderPath" autoplay loop class="" />
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
      if(process.env.NODE_ENV === "development"){
        return "/_nuxt/assets/bottles/"+this.img+".png"
      }
    //   else{
    //     if(this.wineType === "Roséwein"){
    //       return "/_nuxt/Rosewein.f57f7c8b.gif"
    //     }
    //     else if (this.wineType === "Rotwein"){
    //       return "/_nuxt/Rotwein.efba7540.gif"
    //     }
    //     else{
    //       return "/_nuxt/Weißwein.1ba14fd2.gif"
    //     }
    //   }
      
    }
  },
}
</script>