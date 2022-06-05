<script setup>
import { reactive } from "vue";
import Title from "./components/Title.vue";
import Layout from "./components/Layout.vue";
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";
import Modal from "./components/Modal.vue";

const state = reactive({
  todoItems: [
    {
      title: "Learn HTML",
      complete: true,
    },
    {
      title: "Learn CSS",
      complete: true,
    },
    {
      title: "Learn JS",
      complete: false,
    },
  ],
  newTodoItem: "",
  modal: false,
  indexItem: -1,
});

function addNewTodo(item) {
  state.todoItems.push({
    title: item,
    complete: false,
  });
  state.newTodoItem = "";
}
function delModalWindow(index) {
  state.modal = true;
  // state.todoItems.splice(index, 1);
  state.indexItem = index;
  console.log(index)
  // let index = state.todoItems.findIndex('')
  // console.log(index)
}
function delTodoItem() {
  console.log(state.indexItem)
  state.todoItems.splice(state.indexItem, 1);
  closeModal();
}
function closeModal(){
  state.modal = false;
}
</script>

<template>
  <Layout>
    <div class="bg-base-200 flex flex-col shadow-md p-4 rounded w-96">
      <!-- TITLE -->
      <Title title="TodoApp" />
      <!-- TODO FORM -->
      <TodoForm :newTodo="state.newTodoItem" @add-todo=" (item) => addNewTodo(item)"/>
      <!-- TODO LIST -->
      <ul class="flex flex-col gap-4">
       <TodoList  v-for="(todoItem, index) in state.todoItems" :itemComplete='todoItem.complete' :itemTitle="todoItem.title" @modal-window="delModalWindow(index)"/>
      </ul>
      <!-- MODAL WINDOW -->
      <Modal :switchModal="state.modal" @del-todo-item="delTodoItem" @close-modal="closeModal"/>
    </div>
  </Layout>
</template>
