<template>
  <client-only>
    <apexchart :height="$vuetify.breakpoint.smAndDown ? '300px' : 'auto'" type="bar" :options="options" :series="series"></apexchart>
  </client-only>
</template>

<script>
export default {
  name: 'BarChart',
  props: ['data', 'max'],
  components: {
    apexchart: () => process.client ? import('vue-apexcharts') : Promise.resolve({ render: h => h('div') })
  },
  data () {
    return {
      options: {
        legend: {
          show: true
        },
        chart: {
          toolbar: {
            show: false
          }
        },
        xaxis: {
          categories: this.data.map(({ title }) => title)
        },
        yaxis: {
          max: parseInt(this.max) || 20
        },
        plotOptions: {
          bar: {
            distributed: false
          }
        }
      },
      series: this.data[0].scores.map(({ title: name }, index) => ({
        name,
        data: this.data.map(({ scores }) => scores[index].score)
      }))
    }
  }
}
</script>
