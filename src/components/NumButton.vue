<script>
export default {
    components: {

    },
    props: {
        calcType: {
            type: Array,
        },
        numC: {
            type: String,
        }
    },
    emit: ['keyNum'],
    data() {
        return {
            type: this.calcType ?? [],
            result: 0,
            numberC: this.numC ?? '',
        }
    },
    methods: {
        keyin(num) {
            this.numberC += num;
            this.$emit('keyNum', this.numberC);
        }

    }
}
</script>
<template>
    <div class="btns">
        <button type="button" class="btn" v-for="item in type" :key="item.id" @click="keyin(item)">
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