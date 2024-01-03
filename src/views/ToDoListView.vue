<script>
export default {
    data() {
        return {
            addText: '',
            toDoArr: [
                {
                    id: 1,
                    todo: '吃午餐',
                    checkList: false,
                    lastTime: '',
                    recordTime: '',
                },
            ],
            deadline: '',
            record: '',
        }
    },
    methods: {
        addList() {
            if (!this.addText) return;
            const listId = this.toDoArr.length ? Math.max(...this.toDoArr.map(item => item.id)) + 1 : 1;
            // const listId = this.toDoArr.length += 1;
            this.toDoArr.push({
                id: listId,
                todo: this.addText,
                checkList: false,
                lastTime: this.deadline,
                recordTime: this.record,
            })
            this.addText = '';
            sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
            console.log(typeof (this.deadline));
        },
        removeList(id) {
            this.toDoArr = this.toDoArr.filter((items) => items !== id);
            sessionStorage.removeItem('todoList', JSON.stringify(this.toDoArr));
            sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
        }
    },
    mounted() {
        if (sessionStorage.getItem('todoList')) {
            this.toDoArr = JSON.parse(sessionStorage.getItem('todoList'));
        }
        // else {
        //     sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
        // }

    },
}
</script>
<template>
    <header></header>
    <main class="border-[gray] border-[1px] p-4">
        <h1>Todo List</h1>
        <div class="bg-[#8DD7CF] border-[#1AAE9F] border-[1px] p-2">
            <input v-model="addText" type="text" class="border-[gray] border-[1px] px-2 py-1 mr-2"
                placeholder="Add New Todo Here...">
            <span>deadline:<input type="date" v-model="deadline"></span>
            <span>recording:<input type="date" v-model="record"></span>
            <button type="button" @click="addList()"
                class="text-[#44BDB1] bg-[white] border-[#63C8BD] border-[1px] rounded-md px-3 py-1 ml-2">
                <font-awesome-icon :icon="['fas', 'plus']" />
            </button>
        </div>
        <hr class="text-[#DFE6ED] my-2">
        <div class="h-[250px] border-[gray] border-[1px] p-2 overflow-y-scroll">
            <div v-for="item in toDoArr" :key="item.id"
                class="bg-[#E9A2AD] border-[#D3455B] border-[1px] px-1 py-2 my-1 flex justify-between items-center">
                <input v-model="item.checkList" type="checkbox" class="mr-[10px]">
                <!-- <input type="text" class="border-[gray] border-[1px] p-1 mr-[10px]" placeholder=".todo__title"> -->
                <div class="w-[100px] flex flex-wrap justify-center items-center">
                    <span :class="{ 'line-through': item.checkList }">
                        {{ item.todo }}
                    </span>
                </div>
                <span>最後時間:{{ item.lastTime }}</span>
                <span>紀錄時間:{{ item.recordTime }}</span>
                <button type="button" class="text-[#D65065] bg-[white] border-[#E18190] border-[1px] rounded-md px-2 py-1"
                    @click="removeList(item)">
                    <font-awesome-icon :icon="['fas', 'trash']" />
                </button>
            </div>
            <!-- <div class="bg-[#E9A2AD] border-[#D3455B] border-[1px] px-1 py-3">
                <input type="checkbox" class="mr-[10px]">
                <input type="text" class="border-[gray] border-[1px] p-1 mr-[10px]" placeholder=".todo__title">
                <button type="button"
                    class="add text-[#D65065] bg-[white] border-[#E18190] border-[1px] rounded-md px-2 py-1">
                    <font-awesome-icon :icon="['fas', 'trash']" />
                </button>
            </div> -->
        </div>
    </main>
    <footer></footer>
</template>
<style lang="scss" scoped></style>