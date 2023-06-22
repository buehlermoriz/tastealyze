<template>
  <div class="general_treemap_wrapper"></div>
  <div v-if="keyword===null" class="flex m-3 items-center">
    <img src="../assets/click.gif" />
    <p class="text-gray-400 italic">Info: Du willst wissen, welche Keywords sich mit den Begriffen gut kombinieren lassen? Klicke doch einfach auf das entsprechende Feld. </p>
  </div>

  <div id="treemap"></div>
  <p id="tooltipTreemap">{{ tooltip }}</p>
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
    emitValue(value) {
      this.$emit("treemap_select", value);
    },
  },
  mounted() {
    const self = this;

    const generate = () => {
      // set the dimensions and margins of the graph
      const margin = { top: 10, right: 10, bottom: 10, left: 10 };
      const screenWidth = window.innerWidth;
      const isMobile = screenWidth < 768;
      let width = 500;
      let height = 500;
      if (isMobile) {
        width = screenWidth * 0.9 - margin.left - margin.right;
        height = width*2 - margin.left - margin.right;
      } else {
        width = screenWidth * 0.4 - margin.left - margin.right;
        height = width*2 - margin.left - margin.right;
      }

      // append the svg object to the body of the page
      const svg = d3
        .select("#treemap")
        .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr("transform", `translate(${margin.left}, ${margin.top})`);

      // Read data
      d3.csv(this.url).then(function (data) {
        // stratify the data: reformatting for d3.js
        const root = d3
          .stratify()
          .id(function (d) {
            return d.keyword;
          }) // Name of the entity (column name is name in csv)
          .parentId(function (d) {
            return d.parent;
          })(
          // Name of the parent (column name is parent in csv)
          data
        );
        root.sum(function (d) {
          return +d.normalized_col;
        }); // Compute the numeric value for each entity
        let tooltipMap = new Map(data.map((d) => [d.keyword, d.tooltip]));

        // Assign tooltip values to tooltips variable
        self.tooltips = root.leaves().map((d) => d.data.tooltip);
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
          .on("mouseover", function (event, d) {
            //display tooltip
            const tooltip = d3.select("#tooltipTreemap");
            tooltip.style("display", "block");
            // Show tooltip on mouseover
            self.tooltip = tooltipMap.get(d.data.keyword).replace("&#44;", ",");
            //coordinates
            tooltip
              .style("left", event.pageX + 10 + "px")
              .style("top", event.pageY + 10 + "px");
          })
          .on("mousemove", function (event) {
            //coordinates
            const tooltip = d3.select("#tooltipTreemap");
            tooltip
              .style("left", event.pageX + 10 + "px")
              .style("top", event.pageY + 10 + "px");
          })
          .on("mouseout", function () {
            // Hide tooltip on mouseout
            const tooltip = d3.select("#tooltipTreemap");
            tooltip.style("display", "none");
          })
          .on("click", function (event, d) {
            // Emit value to parent component
            self.emitValue(d.data.keyword);
          })

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
            return d.data.keyword;
          })
          .attr("font-size", "13px")
          .attr("fill", "white");
      });
    };
    if (this.keyword== null) {
      generate();
    }  },
};
</script>

<style>
/* center treemap */
#treemap {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}
#tooltipTreemap {
  display: none;
  /* card style */
  position: absolute;
  background-color: #282828;
  color: white;
  padding: 0.5rem;
  border-radius: 0.5rem;
  max-width: 20%;
}
</style>
