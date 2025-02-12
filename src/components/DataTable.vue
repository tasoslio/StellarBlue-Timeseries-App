<script setup>
import { ref, onMounted, reactive} from 'vue';
import { AgGridVue } from "ag-grid-vue3";
import { AllCommunityModule, ModuleRegistry} from 'ag-grid-community';
import axios from 'axios'; 
import moment from 'moment';
import { useToast } from 'vue-toastification';

// Register all Community features
ModuleRegistry.registerModules([AllCommunityModule]);

const toast = useToast();


const formatTimestamp = (timestamp) => {
        return moment(timestamp).format('DD-MM-YYYY HH:mm');
};

const formatToTimestamp = (formattedDate) => {
      return moment(formattedDate, 'DD-MM-YYYY HH:mm').format('YYYY-MM-DDTHH:mm:ss');
    };

const state = reactive({
        timeseries: [],

    });


    onMounted(async () =>{
        try {
            const response = await axios.get('/api/timeseries')
            
            for (let i = 0; i < response.data.length; i++) {
                response.data[i].DateTime = formatTimestamp(response.data[i].DateTime);
                
            }
            state.timeseries = response.data;
            
        } catch (error) {
            console.error('Error fetching jobs', error)
        } 
    });

const colDefs = ref([
        { field: "DateTime"},
        { field: "ENTSOE_DE_DAM_Price" , editable: true},
        { field: "ENTSOE_GR_DAM_Price", editable: true},
        { field: "ENTSOE_FR_DAM_Price", editable: true }
    ]);

    const onCellValueChanged = async (event) => {
    
        const updatedRow = {
            ENTSOE_DE_DAM_Price: event.data.ENTSOE_DE_DAM_Price,
            ENTSOE_GR_DAM_Price: event.data.ENTSOE_GR_DAM_Price,
            ENTSOE_FR_DAM_Price: event.data.ENTSOE_FR_DAM_Price,
        };

        if (event.value >= -200 && event.value <= 200) {
            try {
            const response = await axios.put(`/api/timeseries/${formatToTimestamp(event.data.DateTime)}`, updatedRow);
            toast.success('Row Updated Successfully');
            setTimeout(function(){location.reload()}, 2000);

        } catch (error) {
            console.error('Error fetching jobs', error);
            toast.error('Row was not updated.');

        }
        } else {
            toast.error('Enter valid inputs from -200 to 200');
            setTimeout(function(){location.reload()}, 2000);
        }
        
    }


</script>


<template>

        <div class="flex justify-center overflow-x-auto shadow-md sm:rounded-lg"> 
            <ag-grid-vue :rowData="state.timeseries" :pagination="true"  @cell-value-changed="onCellValueChanged" :columnDefs="colDefs" style="height: 500px; width: 65%;">

            </ag-grid-vue>
        </div>
       
        

</template>