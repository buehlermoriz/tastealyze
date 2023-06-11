<template>
  <div id="wineselector">
    <div class="ml-[20%]">
      <div class="my-8">
        <h1 class="font-semibold uppercase md:text-5xl font-['Bodoni MT']">
          wähle deinen Wein
        </h1>
      </div>
      <div class="grid gap-16 grid-cols-9">
        <div id="Weißwein" class="col-span-1 flex justify-center">
          <img
            src="../assets/bottles/whitewine.png"
            class="mx-auto my-auto max-h-[300px]"
            :class="{ 'active-bottle': active === 'Weißwein' }"
            @click="updateActive('Weißwein')"
          />
        </div>
        <div id="Rotwein" class="col-span-1 flex justify-center">
          <img
            src="../assets/bottles/redwine.png"
            class="mx-auto my-auto max-h-[600px]"
            :class="{ 'active-bottle': active === 'Rotwein' }"
            @click="updateActive('Rotwein')"
          />
        </div>
        <div id="Roséwein" class="col-span-1 flex justify-center">
          <img
            src="../assets/bottles/rosewine.png"
            class="mx-auto my-auto max-h-[300px]"
            :class="{ 'active-bottle': active === 'Roséwein' }"
            @click="updateActive('Roséwein')"
          />
        </div>
        <div class="col-span-6 mr-5">
          <h2 class="text-2xl mb-5">{{ active }}</h2>
          <p class="mb-5">{{ getText(active) }}</p>
          <GrapeCarousel />
          <div class="grid gap-5 grid-cols-6">
            <div class="col-span-1">
              <button @click="updateGrape('Merlot')">Merlot</button>
            </div>
          </div>
          <RadarChart :key="watchChanges" :wine-type="active" :grape-type="grape" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      active: "Rotwein",
      grape: "",
      watchChanges: 0,
      textMap: {
        Rotwein:
          "Rotwein ist bekannt für seine tiefe, rötliche Farbe und seinen komplexen Geschmack. Er wird aus dunklen Trauben hergestellt und durchläuft einen Fermentationsprozess, bei dem die Traubenschalen für eine gewisse Zeit in Kontakt mit dem Saft bleiben. Dadurch erhält der Rotwein seine charakteristische Farbe und seine tanninhaltige Struktur. Die Aromen von Rotwein reichen von dunklen Früchten wie schwarzen Kirschen und Beeren bis hin zu würzigen Noten wie Vanille, Zimt und schwarzen Pfeffer. Der Körper von Rotwein ist in der Regel vollmundig und kann je nach Reifegrad und Herstellungsstil von weich bis kräftig variieren. Rotwein hat oft ein Alterungspotenzial und kann mit der Zeit an Komplexität und Tiefe gewinnen.",
        Weißwein: "Weißwein ist bekannt für seine helle Farbe und seinen frischen, lebendigen Charakter. Im Gegensatz zu Rotwein werden für die Herstellung von Weißwein hauptsächlich helle Trauben verwendet, bei denen die Schalen nicht in Kontakt mit dem Saft bleiben. Dadurch behält der Weißwein seine helle Farbe bei und hat eine weniger tanninhaltige Struktur im Vergleich zu Rotwein. Weißwein zeigt oft Aromen von Zitrusfrüchten wie Zitronen und Limetten, tropischen Früchten wie Ananas und Pfirsichen sowie blumigen Noten wie Jasmin und Akazien. Der Körper von Weißwein variiert von leicht und erfrischend bis hin zu vollmundig und cremig, je nach Rebsorte und Ausbauart. Weißweine werden in der Regel jung getrunken und sind für ihren lebendigen Charakter und ihre knackige Säure bekannt.",
        Roséwein: "Roséwein ist für seine rosa bis hellrote Farbe und seine erfrischende Natur bekannt. Roséwein wird aus dunklen Trauben hergestellt, bei denen die Schalen nur für eine kurze Zeit in Kontakt mit dem Saft bleiben, was zu einer geringeren Extraktion von Farbstoffen und Tanninen führt. Dadurch erhält der Roséwein seine charakteristische helle Farbe und seinen leichteren Körper im Vergleich zu Rotwein. Roséweine bieten eine Vielfalt an Aromen, von frischen roten Beeren wie Erdbeeren und Himbeeren bis hin zu blumigen und würzigen Noten. Roséweine sind bekannt für ihre erfrischende Säure und ihren leichten, zugänglichen Charakter. Sie werden oft gut gekühlt serviert und sind eine beliebte Wahl für sommerliche Gelegenheiten und leichte Speisen.",
      },
    };
  },
  methods: {
    updateActive(id) {
      this.active = id;
    },
    updateGrape(grape) {
      this.grape = grape;
    },
    getText(id) {
      return this.textMap[id] || "";
    },
  },
  //increase watchChanges, to trigger a reload of the radar chart on both variables active and grape
  watch: {
    active: function (newActive) {
      this.watchChanges++;
    },
    grape: function (newGrape) {
      this.watchChanges++;
    },
  },
};
</script>
<style>
.active-bottle {
  transform: scale(1.6);
  transition: transform 1s ease;
}
</style>
