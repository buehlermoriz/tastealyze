<template>
  <div class="wordcloud mt-5"></div>
</template>

<script>
import { onMounted, ref } from 'vue';
import * as d3 from 'd3';
import cloud from 'd3-cloud';

export default {
  props: {
    keywords: {
      type: Array,
      required: true
    },
    color: {
      type: String,
      required: true
    },
    cloudnr: {
      type: Number,
      required: true
    },
  },
  setup(props) {
    
    onMounted(() => {
      const wordcloud = document.getElementsByClassName('wordcloud')[props.cloudnr];
      const data = props.keywords;

      const width = 600;
      const height = 600;

      const svg = d3
        .select(wordcloud)
        .append('svg')
        .attr('width', width)
        .attr('height', height)
        .append('g')
        .attr('transform', `translate(${width / 2}, ${height / 2})`);

      const fontSizeScale = d3
        .scaleLinear()
        .domain([0, d3.max(data, d => d[1])])
        .range([10, 80]);

        const colorScale = d3.scaleOrdinal()
  .domain(data.map(d => d[0]))
  .range(data.map(([word, weight]) => {
    if (props.color === 'red') {
      return weight > 0.4 ? '#800000' : weight > 0.2 ? '#B80F0A' : '#555555';
    } else if (props.color === 'green') {
      return weight > 0.4 ? '#0f4336' : weight > 0.2 ? '#556B2F' : '#555555';
    } else {
      // Default color
      return '#555555';
    }
  }));
      

      const layout = cloud()
        .size([width, height])
        .words(data.map(d => ({ text: d[0], size: fontSizeScale(d[1]) })))
        .padding(5)
        .rotate(() => ~~(Math.random() * 2) * 90)
        .font('Impact')
        .fontSize(d => d.size)
        .on('end', draw);

      layout.start();

      function draw(words) {
        svg
          .selectAll('text')
          .data(words)
          .enter()
          .append('text')
          .style('font-size', d => `${d.size}px`)
          .style('fill', (_, i) => colorScale(i))
          .attr('text-anchor', 'middle')
          .attr('transform', d => `translate(${d.x}, ${d.y})rotate(${d.rotate})`)
          .text(d => d.text)
          .on('mouseover', showTooltip)
          .on('mouseout', hideTooltip);
      }

      function showTooltip(event, d) {
        const tooltip = d3
          .select('body')
          .append('div')
          .attr('class', 'tooltip')
          .style('position', 'absolute')
          .style('pointer-events', 'none')
          .style('background-color', 'white')
          .style('border', '1px solid black')
          .style('padding', '5px')
          .style('left', `${event.pageX + 10}px`)
          .style('top', `${event.pageY}px`);

        tooltip.html(d.text + '<br/>' + d[2]);
      }

      function hideTooltip() {
        d3.select('.tooltip').remove();
      }
    });

  }
};
</script>

<style>
.tooltip {
  opacity: 0.9;
}
</style>
