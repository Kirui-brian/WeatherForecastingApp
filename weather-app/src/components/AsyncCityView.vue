<template>
    <div class="flex flex-col flex-1 items-center">
        <!-- Banner -->
        <div v-if="route.query.preview" class="text-white p-4 bg-weather-secondary w-full text-center">
            <p>You are currently previewing this location, click on the '+' icon to add it on your homepage.</p>
        </div>
        <!-- Weather Overview -->
        <div class="flex flex-col items-center text-white py-12">
            <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
            <p class="text-sm mb-12">
                {{ 
                    new Data(weatherData.currentTime).toLocaleDateString(
                        'en-us',
                        {
                            weekday:'short',
                            day: '2-digit',
                            month: 'long',
                        }
                    ) 
                }}
                {{ 
                    new Date(weatherData.currentTime).toLocaleTimeString(
                        'en-us',
                        {
                            timeStyle: 'short',
                        }
                    )
                 }}
            </p>
            <p class="text-8xl mb-8">
                {{ Math.round(weatherData.current.temp) }}&deg;
            </p>
            <div class="text-center">
                <p>Feels like
                    {{ Math.round(weatherData.current.feels_like) }}&deg;
                </p>
                <p class="capitalize">
                    {{ weatherData.current.weather[0].description }}
                </p>
            </div>
        </div>
    </div>
</template>

<script setup>
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute(axios);
const getWeatherData = async () => {
    try {
        const weatherData = await axios.get(``);
        // calculate current date & time
        const localOffset = new Date().getTimezoneOffset() * 60000;
        const utc = weatherData.data.current.dt * 1000 + localOffset.getTimezoneOffset();
        weatherData.data.currentTime = utc + 1000 * weatherData.data.timezone_offset;

        //calculate hourly weather offset
        weatherData.data.hourly.forEach((hour) => {
            const utc = hour.dt * 1000 + localOffset;
        });

        return weatherData.data;
    } catch (error) {
        console.log(error);
    }
}
const weatherData = await getWeatherData();
</script>
