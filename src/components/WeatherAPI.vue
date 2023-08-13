<script setup>
import { onBeforeMount,ref } from 'vue';

const baseURL = "http://api.weatherapi.com/v1/"
const apiKey = '5ad3c720a98944c18cb41011232006'
const apiURL = baseURL + 'forecast.json?q=Khulna&lang=Bn&key='+apiKey

let data = ref('');

onBeforeMount(async () =>{
   try {
    data.value = await fetch(apiURL)
        .then(res => res.json())
        
    console.log(data.value)
   } catch (e) {
    console.log('Error fetching data', e)
   }
})
</script>
<template>
    <div class="mx-auto items">
        <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
            <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                <tbody >
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>তাপমাত্রা</td>
                        <td id="tempc">{{ data.current.temp_c }}</td>
                        <td id="tempf">{{ data.current.temp_f }}</td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>রিয়েল ফিল</td>
                        <td id="feelslikec">{{ data.current.feelslike_c }}</td>
                        <td id="feelslikef">{{ data.current.feelslike_f }}</td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>আকাশের অবস্থা</td>
                        <td id="skyconditiontxt"><img height="50px" :src="data.current.condition.icon"/></td>
                        <td id="skyconditionimg">{{ data.current.condition.text }}</td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>বাতাসের আদ্রতা</td>
                        <td id="humidity" colspan="2">{{ data.current.humidity }}</td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>UV Index</td>
                        <td id="uv" colspan="2">{{ data.current.uv }}</td>
                    </tr>
                    <tr class="border-b border-gray-200 dark:border-gray-700">
                        <td>বাতাসের গতিবেগ</td>
                        <td id="wind_kph">{{ data.current.wind_kph }}</td>
                        <td id="wind_mph">{{ data.current.wind_mph }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>