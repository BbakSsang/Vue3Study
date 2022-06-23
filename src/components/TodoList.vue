<template>
  <ul class="list-group" v-for="(i, index) in todolist" v-bind:key="i.id">
    <li class="list-group-item d-flex align-items-center mt-2">
      <div class="form-check flex-grow-1">
        <input
          class="CheckInput"
          :value="todolist.isdone"
          @change="toggleTodo(index)"
          type="checkbox"
        />
        <label class="checkLabel" :class="{ todoStyle: i.isdone }"
          >{{ i.sbj }}
        </label>
      </div>

      <div>
        <button class="btn btn-danger btn-sm" @click="deleteitem(index)">
          삭제
        </button>
      </div>
    </li>
  </ul>
</template>

<script setup>
// import { defineProps, defineEmits } from "vue";

const props = defineProps({
  todolist: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["toggle-todo", "delete-item"]);
const toggleTodo = (index) => {
  emit("toggle-todo", index);
};
const deleteitem = (index) => {
  emit("delete-item", index);
};
//props:['todolist']//받아오는 이름 + 위에서 사용하는 이름 props는 return역할을 함께함
</script>

<style></style>
