<template>
  <div id="priceandpoints">

    <div class="grid h-screen place-items-center ">
      <div>
          <h1 class="headline-map">Price und Punkte</h1>
          
  
          
          <p id="value-range"></p>
      </div>
      <div class="relative p-4">
        <div class="flex justify-center" id="my_dataviz">
        <!--y axis-->
        <p class="text-2xl transform -rotate-90 absolute left-0 self-center mr-3" >Punkte</p>
        <!--y axis-->
        <p class="text-2xl transform  absolute bottom-0 self-center mr-3">Preis</p>
      </div>
     
        
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
var margin = {top: 10, right: 30, bottom: 30, left: 60},
        width = 800 - margin.left - margin.right,
        height = 800 - margin.top - margin.bottom;
    
    // append the svg object to the body of the page
    var svg = d3.select("#my_dataviz")
      .append("svg")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
      .append("g")
        .attr("transform",
              "translate(" + margin.left + "," + margin.top + ")");
    
    //Read the data from csv in assets folder
    d3.csv("https://raw.githubusercontent.com/buehlermoriz/tastealyze/main/assets/data.csv").then((data1) => {
        console.log(data1);

      // Add X axis with the label "price"
      var x = d3.scaleLinear()
        .domain([0, 500])
        .range([ 0, width ]);

        svg.append("g")
        .attr("transform", "translate(0," + height + ")")
        .call(d3.axisBottom(x));

    
      // Add Y axis
      var y = d3.scaleLinear()
        .domain([75, 105])
        .range([ height, 0]);
      svg.append("g")
        .call(d3.axisLeft(y));
    
      // Add dots
      svg.append('g')
        .selectAll("dot")
        .data(data1)
        .enter()
        .append("circle")
          .attr("cx", function (d) { return x(d.price); } )
          .attr("cy", function (d) { return y(d.points); } )
          .attr("r", 3)
          .style("fill", "#fb6a4a");

    })
    }
}


</script>