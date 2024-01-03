<script>
export default {
    data() {

    },
    methods: {

    },
    mounted() {

    },
}
</script>
<template>
    <header></header>
    <main class="border-[gray] border-[1px] p-4">
        <h1>Todo List</h1>
        <div class="bg-[#8DD7CF] border-[#1AAE9F] border-[1px] p-2">
            <input type="text" class="text-[#C3CFD9] border-[gray] border-[1px] px-2 py-1 mr-[20px]" value="Add New Todo Here...">
            <button type="button" class="add text-[#44BDB1] bg-[white] border-[#63C8BD] border-[1px] rounded-md px-4 py-1">Add</button>
        </div>
        <hr class="text-[#DFE6ED] my-2">
        <div class=" border-[gray] border-[1px] p-2">
            <div class="bg-[#E9A2AD] border-[#D3455B] border-[1px] px-1 py-3">
                <input type="checkbox" class="mr-[10px]">
                <input type="text" class="text-[#C3CFD9] border-[gray] border-[1px] p-1 mr-[10px]"
                    value=".todo__title">
                <button type="button" class="add text-[#D65065] bg-[white] border-[#E18190] border-[1px] rounded-md px-2 py-1">Delete</button>
            </div>
            <div class="bg-[#E9A2AD] border-[#D3455B] border-[1px] px-1 py-3">
                <input type="checkbox" class="mr-[10px]">
                <input type="text" class="text-[#C3CFD9] border-[gray] border-[1px] p-1 mr-[10px]"
                    value=".todo__title">
                <button type="button" class="add text-[#D65065] bg-[white] border-[#E18190] border-[1px] rounded-md px-2 py-1">Delete</button>
            </div>
        </div>
    </main>
    <footer></footer>
</template>
<style lang="scss" scoped>
</style>