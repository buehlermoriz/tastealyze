<template>
  <div class="flex justify-center">
    <div class="max-w-2xl">
      <div id="loading" class="min-h-[300px] flex items-center justify-center">
        <img :src="loaderPath" autoplay loop class="mx-auto my-auto" />
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
      validator: (value) => ["Weißwein", "Rotwein", "Roséwein"].includes(value),
    },
    grapeType: {
      type: String,
      required: false,
      default: "",
    },
    lastData: {
      type: Array,
      required: false,
      default: null,
    },
  },
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
  computed: {
    loaderPath() {
        return "/img/loader/" + this.wineType + ".gif";
    },
  },
  async mounted() {
    const radarCanvas = document.getElementById("radar-chart");
    //change the color of the chart according to the wine type
    switch (this.wineType) {
      case "Weißwein":
        this.wineColor = "rgba(242, 228, 183, 0.01)";
        this.wineBorderColor = "rgba(242, 228, 183, 0.02)";
        break;
      case "Rotwein":
        this.wineColor = "rgba(248, 113, 113, 0.01)";
        this.wineBorderColor = "rgba(248, 113, 113, 0.02)";
        break;
      case "Roséwein":
        this.wineColor = "rgba(244, 165, 158, 0.01)";
        this.wineBorderColor = "rgba(244, 165, 158, 0.02)";
        break;
    }
    Promise.all([
      d3.csv(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/radar_chart.csv"
      ),
    ]).then((loadData) => {
      let data = loadData[0];
      const results = data
        //filter for red, white rosewine
        //filter optionally for grape type
        .filter((entry) => entry.type === this.wineType&& (this.grapeType === "" || entry.varieties === this.grapeType))
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
      //set data to variable
      if (this.lastData !== null) {
        this.data.datasets = results.concat(this.lastData);
      }
      else{
        this.data.datasets = results;
      }
      //emit data to parent component for further use

// Calculate the mean for each position in the data arrays
const dataAverages = results[0].data.map((_, index) => {
  const sum = results.reduce((total, element) => total + element.data[index], 0);
  return sum / results.length;
});

      // Generate a new array with the resulting averages
      const returnArray = [
        {
          backgroundColor: "rgba(50, 50, 50, 0.7)",
          borderColor: "rgba(50, 50, 50, 0.8)",
          data: dataAverages,
          pointRadius: 0,
        },
      ];

      this.$emit("updateData", returnArray);
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
