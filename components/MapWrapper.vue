<template>
    <div id="worldmap" class="map_wrapper">
        <h1 class="headline-map">Globale Unterschiede <br> in der Weinproduktion</h1>
        <p class="text-center" id="description">Diese Grafik zeigt globale Unterschiede in der Weinproduktion. Dabei können Sie aus drei Bereichen auswählen. Mit einer Wahl der durchscnittlichen Punkte erhalten Sie eine Visualisierung wie viele Punkte die Tester den Weinen eines Landes auf einer Skala von 0 bis 1 durchschnittlich gegeben haben. Bei der Auswahl des Preises erhalten sie die durchscnittlichen Preise. Zuletzt lassen sich die Ergebnisse einer Sentimentanalyse darstellen. Hierbei wurden die Texte der Produktbewertungen ausgewertet. Je nach dem wie positiv (oder Negativ) eine Produktbeschriebung ist wurde eine Wert zwischen 0 und 1 ermittelt, welcher auf der Karte dargestellt wird.</p>
        <p> Sie interessieren sich für ein einzelnes Land? Hovern sie einfach mit der Maus über das entpsprechende Land</p>
        <Map />
    </div>
</template>
<style>
/* Background Color*/
.map_wrapper {
    margin-top: 100px;
    background-color: #fbfbfbfb;
    padding-left: 20%;
    padding-right: 2%;
}
#description {
  height: 100%;
  display: block;
  padding: 1rem;
  margin-bottom: 1rem;
  position: relative;
}
.headline-map {
    text-align: center;
    padding-top: 20px;
    padding-bottom: 20px;
    line-height: 1;
    font-size: 4rem;
    font-weight: bold;
}
</style>