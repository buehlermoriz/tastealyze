<template>
  <div id="map"></div>
</template>
<script>
import * as d3 from "d3";
import { geoMercator, geoPath } from "d3-geo";
import * as topojson from "topojson-client";

export default {
  mounted() {
    var width = 900;
    var height = 600;

    var projection = d3.geoMercator();

    var svg = d3
      .select("#map")
      .append("svg")
      .attr("width", width)
      .attr("height", height);
    var path = d3.geoPath().projection(projection);
    var g = svg.append("g");
    var url = "https://unpkg.com/world-atlas@2.0.2/countries-110m.json";

    var url = "https://unpkg.com/world-atlas@2.0.2/countries-110m.json";
    fetch(url)
      .then((response) => response.json())
      .then((topology) => {
        g.selectAll("path")
          .data(topojson.feature(topology, topology.objects.countries).features)
          .enter()
          .append("path")
          .attr("d", path);
      })
      .catch((error) => console.log(error));
  },
};
d3.csv("../assets/countries.csv",  (data) => {
  console.log(data);
  // create a map from the data using the country name as the key
  var countryData = d3.map(data, function (d) {
    return d.country;
  });

  g.selectAll("path").style("fill", function (d) {
    var country = d.properties.name;
    var points = +countryData.get(country).points;
    return colorScale(points);
  });
});

</script>

<style>
#map {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
</style>
