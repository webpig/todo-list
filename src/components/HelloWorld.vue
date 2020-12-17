<template>
    <div class="container">
        <div class="header">
            <input placeholder="" class="input" v-model="taskTitle"/>
            <button class="add-btn" @click="addTask">+</button>
        </div>
        <div class="task-list" v-if="taskList.length > 0">
            <div class="title">任务列表：</div>
            <div class="task-item" v-for="(item, index) in taskList" :key="item.id">
                <p>{{item.title}}</p>
                <button class="delete-btn" @click="deleteTask(index)">删除</button>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { ref } from 'vue'

const createdId = () => {
    let id = 0
    return () => ++id
}

interface Task {
    id: number,
    title: string
}

export default {
    setup() {
        const taskList = ref<Array<Task>>([])
        const taskTitle = ref('')
        const getId = createdId()

        const addTask = () => {
            const val = taskTitle.value.trim()

            if (!val) {
                alert('请输入')
                return
            }

            taskList.value.push({
                id: getId(),
                title: val
            })
            taskTitle.value = ''
        }

        const deleteTask = (index: number) => {
            taskList.value.splice(index, 1)
        }

        return {
            taskList,
            taskTitle,
            addTask,
            deleteTask
        }
    },
}
</script>

<style>
.container {
    padding: 0 10px;
}
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.input {
    flex: 1;
    font-size: 14px;
    height: 30px;
    padding-left: 12px;
}
.add-btn {
    width: 30px;
    height: 30px;
    margin-left: 10px;
}
.title {
    margin-top: 30px;
    font-weight: 600;
}
.task-item {
    display: flex;
    align-items: center;
    font-size: 14px;
}
.delete-btn {
    margin-left: auto;
}
</style>
