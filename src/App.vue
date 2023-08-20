<template>
  <div id = "app">
    <navBar @loadWeather='getWeather' @changeView = 'changeView'/>
    <geolocationRecognizer @returnedCityName='getCityName' ref ="geolocationRecognizer"/>
    <weatherLoader  ref = "weatherLoader" @updateWeatherList="updateWeatherList" @updateIndexOfRecordWithCurrentTime = "updateIndexOfRecordWithCurrentTime"/>
    <weatherPanel :weatherList = 'weatherList' :isTableView='isTableView' :cityName='cityName' :indexOfRecordWithCurrentTime = 'indexOfRecordWithCurrentTime'/>
  </div>
</template>

<script>
import navBar from './components/NavBar.vue'
import geolocationRecognizer from './components/geolocationRecognizer.vue'
import weatherLoader from './components/weatherLoader.vue'
import weatherPanel from './components/weatherPanel.vue'

export default {
  name: 'App',
  components: {
    navBar,geolocationRecognizer,weatherLoader,weatherPanel
  },
  data(){
    return{
      weatherList:[],
      cityName:'',
      isTableView:'',
      indexOfRecordWithCurrentTime:0
    }
  },
  methods:{
    getCityName(name) {
      this.cityName=name.cityName
    },
    getWeather (amountOfDays) { 
      this.$refs.weatherLoader.getWeather(amountOfDays,this.cityName,'ua','metric')
    },
    updateWeatherList (data) {
      this.weatherList = data.weatherList
      console.log(this.weatherList)
    },
    changeView(isTableView){
      this.isTableView = isTableView
    },
    updateIndexOfRecordWithCurrentTime(index){
      this.indexOfRecordWithCurrentTime = index.IndexOfRecordWithCurrentTime
    }

  }
}
</script>

<style>
  #app{
    height: 100%;
    width: 100%;
    background-color:#C1CFEA;
    background-repeat: repeat;
  }
</style>
