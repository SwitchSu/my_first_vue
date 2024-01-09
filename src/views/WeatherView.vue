<script>
import WeatherCard from '@/components/WeatherCard.vue';
export default {
    components: {
        WeatherCard,
    },
    data() {
        return {
            weather: [],
            list: [['基隆市', '臺北市', '新北市', '桃園市', '新竹市', '新竹縣', '宜蘭縣', '苗栗縣', '臺中市', '彰化縣', '南投縣', '雲林縣',
                '嘉義市', '嘉義縣', '臺南市', '高雄市', '屏東縣', '花蓮縣', '臺東縣', '金門縣', '連江縣', '澎湖縣'],
            ['基隆市', '臺北市', '新北市', '桃園市', '新竹市', '新竹縣', '宜蘭縣'],
            ['苗栗縣', '臺中市', '彰化縣', '南投縣', '雲林縣'],
            ['嘉義市', '嘉義縣', '臺南市', '台南市', '高雄市', '屏東縣'],
            ['花蓮縣', '臺東縣'], ['金門縣', '連江縣', '澎湖縣']],
        };
    },
    mounted() {
        fetch("https://opendata.cwa.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=CWA-026F36E2-988A-4EAC-93B8-4B2366778207")
            .then((res) => res.json())
            .then((result) => {
                this.weather = result.records.location;
            })
    },
    methods: {

    }
}
</script>
<template>
    <div class="w-[100vw]">
        <WeatherCard :weather-type="weather" />
        {{ weather }}
    </div>
</template>
<style scoped='scss'></style>