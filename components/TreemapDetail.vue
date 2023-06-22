<template>
  <div class="treemap_detail_wrapper">
    <h2 class="font-semibold uppercase md:text-5xl m-3">{{ keyword }}</h2>
    <p class="m-3" v-if="keyword">Doch welche Begriffe werden mit dem Keyword <span class="font-semibold"> {{ keyword }} </span>  in Weinnamen häufig kombiniert? Hier die Top 10 der kombinierten Keywords. <br> Über den nachfolgenden Button haben Sie die Möglichkeit zurück zur Übersicht zu gelangen. </p>
    <button @click="backToOverview" v-if="keyword" type="button" class="text-white bg-gradient-to-br from-pink-500 to-orange-400 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-pink-200 dark:focus:ring-pink-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mx-3 mb-2">zur Übersicht</button>
    <div id="treemap_detail"></div>
  <p id="tooltipDetail">{{ tooltip }}</p>

  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  data() {
    return {
      tooltips: [], // Store tooltip data
      tooltip: "", // Store tooltip
    };
  },
  props: {
    url: {
      type: String,
      required: true,
    },
    keyword: {
      type: String,
      required: false,
      default: null,
    },
  },
  methods: {
    backToOverview() {
      this.$emit("treemap_select", null);
    },
  },
  mounted() {
    const self = this;

    const generate = () => {
      //remove general Treemap
      const treemap = d3.select("#treemap");
      const tooltipTreemap = d3.select("#tooltipTreemap");

      if (!treemap.select("svg").empty()) {
        treemap.select("svg").remove();
        tooltipTreemap.style("display", "none");
      }

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
        data = data["children"].find((item) => item.name === self.keyword);
        // stratify the data: reformatting for d3.js
        const root = d3
          .hierarchy(data)
          .sum((d) => d.value)
          .sort((a, b) => b.value - a.value);

        // Then d3.treemap computes the position of each element of the hierarchy
        // The coordinates are added to the root object above
        d3.treemap().size([width, height]).padding(4)(root);
        let tooltipMap = new Map(data.children.map((d) => [d.name, d.tooltip]));
        self.tooltips = root.leaves().map((d) => d.data.tooltip);

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
        .on("mouseover", function (event, d) {
            //display tooltip
            const tooltip = d3.select("#tooltipDetail");
            tooltip.style("display", "block");
            // Show tooltip on mouseover
            self.tooltip = tooltipMap.get(d.data.name);
            //coordinates
            tooltip
              .style("left", event.pageX + 10 + "px")
              .style("top", event.pageY + 10 + "px");
          })
          .on("mousemove", function (event) {
            //coordinates
            const tooltip = d3.select("#tooltipDetail");
            tooltip
              .style("left", event.pageX + 10 + "px")
              .style("top", event.pageY + 10 + "px");
          })
          .on("mouseout", function () {
            // Hide tooltip on mouseout
            const tooltip = d3.select("#tooltipDetail");
            tooltip.style("display", "none");
          });
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
    if (this.keyword) {
      generate();
    }
  },
};
</script>
<style>
#tooltipDetail {
  display: none;
  /* card style */
  position: absolute;
  background-color: #282828;
  color: white;
  padding: 0.5rem;
  border-radius: 0.5rem;
  max-width: 20%;
}</style>