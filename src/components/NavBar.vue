<template>

<div class = "root">
    <nav class="navbar navbar-light" style="background-color: #5DB0E5;">
            <a class="navbar-brand" href="#">WeatherApp</a>
            <div class="d-flex btn-group mx-auto" role="group" aria-label="Basic example">
                <button type="button" class="btn btn-primary" v-on:click="loadWeather(1)">Today</button>
                <button type="button" class="btn btn-primary" v-on:click="loadWeather(2)">Tomorrow</button>
                <button type="button" class="btn btn-primary" v-on:click="loadWeather(3)">3 days</button>
                <button type="button" class="btn btn-primary" v-on:click="loadWeather(4)">4 days</button>
                <button type="button" class="btn btn-primary" v-on:click="loadWeather(5)">5 days</button>
            </div>
        <SwitcherPanelDesign @changeView = 'changeView'/>
    </nav>
</div>

</template>

<script>
import '../../public/styles/mainStyles.css'
import SwitcherPanelDesign from './SwitcherPanelDesign.vue';

export default{
    name:"navBar",
    components :{
        SwitcherPanelDesign
    },
    methods:{
        loadWeather(amountOfDays){
            this.$emit('loadWeather',amountOfDays)
        },
        changeView(data){
            this.$emit('changeView',data.isTableView)
        }
    }
}
</script>
