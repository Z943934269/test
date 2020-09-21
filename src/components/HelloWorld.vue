<template>
  <div>
    <div class="flex">
      <div @click="resver1"
           class="btn">
        升序
      </div>
      <div @click="resver2"
           class="btn">
        降序
      </div>
    </div>
    <div id="echars"
         style="width:600px;height:400px;">

    </div>
  </div>

</template>

<script>
import * as echarts from 'echarts'
let option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'cross'
    }
  },
  toolbox: {

  },
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: ['01:15', '02:30', '03:45', '05:00', '06:15', '07:30']
  },
  yAxis: {
    type: 'value',
    axisLabel: {
      formatter: '{value} '
    },
    axisPointer: {
      snap: true
    }
  },
  visualMap: {
    show: false,
    dimension: 0,
    pieces: [{
      lte: 6,
      color: 'green'
    }]
  },
  series: [
    {
      name: '',
      type: 'bar',
      smooth: false,
      data: [20, 30, 15, 12, 5, 25],
      markArea: {
        data: []
      }
    }
  ]
};
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      data: [20, 30, 15, 12, 5, 25]
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      this.echartsLine = echarts.init(document.getElementById('echars'))
      this.echartsLine.setOption(option, true)
      this.echartsLine.resize()
    },
    resver1 () {
      this.data = this.data.sort(function (a, b) {
        return a - b
      })
      option.series[0].data = this.data
      this.echartsLine.setOption(option, true)
    },
    resver2 () {
      this.data = this.data.sort(function (a, b) {
        return b - a
      })
      option.series[0].data = this.data
      this.echartsLine.setOption(option, true)
    }
  }
}
</script>
<style scoped>
.btn {
  margin: 0 20px;
  width: 80px;
  height: 80px;
  background: red;
  cursor: pointer;
}
.btn:hover {
  opacity: 0.7;
}
.flex {
  display: flex;
  justify-content: flex-start;
}
</style>