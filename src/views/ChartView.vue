<template>
  <div>
    <line-chart :labels="chartLabels" :datasets="chartDatasets"></line-chart>
    <bar-chart :labels="chartLabels" :datasets="chartDatasets"></bar-chart>
  </div>
</template>

<script>
import LineChart from "../components/Charts/LineChart.vue"
import BarChart from "../components/Charts/BarChart.vue"
export default {
  name: 'ChartView',

  components: {
    LineChart,
    BarChart
  },
  data() {
    return {
      chartLabels: [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July'
      ],
      chartDatasets: [
        {
          label: 'Data One',
          backgroundColor: '#f87979',
          data: [40, 39, 10, 40, 39, 80, 40]
        }
      ]
    }
  },
  methods:{
    addData()
    {
      // console.log(this.chartDatasets[0].data.push(100))
      // this.chartDatasets[0].data.push(Math.floor(Math.random() * 100));
      // this.chartLabels.push("")
      // setTimeout(()=>{this.addData()}, 1000);
    }
  },
  created()
  {
    this.addData();
  }
}
</script>
