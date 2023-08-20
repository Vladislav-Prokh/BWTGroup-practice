<template class = "template w-auto h-auto">
 <div class="container py-5 h-100 overflow-hidden" v-if="isTableView">
    <div class = "row" style ="margin: 10%;" >
       
          <table class="weatherTable table table-striped me-3">
                      <thead>
                        <tr>
                          <th scope="col">#</th>
                          <th scope="col">00:00</th>
                          <th scope="col">03:00</th>
                          <th scope="col">06:00</th>
                          <th scope="col">09:00</th>
                          <th scope="col">12:00</th>
                          <th scope="col">15:00</th>
                          <th scope="col">18:00</th>
                          <th scope="col">21:00</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for ="(dayWeatherRecord,index) in weatherList" :key="index">
                          <th scope="row">{{ dayWeatherRecord[index*8+indexOfRecordWithCurrentTime].dt_txt.slice(0,11)}}</th>
                          <td  v-for ="(timeWeatherRecord,index) in dayWeatherRecord" :key="index">
                          <span v-if="timeWeatherRecord.dt_txt!='-'">{{ timeWeatherRecord.main.temp }}°C</span>
                          <span v-else>-</span>
                          </td>
                        </tr>
                      </tbody>
              </table>
        </div>
    </div>
 <div class = "container-fluid" v-else>
  <section class="card_section vh-auto">
    <div class="container py-5 h-100">
      <div class="row col-12 d-flex justify-content-center align-items-center h-auto" style="color: #282828;">
        <div class="wrap col-12 mx-auto d-lg-flex justify-content-center" style ="flex-wrap:wrap">
          <div class="card col-sm-12 col-md-5 m-4 gradient-custom " style="border-radius: 25px;" v-for ="(dayWeatherRecord,index) in weatherList" :key="index">
            <div class="card-body p-4">
              <div id="demo1" class="carousel slide" data-ride="carousel">
                <!-- Carousel inner -->
                <div class="carousel-inner">
                  <div class="carousel-item active">
                    <div class="d-flex justify-content-between mb-4 pb-2">
                      <h6><strong >{{new Date(dayWeatherRecord[index*8+indexOfRecordWithCurrentTime].dt_txt).toString().slice(0,21) }}</strong></h6>
                      <div v-if="index==0">
                        <h2 class="display-2"><strong >{{dayWeatherRecord[indexOfRecordWithCurrentTime].main.temp.toFixed(1)}}°C</strong></h2>
                        <p class="text-muted mb-0 ms-0">{{ cityName }}</p>
                      </div>
                      <div v-else>
                        <h2 class="display-2"><strong >{{dayWeatherRecord[index*8+indexOfRecordWithCurrentTime].main.temp.toFixed(1)}}°C</strong></h2>
                        <p class="text-muted mb-0 ms-0">{{ cityName }}</p>
                      </div>
                      <div class = "mainWeatherImgItem mx-auto" >
                        <img class = "mainWeatherImg" :src="`https://openweathermap.org/img/wn/${dayWeatherRecord[index*8+indexOfRecordWithCurrentTime].weather[0].icon}@2x.png`">
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div id="demo2" class="carousel slide" data-ride="carousel">
                      <div class="carousel-inner">
                          <div class="carousel-item active">
                            <div class="d-flex justify-content-around text-center mb-4 pb-3 pt-2">
                                <div class="flex-column" v-for ="(timeWeatherRecord,index) in dayWeatherRecord" :key="index+1">
                                    <div class = "wrapp" >
                                        <div  v-if="timeWeatherRecord.dt_txt!='-'">
                                            <p class="mb-0 text-muted" style="font-size: .60rem;">Time</p>
                                            <p class="mb-0"><strong>{{ timeWeatherRecord.dt_txt.slice(11,16)}}</strong></p>
                                            <p class="small my-3"><strong>{{timeWeatherRecord.main.temp.toFixed(1)}}°C</strong></p>
                                            <p class="mb-0 text-muted" style="font-size: .60rem;">Wind speed</p>
                                            <p class="mb-0"><strong>{{timeWeatherRecord.wind.speed}}</strong></p>
                                            <p class="mb-0 my-1"><strong>{{ timeWeatherRecord.weather[0].main}}</strong></p>
                                        </div>
                                        <div v-else>
                                          {{ timeWeatherRecord.dt_txt }}
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </div>
                      </div>
                </div>
            </div>
          </div>
          </div>
        </div>
      </div>
    </section>
 </div>
</template>

<script>
    export default{
        name:"weatherPanel",
        props:{
            weatherList:[],
            isTableView:Boolean,
            cityName:String,
            indexOfRecordWithCurrentTime: Number
        },
    }
</script>

<style>
#root{
 height: 100%;
 width: 100%;
}
.card_section{
  height: 100%;
 width: 100%;
}
.mainWeatherImgItem{
  width: 100px;
  height: 100px;
}
.mainWeatherImgItem .mainWeatherImg{
  width:150;
  height:120;
}
.card{
  display: inline-block;
}
</style>