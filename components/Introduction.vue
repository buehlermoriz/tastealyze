<template> 

    <div id="introduction"  class="w-full bg-cover background" :style="`background-image: url(${backgroundImage})`">
    <div class="columns-1 " style=" margin-left:350px; margin-right: 700px; padding-top: 100px;">
        <h2 class=" font-semibold uppercase md:text-5xl"  >Gibt es Qualitäts- und Eigenschaftsunterschiede in der <span class="text-red-700">globalen Weinproduktion?</span></h2>
        <p class="font-regular text-l font-['Roboto']" style="padding-top: 30px;" >Verschiedene Faktoren beeinflussen die Qualität und die charakteristischen Eigenschaften von Wein. Seit Jahrtausenden ist Wein ein wichtiger Bestandteil der menschlichen Kultur und wird weltweit produziert. Es gibt unzählige Sorten und Geschmacksrichtungen, die von Region zu Region variieren. Während einige Weine in bestimmten Gebieten besonders bekannt und beliebt sind, werden wiederum andere Sorten auf der ganzen Welt angebaut und genossen. Winetasting, auch als Weinverkostung bezeichnet, ist eine Möglichkeit, um die Qualität zumeist mehrerer Weine zu beurteilen. Dabei werden Farbe und Klarheit, Aroma, Geschmack, Körper und Struktur sowie der Abgang, also der Nachgeschmack nach dem Herunterschlucken, analysiert. Die Temperatur des Weins sowie ein geeignetes Glas spielen dabei ebenfalls eine wichtige Rolle. </p>
    
      

    </div>
    
    </div>
                 
    
    </template>
    <style>
.background{
    height:43rem;
}
</style>
<script>
import backgroundImage from '~/assets/weinauftuch.jpg';

export default {
    name: 'Introduction',
    components: {
    },
    data() {
        return {
            backgroundImage: backgroundImage,
        }
    },
    mounted() {
    },
}
</script>