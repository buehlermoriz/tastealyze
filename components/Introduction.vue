<template>
  <div class="md:h-screen">
    <div
      id="introduction"
      class="w-full md:min-h-full bg-cover"
      :style="`background-image: url(${backgroundImage})`"
    >
      <div class="mx-[5%] pt-5 md:ml-[20%] md:mr-[35%] md:pt-16">
      </div>
    </div>
  </div>
</template>

<script>
import backgroundImage from "~/assets/weinauftuch.jpg";

export default {
  name: "Introduction",
  components: {},
  data() {
    return {
      backgroundImage: backgroundImage,
    };
  },
  mounted() {},
};
</script>
