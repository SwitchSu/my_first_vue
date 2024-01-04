<script>
import Swal from 'sweetalert2';
export default {
    data() {
        return {
            addText: '',
            toDoArr: [
                {
                    id: 1,
                    todo: '吃午餐',
                    checkList: false,
                    editIng: false,
                    lastTime: '2024-02-30',
                    recordTime: '2024-01-03',
                    newTodo: '',
                },
            ],
            deadline: new Date().toISOString().split('T')[0],
            done: '',
            loading: '',
        }
    },
    methods: {
        addList() {
            let date = new Date().toISOString().split('T');
            Swal.fire({
                title: "確定要新增嗎?",
                icon: "question",
                showCancelButton: true,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "是",
                cancelButtonText: "否",
            }).then((result) => {
                if (result.isConfirmed) {
                    if (!this.addText || !this.deadline) return Swal.fire({
                        title: "請不要空白!!",
                        icon: "error"
                    });
                    const listId = this.toDoArr.length ? Math.max(...this.toDoArr.map(item => item.id)) + 1 : 1;
                    // const listId = this.toDoArr.length += 1;
                    this.toDoArr.push({
                        id: listId,
                        todo: this.addText,
                        checkList: false,
                        editIng: false,
                        lastTime: this.deadline,
                        recordTime: date[0],
                        newTodo: '',
                    })
                    this.addText = '';
                    this.deadline = new Date().toISOString().split('T')[0];
                    sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
                    Swal.fire({
                        title: "儲存成功",
                        icon: "success"
                    });
                }
            });
        },
        removeList(id) {
            this.toDoArr = this.toDoArr.filter((items) => items !== id);
            sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
        },
        saveList() {
            sessionStorage.setItem('todoList', JSON.stringify(this.toDoArr));
        },
        startEdit(item) {
            item.editIng = !item.editIng;
            item.newTodo = item.todo;
        },
        topEdit(item) {
            item.editIng = !item.editIng;
            item.todo = item.newTodo;
            item.newTodo = '';
            this.saveList();
        },
        doneList() {
            this.done = this.toDoArr.filter(item => item.checkList).length;
            return this.done;
        },
        load() {
            this.loading = (this.done / this.toDoArr.length) * 100 + '%';
            return this.loading;
        },
    },
    mounted() {
        if (sessionStorage.getItem('todoList')) {
            this.toDoArr = JSON.parse(sessionStorage.getItem('todoList'));
        }
    },
}
</script>
<template>
    <header>
    </header>
    <main class="border-[gray] border-[1px] p-4">
        <h1>Todo List</h1>
        <div class="bg-[#8DD7CF] border-[#1AAE9F] border-[1px] p-2 flex justify-evenly items-center">
            <input v-model="addText" type="text" class="border-[gray] border-[1px] px-2 py-1 mr-2"
                placeholder="Add New Todo Here...">
            <span>最後期限:<input type="date" v-model="deadline"></span>
            <button type="button" @click="addList()"
                class="text-[#44BDB1] bg-[white] border-[#63C8BD] border-[1px] rounded-md px-3 py-1 ml-2">
                <font-awesome-icon :icon="['fas', 'plus']" />
            </button>
        </div>
        <hr class="text-[#DFE6ED] my-2">
        <!-- <div class="border-[gray] border-[1px] p-2">
            <div class="px-1 py-2 flex gap-[20px] items-center">
                <div>Finished</div>
                <div class="mr-[80px]">To-do</div>
                <div class="mr-[80px]">Deadline</div>
                <div>Record</div>
                <div>Delete</div>
            </div>
        </div> -->
        <div class="h-[250px] border-[gray] border-[1px] p-2 overflow-y-scroll">
            <div v-for="item in toDoArr" :key="item.id"
                class="bg-[#E9A2AD] border-[#D3455B] border-[1px] px-1 py-2 my-1 flex gap-[20px] items-center">
                <input v-model="item.checkList" type="checkbox" class="mr-[10px]" @change="saveList()">
                <div class="w-[100px] flex break-all justify-center items-center">
                    <span v-if="!item.editIng" :class="{ 'line-through': item.checkList }" @click="startEdit(item)">
                        {{ item.todo }}
                    </span>
                    <input class="w-[100px]" v-else v-model="item.newTodo" type="text" @keyup.enter="$event.target.blur()"
                        @blur="topEdit(item)">
                </div>
                <span>最後期限:{{ item.lastTime }}</span>
                <span>紀錄時間:{{ item.recordTime }}</span>
                <div class="w-[40px] h-[30px]">
                    <button v-show="!item.checkList" type="button"
                        class="text-[#D65065] bg-[white] border-[#E18190] border-[1px] rounded-md px-2 py-1"
                        @click="removeList(item)">
                        <font-awesome-icon :icon="['fas', 'trash']" />
                    </button>
                </div>

            </div>
        </div>
        <div class="flex items-center mt-3">
            <div class="w-[90px]">
                進度條:{{ doneList() }}/{{ toDoArr.length }}
            </div>
            <div class="w-full h-[15px] border-[#000000] border-[1px] rounded-lg">
                <div class="trans h-full bg-[#a2fdff] rounded-lg" :style="{ width: load() }"></div>
            </div>
        </div>

    </main>
    <footer></footer>
</template>
<style lang="scss" scoped>
.trans {
    transition: 0.6s;
}
</style>