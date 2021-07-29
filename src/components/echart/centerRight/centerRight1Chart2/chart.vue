<template>
  <div>
    <Echart
      :options="options"
      id="centreRight2Chart333"
      height="4.20rem"
      width="100%"
    ></Echart>
  </div>
</template>

<script>
import Echart from '@/common/echart'
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
  legend: {
        show:false
    },
    toolbox: {
        show: false,
        feature: {
            // mark: {show: true},
            // dataView: {show: true, readOnly: false},
            // restore: {show: true},
            // saveAsImage: {show: true}
        }
    },
    series: [
        {
            name: '面积模式',
            type: 'pie',
            radius: [10, 40],
            center: ['50%', '50%'],
            roseType: 'area',
            itemStyle: {
                borderRadius: 8
            },
            data: [
                {value: 40, name: 'rose 1'},
                {value: 38, name: 'rose 2'},
                {value: 32, name: 'rose 3'},
                {value: 30, name: 'rose 4'},
                // {value: 28, name: 'rose 5'},
                // {value: 26, name: 'rose 6'},
                // {value: 22, name: 'rose 7'},
                // {value: 18, name: 'rose 8'}
            ]
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