<template>

  <div class="vm-chart-bar vm-panel">

    <div class="panel-body" :id="this.id" :style="{ height: height + 'px'}">

    </div>

  </div>

</template>

<script>

  // 引入 ECharts 主模块

  var echarts = require('echarts/lib/echarts')

  // 引入柱状图

  require('echarts/lib/chart/bar')

  // 引入提示框和标题组件

    require('echarts/lib/component/dataZoom')

  export default {

    name: 'TimeLine',

    props: {

      height: {

        type: Number,

        default: 100

      },

      // 横坐标数据

      xAxisData: {

        type: Object,

        required: true,

        default: function () {
          return {
            min:0,
            max:1
          }
        }

      },

    },

    data: function () {

      return {
        // 刻度颜色
        chart: null,
       

      }

    },

    computed: {

      // 生成一个随机id, 实现图表组件的复用

      id: function () {

        return parseInt(Math.random() * 1000000)

      },

    },

    methods: {
      changeDataZoom:function(){

      },

      renderChart: function () {
        var _self = this
        if (this.chart) {

          this.chart.dispose()

        }

        // 初始化echart

        this.chart = echarts.init(document.getElementById(this.id))
        debugger
        this.chart.setOption({
           dataZoom:[{
                type: 'inside'
            }, {
                type: 'slider'
            }],

          grid: {
            left: 30,
            right: 15,
          },

          xAxis: {
            min:this.xAxisData.min,//1540043434000,
            max:this.xAxisData.max,//1540044534000,
            type:"time",
            axisTick:{show:false},
            axisLine: {show: false},
            splitLine:{show:false}
          },
          yAxis: {
            show:false,
          },

        })
        this.chart.on('dataZoom', function(param) {
              _self.$emit("listenChildDataZoom",param)
        })

      }

    },

    watch: {
      xAxisData: function () {
        debugger
        console.log(this.xAxisData)
        this.renderChart()
      },
      

    },

    mounted: function () {
      this.renderChart()
    }

  }

</script>