<template>
  <!-- Tooltip -->
  <div class="grid grid-cols-5 gap-y-1">
    <div class="col-span-4 flex items-center">
      <div class="tooltip">
        <h2 class="headline">{{ tooltipCountry }}</h2>
        <div class="tooltip-box">
          durchschnittliche Bewertung
          <p class="tooltip-nr">{{ tooltipPoints }}</p>
        </div>
        <!-- <div class="tooltip-box">
          {{ tooltipCountry }}
          <img class="block h-14 w-auto" :src="'../assets/Flags/'"+tooltipCountry + "'.gif'" alt="tastealyze" />
        </div> -->
        <div class="tooltip-box">
          durchschnittlicher Preis
          <p class="tooltip-nr">{{ tooltipPrice }}</p>
        </div>
        <div class="tooltip-box">
          Tonalität
          <p class="tooltip-nr">{{ tooltipLanguage }}</p>
        </div>
      </div>
    </div>
  </div>
  <div class="grid grid-cols-5 gap-y-1">
    <div class="col-span-4 flex items-center">
      <div id="map"></div>
    </div>
    <div class="col-span-1 flex flex-col justify-center">
      <div>
        <div class="radio-group">
          <input
            type="radio"
            id="control_01"
            name="select"
            value="points"
            v-model="selectedValue"
            checked
          />
          <label for="control_01">
            <h2 class="font-bold uppercase">Punkte</h2>
            <p>
              Diese Darstellung zeigt Ihnen die durchschschnittlichen Punkte,
              welche Weine aus einem Land erhalten.
            </p>
          </label>
        </div>
        <div>
          <input
            type="radio"
            id="control_02"
            name="select"
            value="price"
            v-model="selectedValue"
          />
          <label for="control_02">
            <h2 class="font-bold uppercase">Preis</h2>
            <p>
              Diese Darstellung zeigt Ihnen den durchschschnittlichen Preis,
              welcher für Weine aus den Ländern bezahlt wird.
            </p>
          </label>
        </div>
        <div>
          <input
            type="radio"
            id="control_03"
            name="select"
            value="sentiment"
            v-model="selectedValue"
          />
          <label for="control_03">
            <h2 class="font-bold uppercase">Sprache</h2>
            <p>
              Diese Darstellung zeigt Ihnen wie positiv oder negativ die Sprache
              der Reviews zu Weinen aus den Ländern ausfällt.
            </p>
          </label>
        </div>
      </div>
    </div>
  </div>
  <div class="legend-container"></div>
</template>

<script>
import * as d3 from "d3";

