<template>
  <div id="map"></div>
</template>

<script>
import * as d3 from "d3";

export default {
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
      .center([0, 60])

  

    // Load external data and boot
    Promise.all([
      d3.json(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/wold_map.geojson"
      ),
      d3.csv(
        "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/countries.csv"
      ),
    ]).then(function (loadData) {
      let topo = loadData[0];
      let data = loadData[1];

      // Create a map from country code to points
      let pointsByCountry = new Map(data.map((d) => [d.country, +d.points]));

      const colorScale = d3
        .scaleThreshold()
        .domain([0.2, 0.4, 0.6, 0.8, 1])
        .range(d3.schemeReds[6]);

      // Draw the map
      svg
        .append("g")
        .selectAll("path")
        .data(topo.features)
        .join("path")
        // draw each country
        .attr("d", d3.geoPath().projection(projection))
        // set the color of each country based on points
        .attr("fill", function (d) {
          let points = pointsByCountry.get(d.properties.name) || 0;
          return colorScale(points);
        })
        .attr("stroke", "white")
        .attr("stroke-width", 0.5);
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
</style>