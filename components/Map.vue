<template>
  <div class="grid grid-cols-5 gap-y-1"> 
  <div class="col-span-4 flex items-center">
    <div id="map"></div>
    </div>
  <div class="col-span-1 flex flex-col justify-center">
  <div>
    <div class="radio-group">
      <input type="radio" id="control_01" name="select" value="points" v-model="selectedValue" checked>
  <label for="control_01">
    <h2>Punkte</h2>
    <p>Diese Darstellung zeigt Ihnen die durchschschnittlichen Punkte, welche Weine aus einem Land erhalten.</p>
  </label>
</div>
<div>
  <input type="radio" id="control_02" name="select" value="price" v-model="selectedValue">
  <label for="control_02">
    <h2>Preis</h2>
    <p>Diese Darstellung zeigt Ihnen den durchschschnittlichen Preis, welcher für Weine aus den Ländern bezahlt wird.</p>
  </label>
</div>
<div>
  <input type="radio" id="control_03" name="select" value="sentiment" v-model="selectedValue">
  <label for="control_03">
    <h2>Sprache</h2>
    <p>Diese Darstellung zeigt Ihnen wie positiv oder negativ die Sprache der Reviews zu Weinen aus den Ländern ausfällt.</p>
  </label>
    </div>
  </div>  
  </div>
  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  data() {
    return {
      selectedValue: "points",
    };
  },
  mounted() {
    var width = 1100;
    var height = 800;

    // The svg
    var svg = d3
      .select("#map")
      .append("svg")
      .attr("width", width)
      .attr("height", height);

    // Map and projection
    const path = d3.geoPath();
    const projection = d3
      .geoMercator()
      .scale(160)
      .center([0, 60]);

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
        // Create a map from country code to selected data value
        let dataByCountry = new Map(
          data.map((d) => [d.country, +d[this.selectedValue]])
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
          .attr("stroke-width", 0.5);
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

</style>
