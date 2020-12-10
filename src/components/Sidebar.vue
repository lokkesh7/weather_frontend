<template>
  <div id="sidebar" class="col-md-3 col-sm-4 col-xs-12 sidebar">
    <div id="search">
      <input
        id="location-input"
        type="text"
        v-model="city"
        placeholder="City"
        @keyup.enter="emitParentMethod"
      />
      <button id="search-btn" @click="emitParentMethod">
        <img src="../assets/search.svg" width="24" height="24" />
      </button>
    </div>
    <div id="info">
      <div class="wrapper-left">
        <div id="current-weather">
          {{ climate.temp }}
        </div>
        <div id="weather-desc">{{ climate.desc }}</div>
        <div class="temp-max-min">
          Sunrise: {{ climate.sunrise }}
          <br />
          Sunset: {{ climate.sunset }}
        </div>
      </div>
      <div class="wrapper-right">
        <div class="date-time-info">
          <div id="date-desc">
            <img src="../assets/calendar.svg" width="20" height="20" />
            {{ climate.date }}
          </div>
        </div>
        <div class="location-info">
          <div id="location-desc">
            <img
              src="../assets/location.svg"
              width="10.83"
              height="15.83"
              style="opacity: 0.9"
            />
            {{ climate.city }}, {{ climate.country }}
            <div id="location-detail" class="mt-1">
              Lat: {{ climate.coord.lat }}
              <br />
              Long: {{ climate.coord.lon }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, toRefs } from "vue";
export default {
  props: ["weather"],
  setup(props, ctx) {
    const city = ref('')
    const {weather} = toRefs(props)

    const emitParentMethod = () => {
      ctx.emit('searchClick', city.value)
    }
    return { climate: weather, city, emitParentMethod};
  },
};
</script>