<script setup lang="ts">
import { LineChart } from 'echarts/charts'
import { use } from 'echarts/core'
import {
  TooltipComponent,
  LegendComponent,
  GridComponent,
  VisualMapComponent,
  DataZoomComponent,
  TitleComponent
} from 'echarts/components'
import { SVGRenderer } from 'echarts/renderers'
import { onMounted, reactive, ref } from 'vue'
import VChart from 'vue-echarts'
use([
  SVGRenderer,
  LineChart,
  TitleComponent,
  TooltipComponent,
  LegendComponent,
  GridComponent,
  VisualMapComponent,
  DataZoomComponent
])
const initOption = {
  devicePixelRatio: 2,
  renderer: 'svg'
}
const lineChart = ref()
const lineOption = reactive<any>({
  tooltip: {
    trigger: 'axis',
    textStyle: {
      fontSize: 16
    }
  },
  grid: {
    top: '14%',
    left: '8%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  // dataZoom: [
  //   {
  //     show: true,
  //     type: 'inside',
  //     filterMode: 'none',
  //     xAxisIndex: [0],
  //     startValue: yAxisData.value[0],
  //     endValue: yAxisData.value[yAxisData.value.length - 1],
  //   },
  // ],
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data:  ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    axisLabel: {
      color: '#00B9FC',
      interval: 0
    },
    splitLine: {
      interval: 0
    },
    axisTick: {
      interval: 0
    }
  },
  color: ['#5dc992'],
  yAxis: [
    {
      type: 'value',
      name: '设备数量(台)',
      splitLine: {
        lineStyle: {
          type: 'dashed',
          color: ['#353A4E'],
          dashoffset: 15
        }
      },
      nameTextStyle: {
        color: '#fff'
      },
      axisLabel: {
        color: '#fff'
      }
    }
  ],
  series: [
    {
      name: 'test',
      type: 'line',
      showAllSymbol: false,
      yAxisIndex: 0,
      data: [150, 230, 224, 218, 135, 147, 260],
    }
  ]
})
onMounted(() => {
  lineChart.value.resize()
})
</script>

<template>
  <main>
    <h1>This is an home page</h1>
    <div style="width: 500px;height:500px">
      <v-chart ref="lineChart" :init-option="initOption" :option="lineOption" />
    </div>
  </main>
</template>
