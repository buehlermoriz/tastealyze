<template>
  <div class=" pb-14  mt-28 pb-28 grid text-center ">
    <h2 class=" ml-[20%] pt-16 pb-8  font-semibold uppercase md:text-5xl font-['Bodoni MT']">
    Wie werden Weine beschrieben?
  </h2>
    <p class=" ml-[20%] pr-8">
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
    <div class="grid grid-cols-6 gap-y-1">
      <div class="col-span-3" style="margin-left: 350px">
        <h3
          class="font-semibold uppercase md:text-3xl font-['Bodoni MT']"
          style="margin-left: 100px; padding-top: 50px"
        >
          Wein <span class="text-red-800">unter </span> 80 Punkte:
        </h3>
        <!-- Wordcloud =80 Points -->
        <Wordcloud
          :color="'red'"
          :cloudnr="0"
          :keywords="badWines"
        />
      </div>
      <div class="col-span-3" style="margin-right: 150px; margin-left: 200px">
        <h3
          class="font-semibold uppercase md:text-3xl font-['Bodoni MT']"
          style="margin-left: 100px; padding-top: 50px"
        >
          Wein <span class="text-green-900">über </span> 80 Punkte:
        </h3>
        <!-- Wordcloud >80 Points-->
        <Wordcloud
          :color="'green'"
          :cloudnr="1"
          :keywords="goodWines"
        />
      </div>
    </div>
  </div>
</template>
<script>
import { badWines } from '@/assets/badwines.js';
import { goodWines } from '@/assets/goodwines.js';

export default{
  data() {
    return {
      badWines: badWines,
      goodWines: goodWines,
    };
  },
};


</script>
