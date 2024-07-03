<template>
  <v-app class="test">
    <v-container class="container">
      <v-card class="test1 mx-auto my-12 panel-borderless bg-teal-darken-4">
        <v-card-title class="title">오늘의 할 일 🥳</v-card-title>
        <v-card-text>
          <InputTodo @add-todo="addTodo" />
          <div class="summary-with-button">
            <TodoSummary :todoList="todoList" />
          </div>
          <TodoList class="tdlist" :todoList="todoList" @delete-todo="deleteTodo" @toggle-completed="toggleCompleted" />
        </v-card-text>
      </v-card>
    </v-container>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'
import InputTodo from './components/InputTodo.vue'
import TodoList from './components/TodoList.vue'
import TodoSummary from './components/TodoSummary.vue'

const todoList = ref([
  { id: 1, todo: "투두리스트 작성", completed: true, date: new Date() },
  { id: 2, todo: "점심 먹기", completed: false, date: new Date() },
])

const addTodo = (todo) => {
  if (todo.length >= 2) {
    todoList.value.push({
      id: new Date().getTime(),
      todo: todo,
      completed: false,
      date: new Date() // 현재 날짜 설정
    })
  }
}

const deleteTodo = (id) => {
  const index = todoList.value.findIndex((item) => id === item.id)
  todoList.value.splice(index, 1)
}

const toggleCompleted = (id) => {
  const index = todoList.value.findIndex((item) => id === item.id)
  todoList.value[index].completed = !todoList.value[index].completed
}
</script>

<style>
.v-list-item__content {
  display: flex;
  align-items: center;
  width: 100%;
}

.summary-with-button {
  display: flex;
  align-items: center;
}

.ml-4 {
  margin-left: 16px;
}

</style>