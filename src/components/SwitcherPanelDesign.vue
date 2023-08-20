<template>
    <div id = "container">
        <div class="form-check form-switch d-flex justify-content-end me-2">
               
                <input class="form-check-input" type="checkbox" id="flexSwitchCheckChecked" checked  v-on:click="changeView()">
                <label class="form-check-label" for="flexSwitchCheckChecked">Табличное отображение</label>
        </div>
    </div>
</template>

<script>
 export default {
    name: 'SwitcherPanelDesign.vue',
    data(){
        return{
            isTableView: true
        }
    },
    methods:{
        changeView(){
            this.isTableView = !this.isTableView;
            this.$emit('changeView', {
                isTableView:this.isTableView
         })
        }
    }
 }
</script>