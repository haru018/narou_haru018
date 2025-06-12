<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  name: string
}

const Tasks = ref<Task[]>([
  { name: '課題01'},
  { name: 'レポート'}
])
const Completes = ref<Task[]>([
  { name: '課題02'}
])

const newTaskName = ref('')
const compTaskNum = ref(1)

const addTask = () => {
    if(newTaskName.value=="") return
  Tasks.value.push({ name: newTaskName.value})
  newTaskName.value=""
}

const compTask = () => {
    const complete = Tasks.value.splice(Number(compTaskNum)-1,1)
    Completes.value.push({name: complete[0].name})
    compTaskNum.value=1
}
</script>

<template>
  <div>
    <div>TaskList</div>
    <div>未完タスク</div>
    <ol>
      <li v-for="task in Tasks" :key="task.name">
        <div>名前：{{ task.name }}</div>
      </li>
    </ol>
    <div>
        <label>
            名前
            <input v-model="newTaskName" type="text" />
        </label>
        <button @click="addTask">add</button>
    </div>
    <div>
        <label>
            番号
            <input v-model="compTaskNum" type="text" />
        </label>
        <button @click="compTask">complete</button>
    </div>
    <br>
    <div>完了タスク</div>
    <ol>
      <li v-for="task in Completes" :key="task.name">
        <div>名前：{{ task.name }}</div>
      </li>
    </ol>
    <div>
    </div>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>