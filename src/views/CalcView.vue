<script>
import MyButton from '@/components/MyButton.vue'
import CalcButton from '@/components/CalcButton.vue'
import NumButton from '@/components/NumButton.vue';
export default {
    components: {
        MyButton,
        CalcButton,
        NumButton,
    },
    data() {
        return {
            numA: 0,
            numB: 0,
            result: 0,
            calcType: ['+', '-', 'x', '÷'],
            calcNum: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
            numC: 0,
            ans:0,
        }
    },
    methods: {
        calcResult(type) {
            if (this.numA.toString().trim() === '' || this.numB.toString().trim() === '') return;
            switch (type) {
                case '+':
                    this.result = this.numA + this.numB
                    break;
                case '-':
                    this.result = this.numA - this.numB
                    break;
                case 'x':
                    this.result = this.numA * this.numB
                    break;
                case '÷':
                    this.result = this.numA / this.numB
                    break;
                default:
                    break;
            }
        },
        final(end) {
            this.result = end;
        },
        keyin(end) {
            this.ans = end;
            console.log(this.ans);
        }
    }
    
}
</script>
<template>
    <main>
        <div class="calc">計算機</div>
        <div>
            <label>
                NumA:<input v-model="numA" type="number" class="border-[black] border-[1px] px-2">
            </label>
        </div>
        <div>
            <label>
                NumB:<input v-model="numB" type="number" class="border-[black] border-[1px] px-2">
            </label>
        </div>
        <!-- <div class="">
            <CalcButton :calc-type="calcNum" />
        </div> -->
        <CalcButton :calc-type="calcType" :num-a="numA" :num-b="numB" @final-math="final" />
        <div class="btns">
            <MyButton @click="calcResult('+')">+</MyButton>
            <MyButton @click="calcResult('-')">-</MyButton>
            <MyButton @click="calcResult('x')">x</MyButton>
            <MyButton @click="calcResult('÷')">÷</MyButton>
            <!-- <button type="button" class="btn">+</button>
            <button type="button" class="btn">-</button>
            <button type="button" class="btn">x</button>
            <button type="button" class="btn">÷</button> -->
        </div>
        <div class="result">結果:{{ result }}</div>
        <div class="w-[250px] h-[350px] border-[black] border-[1px]">
            <div class="flex justify-center">
                <input v-model="numC" class="border-[black] border-[1px] my-2 m-auto text-end" type="number">
            </div>
            <div>
                <NumButton :calc-type="calcNum" @key-num = "keyin" />
            </div>
            {{ ans }}
        </div>
    </main>
</template>
<style lang="scss" scoped>
.btns {
    @apply flex gap-[30px];

    // display: flex;
    // gap: 10px;
    // margin-top: 10px;
    .btn {
        // @apply border-[black] border-[1px] px-[15px] py-[10px];
        // border: 1px solid black;
        // padding: 10px 15px;
    }
}
</style>
