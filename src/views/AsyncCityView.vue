<template>
    <div>

    <div class="flex flex-col flex-1 items-center">
        <!-- Banner -->
        <div 
        v-if="route.query.preview" class="text-white p-4 bg-weather-secondary w-full text-center">
            <p>You are currently previewing this city, click the + icon to start tracking this city.</p>
        </div>
        <!-- Weather overview -->
        <div class="flex flex-col items-center text-white py-12">
            <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
                <p class="text-sm mb-12">
                    {{ 
                        new Date(weatherData.currentTime).toLocaleDateString(
                            "en-us",
                            {
                                weekday: "short",
                                day: "2-digit",
                                month: "long",
                            }
                        )
                    }}
                    {{ 
                        new Date(weatherData.currentTime).toLocaleTimeString(
                            "en-us",
                            {
                                timeStyle: "short",
                            }
                        )
                    }}
                </p>
                <p class="text-8xl mb-8">
                    {{ Math.round(weatherData.current.temp) }}&deg;
                </p>
        </div>
    </div>
    </div>
</template>

<script setup>
    const route = useRoute()
    const getWeatherData = async () => {
        try {
            const weatherData = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${route.query.lat}&lon=${route.query.lng}&exclude={part}&appid=APPID&units=imperial`);
            
            //cal current date & time
            const localOffset = new Date().getTimezoneOffset() * 60000;
            utc + 1000 * weatherData.data.timezone_offset;
            
            return weatherData.data;
        } catch(err) {
            console.error(err);
        }
    };
    const weatherData = await getWeatherData();
    console.log(weatherData);
</script>