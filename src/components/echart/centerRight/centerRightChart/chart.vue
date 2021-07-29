<template>
  <div>
    <Echart
      :options="options"
      id="centreRight2Chart4"
      height="4.20rem"
      width="100%"
    ></Echart>
  </div>
</template>

<script>
import Echart from '@/common/echart'
import echarts from 'echarts'
export default {
  data () {
    return {
      options: {},
    };
  },
  components: {
    Echart,
  },
  props: {
    cdata: {
      type: Object,
      default: () => ({})
    },
  },
  watch: {
    cdata: {
      handler () {
        // 固定样式数据
        // let lineStyle = {
        //   normal: {
        //     width: 1,
        //     opacity: 0.5
        //   }
        // };
        

        this.options = {
      title: {
        // text: '世界人口总量',
        // subtext: '数据来自网络'
    },
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'shadow'
        }
    },
    legend: {
        show: false
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    xAxis: {
        axisLabel: {
            show: true,
            textStyle: {
              color: '#fff'
            },
            formatter: function(value, index) {
                console.log(value)
                return "04-0"+index;
            }
          }
    },
    yAxis: {
        type: 'category',
        data: ['预警1', '预警2', '预警3', '预警4', '预警5', '预警6', '预警7']
    },
    series: [
         {
            name: '辅助',
            type: 'bar',
            stack: '总量',
            itemStyle: {
                barBorderColor: 'rgba(0,0,0,0)',
                color: 'rgba(0,0,0,0)'
            },
            emphasis: {
                itemStyle: {
                    barBorderColor: 'rgba(0,0,0,0)',
                    color: 'rgba(0,0,0,0)'
                }
            },
            data: [50, 1200, 1245, 1530, 1376, 1376, 100]
            // data: ["04-01", "04-02", "04-03", "04-04", "04-05", "04-06", "04-07", "04-08", "04-09", "04-10", "04-11"]
        },
        {
            name: '收入',
            type: 'bar',
            itemStyle: {
						normal: {
							color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [{
								offset: 0,
								color: "#541C3D" // 0% 处的颜色
							}, {
								offset: 0.6,
								color: "#08a4fa" // 60% 处的颜色
							}, {
								offset: 1,
								color: "#01ccfe" // 100% 处的颜色
							}], false)
						}
					},
            stack: '总量',
            label: {
                // show: true,
                position: 'top'
            },
            data: [ 261, 345, 393, 108, 154, 135, 900]
        }
    ]
         
        }
      },
      immediate: true,
      deep: true
    }
  }
};
</script>