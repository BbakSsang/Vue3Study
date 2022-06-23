<template>
  <form @submit.prevent="Submit" class="d-flex">
    <div class="flex-grow-1">
      <input
        class="form-control"
        type="text"
        v-model="todo"
        placeholder="할일"
      />
    </div>
    <div>
      <button class="btn btn-primary">추가</button>
    </div>
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  setup(props, context) {
    //props는 아직 잘 모르겠고 context가 부모로 보내는 부분
    let todo = ref("");

    var Submit = () => {
      context.emit("todoAdd", {
        id: Date.now(),
        sbj: todo.value,
        isdone: false,
      }); //context.emit할때 보내려는 이름, {값들}
      todo.value = "";
    };
    return {
      todo, //여기있는 return은 app.vue와 마찬가지로 자식컴포넌트 내에서 사용되는 변수 및 함수명
      Submit,
    };
  },
};
</script>

<style></style>
