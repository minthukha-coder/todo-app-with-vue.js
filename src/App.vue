<template>
  <div class="container my-5">
    <h4>To Do List</h4>
    <div class="row">
      <div class="col-md-6">
        <div class="w-50 input-group">
          <input type="text" class="form-control" v-model="inputTodo">
          <button class="btn btn-primary" @click="addToDo">{{ editTodo ? update : add  }}</button>
        </div>

        <ul class="my-3" style = "list-style-type: none;">
          <template v-for="todo in todos" :key="todo.id">
            <li class="my-2" @dblclick="doneList(todo)" >
              <i class="bi bi-file-music-fill"></i>
                {{ todo.name }}
              <button class="btn btn-warning btn-sm me-2" @click = "editTodoFun(todo)"><i class="bi bi-pencil-square"></i></button>
              <button class="btn btn-success btn-sm me-2" @click="doneList(todo)"><i class="bi bi-check-circle-fill"></i></button>
              <button class="btn btn-danger btn-sm me-2 my-1" @click = "deleteTodo(todo)"><i class="bi bi-trash-fill"></i></button>

            </li>
          </template>
        </ul>
      </div>

      <div class="col-md-6">
        <h4>Done List</h4>
        <ul style = "list-style-type: none;">
          <template v-for="doneTodo in doneTodos" :key="doneTodo.id">
            <li>
              <i class="bi bi-dash-circle"></i> {{ doneTodo.name }}
            <button class="btn btn-danger btn-sm me-2 my-1" @click = "unDone(doneTodo)">Undone</button>
            <button class="btn btn-danger btn-sm me-2 my-1" @click = "deleteDoneTodo(doneTodo)"><i class="bi bi-trash-fill"></i></button>

          </li>
          </template>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const inputTodo = ref('');
const todos = ref([]);
const doneTodos = ref([]);
const editTodo = ref(null);

const add = ref('Add')
const update = ref('Update');

const addToDo = () => {

  if (editTodo.value){
    editTodo.value.name = inputTodo.value
    editTodo.value = null
    }else{
  const newTodo = {
    id: Math.floor(Math.random() * 10) + 1,
    name: inputTodo.value,
    done: false,
  };
  todos.value.push(newTodo);
}

inputTodo.value = '';



};


const doneList = (todo) => {
  todo.done = true
  doneTodos.value.push(todo)
  todos.value = todos.value.filter((t) => t !== todo) // !== ဆိုမှ todoထဲမှာ data တွေပျောက်ပီး do list မှာ သွားပေါ်
}

const unDone = (doneTodo) => {
  doneTodo.done = false
  todos.value.push(doneTodo)
  doneTodos.value = doneTodos.value.filter((t) => t !== doneTodo)
}


const deleteTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo)

}

const deleteDoneTodo = (doneTodo) => {
  doneTodos.value = doneTodos.value.filter((t) => t !== doneTodo)
}

const editTodoFun = (todo) => {
  editTodo.value = todo
  inputTodo.value = todo.name
};

// const markAsDone = (todo) => {
//   todo.done = true;
//   doneTodos.value.push(todo);
//   todos.value = todos.value.filter((t) => t !== todo);
// };
</script>

<style scoped>
  /* Add your scoped styles here if needed */
</style>
