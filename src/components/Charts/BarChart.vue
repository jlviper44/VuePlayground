<template>
  <BarChartGenerator
    :chart-options="chartOptions"
    :chart-data="chartData"
  />
</template>

<script>
import { Bar as BarChartGenerator } from 'vue-chartjs/legacy'

import {
  Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale
} from 'chart.js'

ChartJS.register(
  Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale
)

export default {
  name: 'LineChart',
  components: {
    BarChartGenerator
  },
  props: {
    labels: {
      type: Array,
      default: () => []
    },
    datasets: {
      type: Array,
      default: () => []
    },
  },
  data() {
    return {
      chartData: {
        labels: [],
        datasets: []
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  methods: {
    getData()
    {
      this.chartData.labels = this.labels;
      this.chartData.datasets = this.datasets;
    }
  },
  created()
  {
    this.getData();
  },
  watch: {
    labels()
    {
      this.getData();
    },
    datasets()
    {
      this.getData();
    }
  }
}
</script>
