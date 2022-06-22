<script lang="ts">

    import { onMount } from "svelte";
    import axios from "axios";

    const endpoint = 'https://weatherdbi.herokuapp.com/data/weather/innopolis';

    let weather : {
        currentConditions: any,
    }
    
    let weather_text_c: string;
    let weather_text_f: string;
    let weather_text_h: string;
    let weather_text_v: string;
    let weather_image_url: string;

    onMount(async function () {
        const response = await axios.get(endpoint);
        weather = response.data;
        const weather_api = weather.currentConditions;
        weather_text_c = weather_api.temp.c;
        weather_text_f = weather_api.temp.f;
        weather_text_h = weather_api.humidity;
        weather_text_v = weather_api.wind.km;
        weather_image_url = weather_api.iconURL;
    });

</script>

<main>
    
    <div class="weather">
        <div class="block_info">
            <h2 class="title">Temperature</h2>
            <div class="flex_container">
                <div class="left_part">
                    <div>
                        <span class="just_text">The weather in Celcium is {weather_text_c || "please wait"} </span>
                    </div>
                    <div class="margin_up m1">
                        <span class="just_text">The weather in Fahrenheit is {weather_text_f || "please wait"} </span>
                    </div>
                    <div class="margin_up m2">
                        <span class="just_text">The humidity now is {weather_text_h || "please wait"} </span>
                    </div>
                    <div class="margin_up m3">
                        <span class="just_text">The velocity of wind is {weather_text_v || "please wait"}km/h</span>
                    </div>
                </div>
                <div class="right_part">
                    <img class="weather_image" src={weather_image_url} alt="Please wait">
                </div>
            </div>
        </div>
    </div>
</main>

<style>

    .title {
        font-size: 50px;
        text-align: center;
    }

    .weather {
        margin-bottom: 20px;
    }

    .just_text {
        font-size: 30px;
    }

    .m1 {
        margin-left: 100px;
    }

    .m2 {
        margin-left: 200px;
    }

    .m3 {
        margin-left: 300px;
    }

    .margin_up {
        margin-top: 40px;
    }

    .block_info {
        padding-top: 30px;
        margin-left: 50px;
        margin-top: 10px;
        margin-right: 50px;
    }

    .flex_container {
        display: flex;
        flex-direction: row;
    }

    .left_part {
        width: 60%;
        padding-bottom: 20px;
    }

    .right_part {
        width: 40%;
        text-align: center;
    }

    .weather_image {
        height: 200px;
        width: 200px;
    }

    @media (max-width: 720px) {
        .title {
            font-size: 20px;
        }

        .just_text {
            font-size: 15px;
        }

        .m1 {
            margin-left: 40px;
        }

        .m2 {
            margin-left: 80px;
        }

        .m3 {
            margin-left: 120px;
        }

        .flex_container {
            flex-direction: column-reverse;
        }

        .left_part {
            width: 100%;
        }

        .right_part {
            width: 100%;

        }
    }

    @media (max-width: 540px) {
        .block_info {
            margin-left: 20px;
            margin-right: 20px;
        }
    }
    
</style>