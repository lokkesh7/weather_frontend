<template>
    <div class="highlights-item col-md-4 col-sm-6 col-xs-12 border-top">
        <div>
            <div class="card-heading pt-5">Humidity</div>
            <div class="row pt-4 mt-4">
                <div class="col-sm-12 col-md-12 mt-2 text-center align-middle">
                    <div id="chart">
                        <apexchart :options="chartData" :series="[data]"></apexchart>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import VueApexCharts from "vue3-apexcharts";
export default {
    components: {
        apexchart: VueApexCharts,
    },
    props: ['humidity'],
    setup (props) {
        
        const chartData = reactive({
            chart: {
              type: 'radialBar',
              offsetY: -20,
              sparkline: {
                enabled: true
              }
            },
            plotOptions: {
              radialBar: {
                startAngle: -90,
                endAngle: 90,
                track: {
                  background: "#e7e7e7",
                  strokeWidth: '97%',
                  margin: 5, // margin is in pixels
                  dropShadow: {
                    enabled: true,
                    top: 2,
                    left: 0,
                    color: '#999',
                    opacity: 1,
                    blur: 2
                  }
                },
                dataLabels: {
                  name: {
                    show: false
                  },
                  value: {
                    offsetY: -2,
                    fontSize: '22px'
                  }
                }
              }
            },
            grid: {
              padding: {
                top: -10
              }
            },
            fill: {
              type: 'gradient',
              gradient: {
                shade: 'light',
                shadeIntensity: 0.4,
                inverseColors: false,
                opacityFrom: 1,
                opacityTo: 1,
                stops: [0, 50, 53, 91]
              },
            },
            labels: ['Humidity'],
          })

          const {humidity} = toRefs(props)
        return {data: humidity, chartData}
    }
}
</script>

<style lang="scss" scoped>

</style>