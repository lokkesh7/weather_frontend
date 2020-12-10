<template>
  <div id="root">
    <div class="container-fluid" id="app">
      <div class="row">
        <sidebar :weather="weather" @searchClick="fetchCityWeather"/>
        <main-dashboard
          class="col-md-9 col-sm-8 col-xs-12 content"
          id="dashboard-content"
          :tempDetails="tempDetails"
          :windStatus="windStatus"
          :visibility="visibility"
          :airHumidity="humidity"
        />
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import Sidebar from "./components/Sidebar.vue";
import MainDashboard from "./components/MainDashboard.vue";
import { onMounted, ref, reactive } from 'vue';
import axios from 'axios'

export default {
  name: "App",
  components: {
    sidebar: Sidebar,
    "main-dashboard": MainDashboard,
  },
  setup() {

    const KelvinToCelcius = (temp) => `${Math.round(temp - 273.15)}°C`

    const weather= reactive({coord: {}})
    const tempDetails = reactive({})
    const windStatus = reactive({})
    const humidity = ref(0)
    const visibility = ref(0)

    const fetchCityWeather = (city) => {
      axios.get(`http://localhost:8000/api/get_city_weather/${city}`)
      .then(resp => {
        const data = resp.data.data[0]._source.weather[0]


        weather.temp = KelvinToCelcius(data.main.temp)
        weather.desc = data.weather[0].description
        weather.city = data.name
        weather.country = data.sys.country
        weather.coord.lat = data.coord.lat
        weather.coord.lon = data.coord.lon
        weather.date = moment(data.dt * 1000).format('DD/MM/YY')
        weather.sunrise = moment(data.sys.sunrise * 1000).format('LT')
        weather.sunset = moment(data.sys.sunset * 1000).format('LT')
        
        tempDetails.minTemp = KelvinToCelcius(data.main.temp_min)
        tempDetails.maxTemp = KelvinToCelcius(data.main.temp_max)
        tempDetails.feelsLike = KelvinToCelcius(data.main.feels_like)
        tempDetails.pressure = `${data.main.pressure / 100} bar`


        windStatus.speed = data.wind.speed
        windStatus.deg = data.wind.deg

        visibility.value = `${data.visibility/1000} km`
        humidity.value = data.main.humidity
      })
      .catch(err => console.log(err))
    }

    onMounted(() => {
      fetchCityWeather('chennai')
      
    })
      
    return {
      weather,
      tempDetails,
      windStatus,
      visibility,
      humidity,
      fetchCityWeather
    };
  },
};
</script>

<style>
@import "./css/styles.css";
</style>
