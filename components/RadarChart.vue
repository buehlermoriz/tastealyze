<template>
  <div class="flex justify-center">
    <div class="max-w-2xl">
      <div id="loading" class="min-h-[300px] flex items-center justify-center">
        <img src="../assets/37267-swirling-wine.gif" autoplay loop class="mx-auto my-auto" />
      </div>
      <canvas id="radar-chart" class="hidden"></canvas>
    </div>
  </div>
</template>


<script>
import { Chart, registerables } from "chart.js";
import { RadarController, CategoryScale } from "chart.js";
import * as d3 from "d3";

Chart.register(...registerables);
Chart.register(RadarController, CategoryScale);

export default {
    props: {
    wineType: {
      type: String,
      required: true,
      validator: (value) => ["White", "Red", "Rose"].includes(value),
    },},
  data() {
    return {
      data: {
        labels: [],
        datasets: [],
    },
    wineColor: "",
    wineBorderColor: "",
    };
  },
  async mounted() {
    const radarCanvas = document.getElementById("radar-chart");
    //change the color of the chart according to the wine type
    switch (this.wineType) {
      case "White":
        this.wineColor = "rgba(238, 237, 196, 0.01)";
        this.wineBorderColor = "rgba(238, 237, 196, 0.02)";
        break;
      case "Red":
        this.wineColor = "rgba(248, 113, 113, 0.01)";
        this.wineBorderColor = "rgba(248, 113, 113, 0.02)";
        break;
      case "Rose":
        this.wineColor = "rgba(255, 192, 203, 0.01)";
        this.wineBorderColor = "rgba(255, 192, 203, 0.02)";
        break;
    }
    Promise.all([
      d3.csv(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/radarchart/assets/radar_chart.csv"
      ),
    ]).then((loadData) => {
      let data = loadData[0];
      const results = data
        .filter((entry) => entry.type === this.wineType)
        .map((entry) => ({
          backgroundColor: this.wineColor,
          borderColor: this.wineBorderColor,
          data: [
            parseFloat(entry.abv),
            parseFloat(entry.degree),
            parseFloat(entry.sweet),
            parseFloat(entry.acidity),
            parseFloat(entry.body),
            parseFloat(entry.tannin),
          ],
          pointRadius: 0,
        }));

      this.data.labels = [
        "abv",
        "degree",
        "sweet",
        "acidity",
        "body",
        "tannin",
      ];
      this.data.datasets = results;
      //generate Chart
      const radarChart = new Chart(radarCanvas, {
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
    //hode loading gif
      document.getElementById("loading").style.display = "none";
    });
  },
};
</script>
