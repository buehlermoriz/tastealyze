<template>
  <p>{{ keyword }}</p>
  <div id="treemap_detail"></div>
</template>

<script>
import * as d3 from "d3";

export default {
  props: {
    url: {
      type: String,
      required: true,
    },
    keyword: {
      type: String,
      required: false,
    default: null}
  },
  mounted() {
    const self = this;

    const generate = () => {
      // set the dimensions and margins of the graph
      const margin = { top: 10, right: 10, bottom: 10, left: 10 },
        width = 890 - margin.left - margin.right,
        height = 600 - margin.top - margin.bottom;

      // append the svg object to the body of the page
      const svg = d3
        .select("#treemap_detail")
        .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", `translate(${margin.left}, ${margin.top})`);

      // Read data
      d3.json(this.url).then(function (data) {
        // find the data for the keyword
        data = data["children"].find(item => item.name === self.keyword);
        // stratify the data: reformatting for d3.js
        const root = d3.hierarchy(data)
      .sum(d => d.value)
      .sort((a, b) => b.value - a.value);
        // Then d3.treemap computes the position of each element of the hierarchy
        // The coordinates are added to the root object above
        d3.treemap().size([width, height]).padding(4)(root);

        // use this information to add rectangles:
        svg
          .selectAll("rect")
          .data(root.leaves())
          .join("rect")
          .attr("x", function (d) {
            return d.x0;
          })
          .attr("y", function (d) {
            return d.y0;
          })
          .attr("width", function (d) {
            return d.x1 - d.x0;
          })
          .attr("height", function (d) {
            return d.y1 - d.y0;
          })
          .style("fill", "#f87171")
        // and to add the text labels
        svg
          .selectAll("text")
          .data(root.leaves())
          .join("text")
          .attr("x", function (d) {
            return d.x0 + 10;
          }) // +10 to adjust position (more right)
          .attr("y", function (d) {
            return d.y0 + 20;
          }) // +20 to adjust position (lower)
          .text(function (d) {
            return d.data.name;
          })
          .attr("font-size", "13px")
          .attr("fill", "white");
      });
    };
    if (this.keyword){
      generate();
    }
  },
};
</script>
