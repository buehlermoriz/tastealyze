<template>
  <div class="flex justify-center">
    <div class="max-w-2xl">
      <canvas id="marksChart"></canvas>
    </div>
  </div>
</template>
<script>
import { Chart, registerables } from "chart.js";
import { RadarController, CategoryScale } from "chart.js";
Chart.register(...registerables);
Chart.register(RadarController, CategoryScale);

export default {
  data() {
    return {
      data: {
        labels: ["abv", "degree", "sweet", "acidity", "body", "tannin"],
        datasets: [
          {
            backgroundColor: "rgba(200,0,0,0.1)",
            data: [14.5, 18.0, 1, 4, 5, 4],
            pointRadius: 0,
          },
          {
            backgroundColor: "rgba(200,0,0,0.1)",
            data: [11.5, 10.0, 1, 3, 2, 1],
            pointRadius: 0,
          },
          {
            backgroundColor: "rgba(200,0,0,0.1)",
            data: [11, 11.0, 3, 2, 3, 1],
            pointRadius: 0,
          },
        ],
      },
    };
  },
  mounted() {
    var marksCanvas = document.getElementById("marksChart");
    var radarChart = new Chart(marksCanvas, {
      type: "radar",
      data: this.data,
      options: {
        plugins: {
          legend: {
            display: false,
          },
        },
      },
    });
  },
};
</script>
