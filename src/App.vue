<template>
  <div class="container">
    <h1>TodoList</h1>
    <TodoForm @todoAdd="todoAddapp" />
    <TodoList
      :todolist="todolist"
      @toggle-todo="toggleTodo"
      @delete-item="deleteitem"
    />

    <div v-if="!todolist.length">
      <b>오늘은 갓백수의 삶을 꿈꾸시나용..?</b>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";

let todolist = ref([]);

var deleteitem = (index) => {
  // console.log(index)
  todolist.value.splice(index, 1);
};

var todoAddapp = (todo) => {
  todolist.value.push(todo);
};

var toggleTodo = (index) => {
  todolist.value[index].isdone = !todolist.value[index].isdone;
};

// let todoStyle = {
//   textDecoration: "line-through",
//   color: "gray",
// };
</script>

<style>
.todoStyle {
  color: red;
  text-decoration: line-through;
}
</style>
