<template>
<div class ="container">
  <h1>TodoList</h1>
 <TodoForm @todoAdd="todoAddapp"  />
<ul class="list-group " 
v-for="(i,index) in todolist" 
v-bind:key="i.id">
<li class="list-group-item d-flex align-items-center mt-2">
  <div class="form-check flex-grow-1">
      <input class="CheckInput"
         v-model="i.isdone"
         type="checkbox">
          <label class="checkLabel"
          :class="{todoStyle:i.isdone}"
          >{{i.sbj}} </label>
  </div>

  <div>
    <button class= "btn btn-danger btn-sm"
    @click="deleteitem(index)">삭제</button>
  </div>


</li>

</ul>
  <div v-if="!todolist.length">
    <b>오늘은 갓백수의 삶을 꿈꾸시나용..?</b>
  </div>


</div>
</template>

<script>

import {ref} from 'vue'

import TodoForm from './components/TodoForm.vue';
export default {
components:{
  TodoForm
},

setup()
{
  //let todo= ref("");
  let todolist = ref([  ]);

  let todoStyle={
    textDecoration:'line-through',
    color:'gray'
  }


  var deleteitem=(index)=>{
  // console.log(index)
  todolist.value.splice(index,1)
  }

  var  todoAddapp = (todo)=>{
 todolist.value.push(todo)
  }
  
  return {
   todoAddapp,todolist,todoStyle,deleteitem,
  }; 
}
}
</script>



<style>
.todoStyle{
  color:red;
  text-decoration: line-through;
}
</style>