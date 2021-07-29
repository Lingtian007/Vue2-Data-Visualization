<template>
  <div>
    <div style="width: 800px; height: 400px"
    id="maps"
             class="map"
             ref="map" />
  </div>
</template>

<script>
// import Echart from '@/common/echart';
import echarts from 'echarts'
import getCityLists from './sd.json'

export default {
  data() {
    return {
      data:[], // 坐标点数据，格式 {name: 'xxx', value: [经度,纬度]}
      option: {
        title: {
          left: 'center',
          textStyle: {
            fontSize: 16,
          }
        }
      },
    };
  },
  components: {

  },
  props: {
    cdata: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    cdata: {
      handler() {
     
       
      },
      immediate: true,
      deep: true,
    },
  },
   mounted() { 
      this.drowmap();
  },
  methods: {
    drowmap(){
  echarts.registerMap("shandong", getCityLists);
  let myChart = echarts.init(document.getElementById('maps'))
        myChart.hideLoading();
        let geoCoordMap = {
          济南市: [117.121225, 36.66466],
          菏泽市: [115.480656, 35.23375],
          济宁市: [116.59, 35.38],
          德州市: [116.39, 37.45],
          聊城市: [115.97, 36.45],
          泰安市: [117.13, 36.18],
          临沂市: [118.35, 35.05],
          淄博市: [118.05, 36.78],
          枣庄市: [117.57, 34.86],
          滨州市: [118.03, 37.36],
          潍坊市: [119.1, 36.62],
          东营市: [118.49, 37.46],
          青岛市: [120.3, 36.62],
          烟台市: [120.9, 37.32],
          威海市: [122.1, 37.2],
          日照市: [119.1, 35.62]
        };
        let data = [];
        let dataitem = [
           {
            name: '济南市',
          },
          {
            name: '菏泽市',
          },
          {
            name: '济宁市',
          },
          {
            name: '德州市',
          },
          {
            name: '聊城市',
          },
          {
            name: '泰安市',
          },
          {
            name: '临沂市',
          },
          {
            name: '淄博市',
          },
          {
            name: '枣庄市',
          },
          {
            name: '滨州市',
          },
          {
            name: '潍坊市',
          },
          {
            name: '东营市',
          },
          {
            name: '青岛市',
          },
          {
            name: '烟台市',
          },
          {
            name: '威海市',
          },
          {
            name: '日照市',
          },
        ];
        dataitem.forEach(item => {  //这里是渲染对象，转换成你需要的格式，但是name,value不可改动哦！！！！！！
          let o = {
            name: item.city,
            value: 111,   //value只是用于下方显示颜色用，随意设定数字
            // 字段名：item.某某某
          };
          data.push(o);
        });
        let convertData = function(data) {
          let res = [];
          for (let i = 0; i < data.length; i++) {
            let geoCoord = geoCoordMap[data[i].name];
            if (geoCoord) {
              res.push({
                name: data[i].name,
                value: geoCoord.concat(data[i].value),
                //  提示框如需配置其他请获取定义 O 里相应的字段名即可
              });
            }
          }
          return res;
        };
 
        let option = {
          legend: {
            show: false
          },
          tooltip: {
            padding: 0,
            enterable: true,
            transitionDuration: 1,
            textStyle: {
              color: "#000",
              decoration: "none"
            },
            formatter: function() {
              let tipHtml = "";
              // tipHtml =
              //   '<div>" +
              //       字符串拼接你需要的样式div
              //   "</div>";
              return tipHtml;
            }
          },
          visualMap: {
            show: false,
            x: "left",
            y: "center",
            seriesIndex: [1],
            textStyle: {
              color: "#fff"
            },
            inRange: {
              color: ["#009ef4"]  // 你地图需要的配色设置，这里只做统一配色
            }
          },
          geo: {
            map: "shandong",
            zoom: 1.2,
            left: "25%",
            itemStyle: {
              //地图区域的多边形 图形样式
              // color: "transparent",
              areaColor: 'transparent', // 背景透明
              normal: {
                borderWidth: 1,
                // borderColor: "rgba(37,124,169)",
                // shadowColor: "#e8e8e8",
                // shadowOffsetY: 15,
                // shadowOffsetX: 8
              }
            }
          },
          series: [
                {
              type: 'scatter',
              coordinateSystem: 'geo',
              symbolSize: 27,
              effectType: 'ripple',
              legendHoverLink: false,
              showEffectOn: 'render',
              rippleEffect: {
                period: 4,
                scale: 2.5,
                brushType: 'stroke',
              },
              zlevel: 1,
              itemStyle: {
                normal: {
                  color: function(params) {
                    var colorList = ['#D4262F', '#AADE6C', '#FFE211'];
                    if (params.name == "菏泽市") { 
                     return colorList[0]
                    } else if (params.name == "威海市") {
                      return colorList[1]
                    }else if (params.name == "潍坊市") {
                      return colorList[2]
                    }else {
                      return "#FFF"
                    }
                  },
                  // shadowBlur: 5,
                  // shadowColor: '#fff',
                },
              },
              data: convertData(dataitem ),
            },
            {
              type: "map",
              mapType: "shandong",
              left: "25%",
              zoom: 1.2,
              roam: false, //是否开启鼠标缩放和平移漫游
              showLegendSymbol: false,
              label: {
                show: false
              },
              itemStyle: {
                //地图区域的多边形 图形样式
                normal: {
                  borderWidth: 1,
                  borderColor: "#6A84BD",
                  areaColor: "#2B2740"
                },
                emphasis: {
                  //是图形在高亮状态下的样式,比如在鼠标悬浮或者图例联动高亮时
                  label: {
                    show: false,
                    textStyle: {
                      color: "transparent"
                    }
                  },
                  borderColor: "#6A84BD",
                  areaColor: "#6A84BD"
                }
              },
              data: data
            }
          ]
        };
 
        if (option && typeof option === "object") {
          myChart.setOption(option, true);
        }

    },
    // 开启定时器
    startInterval() {
      const _self = this;
      // 应通过接口获取配置时间，暂时写死5s
      const time = 2000;
      if (this.intervalId !== null) {
        clearInterval(this.intervalId);
      }
      this.intervalId = setInterval(() => {
        _self.reSelectMapRandomArea();
      }, time);
    },
    // 重新随机选中地图区域
    reSelectMapRandomArea() {
      const length = 9;
      this.$nextTick(() => {
        const map = this.$refs.centreLeft2ChartRef.chart;
        let index = Math.floor(Math.random() * length);
        while (index === this.preSelectMapIndex || index >= length) {
          index = Math.floor(Math.random() * length);
        }
        map.dispatchAction({
          type: 'mapUnSelect',
          seriesIndex: 0,
          dataIndex: this.preSelectMapIndex,
        });
        map.dispatchAction({
          type: 'showTip',
          seriesIndex: 0,
          dataIndex: index,
        });
        map.dispatchAction({
          type: 'mapSelect',
          seriesIndex: 0,
          dataIndex: index,
        });
        this.preSelectMapIndex = index;
      });
    },
    handleMapRandomSelect() {
      this.$nextTick(() => {
        // const map = this.$refs.centreLeft2ChartRef.chart;
        // const _self = this;
        // setTimeout(() => {
        //   _self.reSelectMapRandomArea();
        // }, 0);
        // // 移入区域，清除定时器、取消之前选中并选中当前
        // map.on('mouseover', function (params) {
          // clearInterval(_self.intervalId);
          // map.dispatchAction({
          //   type: 'mapUnSelect',
          //   seriesIndex: 0,
          //   dataIndex: _self.preSelectMapIndex,
          // });
          // map.dispatchAction({
          //   type: 'mapSelect',
          //   seriesIndex: 0,
          //   dataIndex: params.dataIndex,
          // });
          // _self.preSelectMapIndex = params.dataIndex;
        // });
        // 移出区域重新随机选中地图区域，并开启定时器
        // map.on('globalout', function () {
        //   _self.reSelectMapRandomArea();
        //   // _self.startInterval();
        // });
        // this.startInterval();
      });
    },
  },
};
</script>
