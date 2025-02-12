<script setup>
import VueApexCharts from 'vue3-apexcharts';
import { reactive, onMounted } from 'vue';
import axios from 'axios';

const state = reactive({
        timeseries: [],
        germanyData: [],
        greeceData: [],
        franceData: [],
        timeData: [],
        lineSeries: [],
        lineOptions: {}
});

onMounted(async () =>{
        try {
            const response = await axios.get('/api/timeseries')
            state.timeseries = response.data;
            state.germanyData = response.data.map((item) => item.ENTSOE_DE_DAM_Price);
            state.greeceData = response.data.map((item) => item.ENTSOE_GR_DAM_Price);
            state.franceData = response.data.map((item) => item.ENTSOE_FR_DAM_Price);
            state.timeData = response.data.map((item) => item.DateTime);            
            state.lineSeries = [
                
                    {
                        name: 'DE Price',
                        data: state.germanyData
                    },
                    {
                        name: 'GR Price',
                        data: state.greeceData
                    },
                    {
                        name: 'FR Price',
                        data: state.franceData
                    }    
                
            ];
            
            state.lineOptions = {
                xaxis: {
                    categories: state.timeData
                    }
            }
        } catch (error) {
            console.error('Error fetching jobs', error)
        } 
    });


</script>


<template>
    <div class="gap-16 p-24 items-center bg-blue-50">
        <h1 class="flex justify-center">Time Series Chart</h1>
        <VueApexCharts type="line" :series="state.lineSeries" :options="state.lineOptions" />
    </div>
</template>