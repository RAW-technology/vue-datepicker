<template>
    <div class="wrapper">
        <Datepicker v-model="selectedDate" placeholder="Select Date" :min-date="new Date()" :format="format" :range="true" :enable-time-picker="false"  />
    </div>
</template>

<script lang="ts" setup>
import { ref, watch, provide } from 'vue';
import Datepicker from '../src/VueDatePicker/VueDatePicker.vue';


const selectedDate = ref<Date | [Date, Date] | null>(null);
    const handleDateSelected = (date) => {
  // Handle the received date here
  console.log('Date selected:', date);
};

provide('handleDateSelected', handleDateSelected);


const format = (selectedDate: Date | [Date, Date] | null): string => {
    if (!selectedDate) return '';

    const formatDate = (date: Date): string => {
    if (!(date instanceof Date)) return ''; 
        const day = date.getDate();
        const month = date.getMonth() + 1;
        const year = date.getFullYear();
        return `${day}/${month}/${year}`;
    };

    if (Array.isArray(selectedDate)) {
        if (selectedDate.length > 1) {
            const [start, end] = selectedDate;
            return `${formatDate(start)} - ${formatDate(end)}`;
        } else {
            return formatDate(selectedDate[0]);
        }
        } else {
            return formatDate(selectedDate);
        }
}


watch(selectedDate, (newValue) => {
  console.log('Selected Date:', newValue);
});
</script>
  
  


<style lang="scss">
    @import 'src/VueDatePicker/style/main';
    .wrapper {
        padding: 200px;
    }
</style>
