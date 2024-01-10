<script>
import summer from '@/assets/img/sun-cloud.svg'
import cloud from '@/assets/img/cloud.svg'
import rain from '@/assets/img/rain.svg'
export default {
    props: {
        weatherType: {
            type: Object,
        },
    },
    data(){
        return{
            // type:this.weatherType ?? {},
            summer,
            cloud,
            rain,
        }
    },
    methods:{
        RainPercentage(item){
            if (item <= 30){
                return summer;
            } else if(item <= 70){
                return cloud;
            }else {
                return rain;
            }
        },
    }
}
</script>
<template>
    <div class="card">
        <div class="name">縣市:{{weatherType.locationName}}</div>
        <div class="temp">
            溫度:{{weatherType.weatherElement[2].time[2].parameter.parameterName}}°C ~ {{ weatherType.weatherElement[4].time[0].parameter.parameterName }}°C
        </div>
        <div class="rain">降雨機率:{{ weatherType.weatherElement[1].time[2].parameter.parameterName }}%</div>
        <div class="sky">{{ weatherType.weatherElement[0].time[0].parameter.parameterName }}</div>
        <div class="feel">{{ weatherType.weatherElement[3].time[0].parameter.parameterName }}
        </div>
        <img :src="RainPercentage(weatherType.weatherElement[1].time[2].parameter.parameterName)" alt="">
    </div>
</template>
<style lang="scss" scoped>
// .btns {
//     @apply flex gap-[30px];
//     .btn {
//         @apply border-[black] border-[1px] px-[15px] py-[10px];
//     }
// }
// .card {
//     width: 200px;
//     height: 300px;
//     padding: 20px;
//     border: 1px solid rgb(18, 129, 92);
//     gap: 10px;
//     border-radius: 15px;
//     display: flex;
//     flex-direction: column;
//     align-items: center;
// }
.card {
    @apply w-[200px] h-[300px] p-[20px] border-[1px] border-[green] flex flex-col items-center;
}
</style>