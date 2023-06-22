<template>
  <div class="pb-14  md:ml-[20%] md:mt-20 md:grid text-center">
    <h2
      class="mx-[5%] font-semibold uppercase md:text-5xl text-2xl"
    >
      Wie werden Weine beschrieben?
    </h2>
    <p class=" px-[5%] mt-5 md:pr-8">
      Bei Weinproben verwenden Tester verschiedene Wörter, um Weine zu
      beschreiben. Dabei gibt es klare Unterschiede in der Wortwahl, je nachdem,
      ob ein Wein als gut oder schlecht bewertet wird. Die Wahl der Wörter
      spielt eine wichtige Rolle, um die sensorischen Eigenschaften und die
      Gesamtbewertung eines Weins treffend zu beschreiben und den Verbrauchern
      eine Vorstellung davon zu vermitteln, was sie erwarten können. Die
      Weintester von WineEnthusiast konnten dabei bis zu 100 Punkte für einen
      besonders guten Wein vergeben. Im folgenden erfahren Sie, wie gut oder
      schlechter bewertete Weine beschrieben wurden.
    </p>
    <div class="md:grid md:grid-cols-6 md:gap-y-1 mt-5">
      <div class="md:col-span-3 my-5">
        <h3 class="font-semibold uppercase text-2xl md:text-3xl">
          Wein <span class="text-red-800">unter </span> 80 Punkte:
        </h3>
        <!-- Wordcloud =80 Points -->
        <Wordcloud :key="componentKey" :color="'red'" :cloudnr="0" :keywords="badWines" />
      </div>
      <div class="md:col-span-3 my-5">
        <h3 class="font-semibold uppercase text-2xl md:text-3xl">
          Wein <span class="text-green-900">über </span> 80 Punkte:
        </h3>
        <!-- Wordcloud >80 Points-->
        <Wordcloud :key="componentKey" :color="'green'" :cloudnr="1" :keywords="goodWines" />
      </div>
    </div>
  </div>
</template>
<script>
import { badWines } from "@/assets/badwines.js";
import { goodWines } from "@/assets/goodwines.js";

export default {
  data() {
    return {
      badWines: badWines,
      goodWines: goodWines,
      componentKey: 0,
    };
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  methods: {
    handleResize() {
      this.componentKey += 1;
      console.log(this.componentKey);
    },
  },
};
</script>
