<template>
<div>
  <el-row >
  <el-col :span="24"  > 
    <TimeLine :xAxisData="xAxisData"  v-on:listenChildDataZoom="changDataZoom" > 
    </TimeLine></el-col>
</el-row>
<el-row v-for=" (item , index) in viewData" :key="index"  >
  <el-col :span="24"  :key="index"> 
    <h1>asda</h1>    
    <VmChartBarLine :title="item.title" :xAxisData="item.xAxisData" :series="item.series" :dataZoomSys="dataZoomSys">
    </VmChartBarLine></el-col>
</el-row>

</div>
</template>



<script>

  import VmChartBarLine from '../components/echarts.vue'
   import TimeLine from '../components/TimeLine.vue'
  import data1 from '../assets/data.json'


  export default {

    name: 'Home',

    components: {
      VmChartBarLine,data1,TimeLine
    },

    data: function () {
      return {
            dataZoomSys:{},
            xAxisData:{},
            viewData:[]
      }

    },
    methods:{
      changDataZoom:function(dataZoomSys){
          this.dataZoomSys = dataZoomSys
      }
    }
    ,mounted(){
          this.xAxisData = {min:1540043434000,max:1540044534000}
          this.viewData = data1
    }

  }

</script>