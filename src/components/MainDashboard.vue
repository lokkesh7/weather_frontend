<template>
    <div  class="dashboard">
      <temperature-details :tempDetails="tempValues" />
      <air-quality-details :windStatus="windDetails" :airVisibility="airVisibility" :humidity="humidity"/>
  </div>
</template>

<script>
import {  toRefs } from 'vue'
import AirQualityDetails from './AirQualityDetails.vue'
import TempDetails from './TempDetails.vue'
export default {
    props:['tempDetails', 'windStatus', 'visibility', 'airHumidity'],
    components: {
        'temperature-details':TempDetails,
        AirQualityDetails
    },
    setup (props) {
        const {tempDetails, windStatus, visibility, airHumidity} = toRefs(props)
        return {tempValues: tempDetails, windDetails: windStatus, airVisibility: visibility, humidity: airHumidity}
    }
}
</script>

<style scoped>
    .dashboard {
        position: relative;
    }
</style>