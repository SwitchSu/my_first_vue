<script>
export default {

}
</script>
<template>
    <div class="btns">
        <button type="button" class="btn">
            <slot/>
        </button>
    </div>
</template>
<style lang="scss" scoped>
.btns {
    @apply flex gap-[30px];
    .btn {
        @apply border-[black] border-[1px] px-[15px] py-[10px];
    }
}
</style>