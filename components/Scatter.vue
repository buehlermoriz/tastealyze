<template>
  <div class="scatter_wrapper pb-28 pt-28 mx-[5%] md:ml-[20%]">
    <div class="md:grid md:grid-cols-6 md:gap-y-1">
      <div class="md:col-span-2">
        <h1 class="text-2xl md:text-5xl text-bold">Preis und Punkte</h1>
        <p>
          "Lisa" ist im Supermarkt und sieht viele Weine, recht daneben sieht
          sie diese Grafik. Verschiedene Weintester haben Punkte an Weine
          vergeben, dazu gibt der Markt die Informationen der Preise zusätzlich
          an, um eine Relation erkennbar zu machen. Diese Grafik zeigt das
          Billige Weine eine Große diskrepant in der Qualität aufweisen, diese
          können von gut bis ungenießbar reichen, wobei teurere Weine oft besser
          bewertet werden.
        </p>
      </div>
      <div class="p-4 md:col-span-4 justify-center">
        <div id="my_dataviz"></div>
      </div>
    </div>
  </div>
</template>

<script>
import * as d3 from "d3";
// get the csv file from assets folder

export default {
  name: "Scatter",
  mounted() {
    // set the dimensions and margins of the graph
    var margin = { top: 10, right: 30, bottom: 30, left: 60 };
    

    const screenWidth = window.innerWidth;
      const isMobile = screenWidth < 768;
      let width = 500;
      let height = 500;
      if (isMobile) {
        width = screenWidth * 0.9 - margin.left - margin.right;
        height = width - margin.left - margin.right;
      } else {
        width = screenWidth * 0.4 - margin.left - margin.right;
        height = width - margin.left - margin.right;
      }

    // append the svg object to the body of the page
    var svg = d3
      .select("#my_dataviz")
      .append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

    //Read the data from csv in assets folder
    d3.csv(
      "https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/data.csv"
    ).then((data1) => {
      // Add X axis
      var x = d3.scaleLinear().domain([0, 500]).range([0, width]);

      svg
        .append("g")
        .attr("transform", "translate(0," + height + ")")
        .call(d3.axisBottom(x));

      // Add Y axis
      var y = d3.scaleLinear().domain([75, 105]).range([height, 0]);
      svg.append("g").call(d3.axisLeft(y));

      //add label
      svg.append("text")
  .attr("class", "x-axis-label")
  .attr("x", width / 2)
  .attr("y", height + margin.bottom)
  .style("text-anchor", "middle")
  .text("Preis in €");

  svg.append("text")
  .attr("class", "y-axis-label")
  .attr("transform", "rotate(-90)")
  .attr("x", -height / 2)
  .attr("y", -25)
  .style("text-anchor", "middle")
  .text("Punkte");

      // Add dots
      svg
        .append("g")
        .selectAll("dot")
        .data(data1)
        .enter()
        .append("rect")
        .attr("width", 25.5)
        .attr("height", 25.5)
        .attr("x", function (d) {
          return x(d.price);
        })
        .attr("y", function (d) {
          return y(d.points);
        })
        .style("opacity", 0.05)
        .style("fill", "#fb6a4a");
    });
  },
};
</script>
