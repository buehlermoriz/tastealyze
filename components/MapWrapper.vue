<template>
    <div id="worldmap" class="px-[5%] md:pl-[20%] bg-gray-100 py-28">
        <h1 class="text-2xl md:text-5xl text-center">Globale Unterschiede <br> in der Weinproduktion</h1>
        <p class="text-center" id="description">Diese Grafik zeigt globale Unterschiede in der Weinproduktion. Dabei können Sie aus drei Bereichen auswählen. Mit einer Wahl der durchscnittlichen Punkte erhalten Sie eine Visualisierung wie viele Punkte die Tester den Weinen eines Landes auf einer Skala von 0 bis 1 durchschnittlich gegeben haben. Bei der Auswahl des Preises erhalten sie die durchscnittlichen Preise. Zuletzt lassen sich die Ergebnisse einer Sentimentanalyse darstellen. Hierbei wurden die Texte der Produktbewertungen ausgewertet. Je nach dem wie positiv (oder Negativ) eine Produktbeschriebung ist wurde eine Wert zwischen 0 und 1 ermittelt, welcher auf der Karte dargestellt wird.</p>
        <p class="text-center"> Sie interessieren sich für ein einzelnes Land? Hovern sie einfach mit der Maus über das entpsprechende Land</p>
        <Map />
    </div>
</template>
<style>
#description {
  height: 100%;
  display: block;
  padding: 1rem;
  margin-bottom: 1rem;
  position: relative;
}
</style>