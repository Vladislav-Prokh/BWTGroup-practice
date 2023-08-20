<template>
    <div class = "container">
    </div>
  </template>
  
<script>
  export default {
    name: 'App',
    components: {
    },
    data () {
      return {
        city: '',
        region: '',
        country: '',
        weatherApiKey: '5bb9aab286919815e1dd0b0ce116586f',
        geolocationApiKey: 'c3ee06c52efd44b08f2eeade4bc574d9'
      }
    },
    methods: {
      async getGeolocationInformation () {
        const API_URL = 'https://ipgeolocation.abstractapi.com/v1/?api_key=' + this.geolocationApiKey
        const apiResponse = await fetch(API_URL)
        const data = await apiResponse.json()
        const { city, country, region } = data
        this.city = city
        this.region = region
        this.country = country
       
      },
      returnCityNametoParentComp () {
        this.$emit('returnedCityName', {
          cityName:this.city
         })
      }
    },
    async mounted(){
      await this.getGeolocationInformation();
      this.returnCityNametoParentComp()
    }
}
</script>
  
  