<template>
    <div class="flex justify-center">
        <canvas id="marksChart" width="200" height="200"></canvas>
    </div>
    </template>
<script>
import { Chart, registerables } from 'chart.js';
import { RadarController, CategoryScale } from 'chart.js';
Chart.register(...registerables);
Chart.register(RadarController, CategoryScale);

export default {
  data(){
    return{
        data: { 
  labels: ["abv","degree","sweet","acidity","body","tannin"],
  datasets: [{
    label: "Red",
    backgroundColor: "rgba(200,0,0,0.2)",
    data: [14.5,18.0,1,4,5,4]
  },
  {
    label: "White",
    backgroundColor: "rgba(0,0,200,0.2)",
    data: [11.5,10.0,1,3,2,1]
    },
    {
    label: "Rose",
    backgroundColor: "rgba(0,200,0,0.2)",
    data: [11,11.0,3,2,3,1]
    },
    ]}
  }},
  mounted(){
    var marksCanvas = document.getElementById("marksChart");
    var radarChart = new Chart(marksCanvas, {
  type: 'radar',
  data: this.data
});
  }
}


</script>