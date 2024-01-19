<template>
  <div>
    <svg width="960" height="600">
      <!-- must be in this order for drawing -->
      <g id="links"></g>
      <g id="nodes"></g>
      <text id="tooltip" style="display: none;"></text>
    </svg>
  </div>
</template>

<script>

// import DataService from '../services/DataService.js';
import requesthelp from "../services/request.js";
import * as d3 from 'd3';

export default {
  name: 'HelloWorld',
  setup() {
    // 初始化数据
    var data = new Object();
    var node_data = new Object();
    // const items = ref([]);
    return {data, node_data};
  },
  methods:{
    async render(){ 
      var response = await requesthelp.axiosGet("/data")
      this.data = response
      response = await requesthelp.axiosGet("/nodes")
      this.node_data = response
      this.draw(this.data, this.node_data)
    },
    draw(data, nodes){
      console.log(data, node_data)
      const svg  = d3.select("svg");

      const width  = parseInt(svg.attr("width"));
      const height = parseInt(svg.attr("height"));

      console.log(width, height);

      // have these already created for easier drawing
      const g = {
        links:  svg.select("g#links"),
        nodes: svg.select("g#nodes")
      };

      console.assert(g.links.size()  === 1);
      console.assert(g.nodes.size() === 1);

      const tooltip = d3.select("text#tooltip");
      console.assert(tooltip.size() === 1);

      let bundle = this.generateSegments(nodes, links);

    },
    generateSegments(nodes,links){

    }
  },
  mounted() {
    this.render()
  }
};

</script>