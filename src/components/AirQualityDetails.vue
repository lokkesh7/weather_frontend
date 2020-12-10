<template>
    <div class="custom-content-card content-card card">
    <div class="card-body pb-0">
    <div class="content-header h4 text-center pt-2 pb-3">Air Quality Details</div>
      <div class="row">
          <wind-details :windData="wind"/>
          <visibilty :visibility="visibility"/>
          <humidity :humidity="airHumidity" />
      </div>
    </div>
  </div>
</template>

<script>
import { toRefs } from 'vue'
import windDetails from "./windDetails.vue"
import Visibilty from './Visibilty.vue'
import Humidity from './humidity.vue'

export default {
    components: { windDetails, Visibilty, Humidity },
    props: ['windStatus', 'airVisibility', 'humidity'],
    setup (props) {
        const {windStatus,airVisibility, humidity} = toRefs(props)
        return {wind:windStatus, visibility: airVisibility, airHumidity: humidity}
    }
}
</script>

<style lang="scss" scoped>

</style>