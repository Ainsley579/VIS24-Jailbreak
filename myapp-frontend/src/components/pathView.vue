<template>
  <div>
  </div>
</template>

<script>

// import DataService from '../services/DataService.js';
import requesthelp from "../services/request.js";
export default {
  name: 'HelloWorld',
  setup() {
    // 初始化数据
    var data = new Object();
    // const items = ref([]);
    return {data};
  },
  methods:{
    async fetchData(){ 
      var response = await requesthelp.axiosGet("/data")
      // this.data = response
      console.log(response)
    }
  },
  mounted() {
    this.fetchData()
  }
  
};

</script>