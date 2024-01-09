<script>
export default {
    props: {
        weatherType: {
            type: Object,
        },
    },
    // data(){
    //     return{
    //         type:this.weatherType ?? {},
    //     }
    // }
}
</script>
<template>
    <div class="card" v-for="item in weatherType" :key="item.id">
        <div class="name">縣市:{{item.locationName}}</div>
        <div class="temp">
            溫度:{{item.weatherElement[2].time[2].parameter.parameterName}}°C ~ {{ item.weatherElement[4].time[0].parameter.parameterName }}°C
        </div>
        <div class="rain">降雨機率:{{ item.weatherElement[1].time[2].parameter.parameterName }}%</div>
        <div class="sky">{{ item.weatherElement[0].time[0].parameter.parameterName }}</div>
        <div class="feel">{{ item.weatherElement[3].time[0].parameter.parameterName }}
        </div>
        <!-- <img src="${s}" alt=""> -->
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