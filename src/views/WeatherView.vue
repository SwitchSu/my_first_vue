<script>
import weathercard from '@/components/WeatherCard.vue';
import weatherslot from '@/components/WeatherSlot.vue';
import { faThList } from '@fortawesome/free-solid-svg-icons';
import { list } from 'postcss';
export default {
    components: {
        weathercard,
        weatherslot,
    },
    data() {
        return {
            weather: [],
            areas: [
                {
                    id: 0,
                    area: '全部縣市',
                },
                {
                    id: 1,
                    area: '北部地區',
                },
                {
                    id: 2,
                    area: '中部地區',
                },
                {
                    id: 3,
                    area: '南部地區',
                },
                {
                    id: 4,
                    area: '東部地區',
                },
                {
                    id: 5,
                    area: '外島地區',
                }],
            list: [['基隆市', '臺北市', '新北市', '桃園市', '新竹市', '新竹縣', '宜蘭縣', '苗栗縣', '臺中市', '彰化縣', '南投縣', '雲林縣',
                '嘉義市', '嘉義縣', '臺南市', '高雄市', '屏東縣', '花蓮縣', '臺東縣', '金門縣', '連江縣', '澎湖縣'],
            ['基隆市', '臺北市', '新北市', '桃園市', '新竹市', '新竹縣', '宜蘭縣'],
            ['苗栗縣', '臺中市', '彰化縣', '南投縣', '雲林縣'],
            ['嘉義市', '嘉義縣', '臺南市', '台南市', '高雄市', '屏東縣'],
            ['花蓮縣', '臺東縣'], ['金門縣', '連江縣', '澎湖縣']],
            CityId: 0,
        };
    },
    mounted() {
        fetch("https://opendata.cwa.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=CWA-026F36E2-988A-4EAC-93B8-4B2366778207")
            .then((res) => res.json())
            .then((result) => {
                // console.log(result);
                this.weather = result.records.location;
                this.weather.sort((a, b) => {
                    return this.list[0].indexOf(a.locationName) - this.list[0].indexOf(b.locationName);
                });
            })
    },
    methods: {

    },
    computed: {
        CountryArea() {
            return this.weather.filter((item) => {
                if (this.CityId === 1) {
                    return this.list[1].includes(item.locationName);
                } else if (this.CityId === 2) {
                    return this.list[2].includes(item.locationName);
                } else if (this.CityId === 3) {
                    return this.list[3].includes(item.locationName);
                } else if (this.CityId === 4) {
                    return this.list[4].includes(item.locationName);
                } else if (this.CityId === 5) {
                    return this.list[5].includes(item.locationName);
                } else {
                    return true;
                }
            })
        },
    }
}
</script>
<template class="w-[100vw]">
    <div class="flex gap-[20px] justify-center mb-2">
        <weatherslot v-for="area in areas" :key="area.id" @click="this.CityId = area.id"
            :class="{ 'text-white bg-cyan-700': this.CityId == area.id }">{{ area.area }}</weatherslot>
    </div>

    <div class="flex flex-wrap justify-center gap-[20px]">
        <weathercard v-for="item in CountryArea" :key="item.id" :weather-type="item" />
        <!-- {{ weather }} -->
    </div>
</template>
<style scoped='scss'></style>