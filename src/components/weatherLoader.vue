<template>
    <div class = "container">
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'App',
    components: {
    },
    data () {
      return {
        weatherList:[],
        weatherApiKey: '5bb9aab286919815e1dd0b0ce116586f'
      }
    },
    methods: {
        getWeather (amountOfDays,cityName,lang,units) {
            var upToThisDate = new Date()
            upToThisDate.setDate(upToThisDate.getDate() + amountOfDays-1);
            const url = `https://api.openweathermap.org/data/2.5/forecast?q=${cityName}&lang=${lang}&units=${units}&appid=${this.weatherApiKey}`
            axios.get(url).then(res => {
                var isRequiredAllWeather = true;
                for (var step = 0; step < res.data.list.length; step++) {
                    if(upToThisDate.getDate() < new Date(res.data.list[step].dt_txt).getDate()){
                        this.weatherList = res.data.list.slice(0,step)
                        isRequiredAllWeather = false
                        break
                    }
                }
                if(isRequiredAllWeather){
                    this.weatherList = res.data.list
                }
                this.makeAmountOfRecordsInArrayMultipleAllTimeFramesOfDay()
                this.groupRecordsByDay()
                this.updateWeatherlist()
                var index = this.findIndexOfRecordWithCurrentTime(this.weatherList)
                this.updateIndexOfRecordWithCurrentTime(index)
            });
        },
        makeAmountOfRecordsInArrayMultipleAllTimeFramesOfDay(){
            var amountOfRecordsForAllTimeFramesOfDay = 8;
                if(this.weatherList.length % amountOfRecordsForAllTimeFramesOfDay != 0){
                    var amountOfRequiredRecords = (Math.trunc(this.weatherList.length/amountOfRecordsForAllTimeFramesOfDay)+1)*amountOfRecordsForAllTimeFramesOfDay- this.weatherList.length;
                    for(var i = 0; i< amountOfRequiredRecords;i++){
                        this.weatherList.unshift({dt_txt:'-',main:{temp:''},wind:{speed:0}})
                    }
            }
        },
        groupRecordsByDay(){
            var groupedRecordsDayObj = new Object();
                var groupedRecordsArr = []
                for(var i =0;i<this.weatherList.length;i++){
                    groupedRecordsDayObj[i] = this.weatherList[i]
                    if((i+1)%8===0){   
                        groupedRecordsArr.push(groupedRecordsDayObj)
                        groupedRecordsDayObj = new Object();
                    }
                }
                this.weatherList = groupedRecordsArr
        },
        updateWeatherlist () {
        this.$emit('updateWeatherList', {
             weatherList:this.weatherList
         })
        },
        findIndexOfRecordWithCurrentTime(list){
            for(var i = 0;i < 8;i++){
                if(list[0][i].dt_txt !== '-'){
                    return i;
                }
            }
            return undefined;
        },
        updateIndexOfRecordWithCurrentTime(index){
            this.$emit('updateIndexOfRecordWithCurrentTime', {
                IndexOfRecordWithCurrentTime:index
         })
        }
    },
}
</script>