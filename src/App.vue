<template>
  <div class="container">
    <h1>TodoList</h1>

    <input
      class="form-control"
      type="text"
      v-model="search"
      placeholder="검색"
    />

    <hr />

    <TodoForm @todoAdd="todoAddapp" />
    <TodoList
      :todolist="searchTodolist"
      @toggle-todo="toggleTodo"
      @delete-item="deleteitem"
    />

    <div v-if="!todolist.length">
      <b>오늘은 갓백수의 삶을 꿈꾸시나용..?</b>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import axios from "axios";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";

let todolist = ref([]);
let getTodolist = async () => {
  try {
    let res = await axios.get("http://localhost:3000/todolist");
    todolist.value = res.data;
    //console.log(res.data[0].sbj);
  } catch (err) {
    console.log(err);
  }
};
getTodolist();

let search = ref("");
let searchTodolist = computed(() => {
  if (search.value) {
    return todolist.value.filter((tmp) => {
      return tmp.sbj.includes(search.value);
    });
  } else {
    return todolist.value;
  }
});

var deleteitem = async (index) => {
  let id = todolist.value[index].id;
  try {
    let res = await axios.delete("http://localhost:3000/todolist/" + id);
    console.log(res);
    // console.log(index)
  } catch (err) {
    throw err;
  }
  todolist.value.splice(index, 1);
};

//비동기로 만든다
var todoAddapp = async (todo) => {
  try {
    //db 저장
    let res = await axios.post("http://localhost:3000/todolist", {
      sbj: todo.sbj,
      isdone: todo.isdone,
    });

    todolist.value.push(res.data);
  } catch (err) {
    throw err;
  }
};

var toggleTodo = async (index) => {
  let id = todolist.value[index].id;
  try {
    await axios.patch("http://localhost:3000/todolist/" + id, {
      isdone: !todolist.value[index].isdone,

      // console.log(index)
    });
  } catch (err) {
    throw err;
  }
  todolist.value[index].isdone = !todolist.value[index].isdone;
};

// var toggleTodo = (index) => {
//   todolist.value[index].isdone = !todolist.value[index].isdone;
// };

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