export default {
  data() {
    return {
      selectedValue: "points",
      tooltipPosition: {
        x: 0,
        y: 0,
      },
      tooltipCountry: "zum auswählen hovern",
      tooltipPoints: "0",
      tooltipPrice: "0",
      tooltipLanguage: "0",
      tooltipValue: "0",
    };
  },
  mounted() {
    var width = 1100;
    var height = 650;

    var legendWidth = 1000;
    var legendHeight = 60;

    var legend = d3
      .select(".legend-container")
      .append("svg")
      .attr("width", legendWidth)
      .attr("height", legendHeight);

    // The svg
    var svg = d3
      .select("#map")
      .append("svg")
      .attr("width", width)
      .attr("height", height);

    // Map and projection
    const path = d3.geoPath();
    const projection = d3.geoMercator().scale(160).center([0, 60]);

    // Load external data and boot
    Promise.all([
      d3.json(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/wold_map.geojson"
      ),
      d3.csv(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/countries.csv"
      ),
    ]).then((loadData) => {
      let topo = loadData[0];
      let data = loadData[1];

      const updateMap = () => {
        //rm old legend
        legend.selectAll("*").remove();

        // Create a map from country code to selected data value
        let dataByCountry = new Map(
          data.map((d) => [d.country, +d[this.selectedValue]])
        );
        let dataBypoints = new Map(data.map((d) => [d.country, +d.points]));
        let dataByprice = new Map(data.map((d) => [d.country, +d.price]));
        let dataBysentiment = new Map(
          data.map((d) => [d.country, +d.sentiment])
        );
        // set different Color colors depending on user selection
        let colorScaleDomain;
        if (this.selectedValue === "points") {
          colorScaleDomain = [0.2, 0.3, 0.4, 0.5, 0.6];
        } else if (this.selectedValue === "price") {
          colorScaleDomain = [10, 30, 50, 70, 90];
        } else if (this.selectedValue === "sentiment") {
          colorScaleDomain = [0.2, 0.4, 0.6, 0.8, 1];
        }

        const colorScale = d3
          .scaleThreshold()
          .domain(colorScaleDomain)
          .range(d3.schemeReds[6]);

        // Draw the map
        svg
          .append("g")
          .selectAll("path")
          .data(topo.features)
          .join("path")
          .attr("d", d3.geoPath().projection(projection))
          .attr("fill", function (d) {
            let value = dataByCountry.get(d.properties.name) || 0;

            return colorScale(value);
          })
          .attr("stroke", "white")
          .attr("stroke-width", 0.5)
          .on("mouseover", (event, d) => {
            const [x, y] = d3.pointer(event);
            const country = d.properties.name;
            const value = (dataByCountry.get(country) || 0).toFixed(2);
            const points = (dataBypoints.get(country) || 0).toFixed(2);
            const price = (dataByprice.get(country) || 0).toFixed(2);
            const sentiment = (dataBysentiment.get(country) || 0).toFixed(2);

            this.tooltipCountry = country;
            this.tooltipValue = value;
            this.tooltipPoints = points;
            this.tooltipLanguage = sentiment;
            this.tooltipPrice = price;
            this.tooltipPosition = {
              x,
              y,
            };
          })
          .on("mouseout", () => {
            (this.tooltipCountry = "zum auswählen hovern"),
              (this.tooltipPoints = "0"),
              (this.tooltipPrice = "0"),
              (this.tooltipLanguage = "0"),
              (this.tooltipValue = "0");
          });

        //draw legend
        const legendRectSize = legendWidth / colorScaleDomain.length;

        var legendGroup = legend
          .selectAll("g")
          .data(colorScaleDomain)
          .enter()
          .append("g")
          .attr("transform", function (d, i) {
            return "translate(" + i * legendRectSize + ", 0)";
          });
        legendGroup
          .append("rect")
          .attr("x", 0)
          .attr("y", 10)
          .attr("width", legendRectSize)
          .attr("height", 20)
          .style("fill", function (d) {
            return colorScale(d);
          });
        legendGroup
          .append("text")
          .attr("x", legendRectSize / 2)
          .attr("y", 40)
          .attr("text-anchor", "middle")
          .attr("dy", "0.5em") // Adjust the value to add margin between legend and text
          .text(function (d) {
            return d;
          });
      };

      updateMap();

      this.$watch("selectedValue", () => {
        svg.selectAll("path").remove();
        updateMap();
      });
    });
  },
};
</script>

<style>
#map {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding-top: 10%;
  padding-bottom: 10%;
}

input[type="radio"] {
  display: none;
}

input[type="radio"]:not(:disabled) ~ label {
  cursor: pointer;
}

label {
  height: 100%;
  display: block;
  background: white;
  border: 2px solid hsla(0, 54%, 18%, 1);
  border-radius: 20px;
  padding: 1rem;
  margin-bottom: 1rem;
  text-align: center;
  position: relative;
}

input[type="radio"]:checked + label {
  background: hsla(0, 54%, 18%, 1);
  color: hsla(215, 0%, 100%, 1);
  box-shadow: 0px 0px 20px hsla(0, 54%, 18%, 0.75);
}

.flex {
  display: flex;
}

.items-center {
  align-items: center;
}

.flex-col {
  flex-direction: column;
}

.justify-center {
  justify-content: center;
}
.tooltip-box {
  display: inline-block;
  padding: 10px;
  border-radius: 10px;
  background-color: #dfdfdf;
  margin-right: 10px;
}
.tooltip-nr {
  text-align: center;
  padding-top: 20px;
  padding-bottom: 20px;
  line-height: 1;
  font-size: 4rem;
  font-weight: bold;
  color: white;
}
.headline {
  padding-top: 20px;
  padding-bottom: 20px;
  line-height: 1;
  font-size: 4rem;
  font-weight: bold;
}
</style>
