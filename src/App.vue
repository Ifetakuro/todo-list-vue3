<script setup>
import { ref } from "vue";

let id = 0;
const todoInput = ref("");
const todos = ref([]);

function removeTodo(todo) {
  todos.value.splice(todos.value.indexOf(todo), 1);
}

function addTodo() {
  todos.value.push({ id: id++, text: todoInput.value, done: false });
  todoInput.value = "";
}

function doneToggle(todo) {
  todo.done = !todo.done;
}
</script>

<template>
  <div class="container" id="app">
    <h1>My Todo List</h1>
    <div class="input-sec">
      <input type="text" name="text" id="todo-input" v-model="todoInput" />
      <button
        @click="addTodo"
        :disabled="!todoInput"
        :class="{ disabled: !todoInput }"
      >
        <i class="bx bx-plus"></i>
      </button>
    </div>
    <div class="todo-lists">
      <ul>
        <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ done: todo.done }"
          @click="doneToggle(todo)"
        >
          {{ todo.text }}
          <span @click="removeTodo(todo)"><i class="bx bxs-trash"></i></span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
@import "./assets/style.css";
@import "https://unpkg.com/boxicons@2.1.2/css/boxicons.min.css";
</style>
