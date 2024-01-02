<script>
export default {
    props:{
        numA:{
            type: Number,
            // default:'',
        },
        numB:{
            type: Number,
            // default:'',
        },
        calcType:{
            type: Array,
            // default:'',
        },
    },
    emit:['finalMath'],
    data(){
        return{
            type: this.calcType ?? [],
            numberA:this.numA ?? 0,
            numberB:this.numB ?? 0,
            result:0,
        }
    },
    methods:{
        calcMath(type){
            if(this.numA.toString().trim() === '' || this.numB.toString().trim() === '') return;
            switch(type){
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
            this.$emit('finalMath',this.result);
        }
    }
}
</script>
<template>
    <div class="btns">
        <button type="button" class="btn" v-for="item in type" :key="item.id" @click="calcMath(item)">
            {{ item }}
        </button>
    </div>
</template>
<style lang="scss" scoped>
.btns {
    @apply flex flex-wrap justify-center gap-[30px];
    .btn {
        @apply border-[black] border-[1px] px-[15px] py-[10px];
    }
}
</style>