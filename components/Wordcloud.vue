<template>
  <div class="wordcloud mt-5"></div>
</template>

<script>
import { onMounted, ref } from "vue";
import * as d3 from "d3";
import cloud from "d3-cloud";

export default {
  data() {
    return {
      width: "",
      height: "",
    };
  },
  props: {
    keywords: {
      type: Array,
      required: true,
    },
    color: {
      type: String,
      required: true,
    },
    cloudnr: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    onMounted(() => {
      const wordcloud =
        document.getElementsByClassName("wordcloud")[props.cloudnr];
      const wordcloudTooltip = document.getElementById("tooltipWordcloud");
      const data = props.keywords;

      const screenWidth = window.innerWidth;
      const isMobile = screenWidth < 768;
      let width = 500;
      let height = 500;
      if (isMobile) {
        width = screenWidth * 0.9;
        height = width;
      } else {
        width = screenWidth * 0.4;
        height = width;
      }

      const tooltip = d3
        .select("wordcloudTooltip")
        .append("div")
        .attr("class", "tooltip")
        .style("position", "absolute")
        .style("opacity", 0); // Set initial opacity to 0

      const svg = d3
        .select(wordcloud)
        .append("svg")
        .attr("width", width)
        .attr("height", height)
        .append("g")
        .attr("transform", `translate(${width / 2}, ${height / 2})`);

      const fontSizeScale = d3
        .scaleLinear()
        .domain([0, d3.max(data, (d) => d[1])])
        .range([10, 80]);

      const colorScale = d3
        .scaleOrdinal()
        .domain(data.map((d) => d[0]))
        .range(
          data.map(([word, weight]) => {
            if (props.color === "red") {
              return weight > 0.4
                ? "#800000"
                : weight > 0.2
                ? "#B80F0A"
                : "#555555";
            } else if (props.color === "green") {
              return weight > 0.4
                ? "#0f4336"
                : weight > 0.2
                ? "#556B2F"
                : "#555555";
            } else {
              // Default color
              return "#555555";
            }
          })
        );

      const layout = cloud()
        .size([width, height])
        .words(
          data.map((d) => ({
            text: d[0],
            size: fontSizeScale(d[1]),
            tooltip: d[2],
          }))
        )
        .padding(5)
        .rotate(() => ~~(Math.random() * 2) * 90)
        .font("Impact")
        .fontSize((d) => d.size)
        .on("end", draw);

      layout.start();

      function draw(words) {
        svg
          .selectAll("text")
          .data(words)
          .enter()
          .append("text")
          .style("font-size", (d) => `${d.size}px`)
          .style("fill", (_, i) => colorScale(i))
          .attr("text-anchor", "middle")
          .attr(
            "transform",
            (d) => `translate(${d.x}, ${d.y})rotate(${d.rotate})`
          )
          .text((d) => d.text)
          .on("mouseover", showTooltip)
          .on("mousemove", moveTooltip)
          .on("mouseout", hideTooltip);
      }

      function showTooltip(event, d) {
        const tooltip = d3
          .select("body")
          .append("div")
          .attr("class", "tooltipWordcloud")
          .style("position", "absolute")
          .style("left", `${event.pageX + 10}px`)
          .style("top", `${event.pageY}px`);

        tooltip.html(
          '<span class="text-xl font-bold">' +
            d.text +
            "</span><br/>" +
            d.tooltip
        );
      }

      function hideTooltip() {
        d3.select(".tooltipWordcloud").remove();
      }
      function moveTooltip(event) {
        d3.select(".tooltipWordcloud")
          .style("left", event.pageX + 10 + "px")
          .style("top", event.pageY + 10 + "px");
      }
    });
  },
};
</script>

<style>
.tooltipWordcloud {
  /* card style */
  position: absolute;
  background-color: #282828;
  color: white;
  padding: 0.5rem;
  border-radius: 0.5rem;
  max-width: 20%;
}
</style>
