<script setup>
import { ref } from "vue";

const id = ref(1)
const todoList = ref([])
const userName = ref("")
const date = ref("")
const todo = ref("")
const isInputsEmpty = ref(false)

function addTodo() {
  if (!userName.value.trim() || !date.value.trim() || !todo.value.trim()) {
    isInputsEmpty.value = true
    return
  }
  isInputsEmpty.value = false
  todoList.value.push({
    id: id.value++,
    userName: userName.value,
    date: date.value,
    todo: todo.value,
  })
  userName.value = "";
  date.value = "";
  todo.value = "";
}

function deleteList() {
  todoList.value = []
  id.value = 1
}

function deleleTodo(todo) {
  todoList.value = todoList.value.filter((t) => t !== todo)
}
</script>

<template>
  <main>
    <div class="add_user">
      <div class="block_1">
        <div class="form">
          <input v-model="userName" id="name" type="text" placeholder="" @focus="isInputsEmpty = false" autocomplete="off"/>
          <label for="name">Введите имя</label>
        </div>
        <div class="form">
          <input v-model="date" id="date" type="text" placeholder="" @focus="isInputsEmpty = false" autocomplete="off"/>
          <label for="date">Время задачи</label>
        </div>
      </div>
      <div class="form">
        <input v-model="todo" id="todo" type="text" placeholder="" @focus="isInputsEmpty = false" autocomplete="off"/>
        <label for="todo">Задача</label>
      </div>
      <button @click="addTodo">Добавить задачу</button>
      <p v-if="isInputsEmpty" class="is_empty">Заполните все поля</p>
    </div>


    <div class="user_list">
      <div v-if="todoList.length > 0">
        <ul>
          <li v-for="(todo, index) in todoList" :key="todo.id">
            <p class="todo_info">{{ index + 1 }}. {{ todo.userName }} {{ todo.date }}</p>
          <p>
            <button @click="deleleTodo(todo)">X</button>
            <span class="todo">{{ todo.todo }}</span>
          </p>
          </li>
        </ul>
        <svg @click="deleteList" id="Layer_1" data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 110.61 122.88" height="30px" width="30px">
          <title>Delete all</title>
          <path d="M39.27,58.64a4.74,4.74,0,1,1,9.47,0V93.72a4.74,4.74,0,1,1-9.47,0V58.64Zm63.6-19.86L98,103a22.29,22.29,0,0,1-6.33,14.1,19.41,19.41,0,0,1-13.88,5.78h-45a19.4,19.4,0,0,1-13.86-5.78l0,0A22.31,22.31,0,0,1,12.59,103L7.74,38.78H0V25c0-3.32,1.63-4.58,4.84-4.58H27.58V10.79A10.82,10.82,0,0,1,38.37,0H72.24A10.82,10.82,0,0,1,83,10.79v9.62h23.35a6.19,6.19,0,0,1,1,.06A3.86,3.86,0,0,1,110.59,24c0,.2,0,.38,0,.57V38.78Zm-9.5.17H17.24L22,102.3a12.82,12.82,0,0,0,3.57,8.1l0,0a10,10,0,0,0,7.19,3h45a10.06,10.06,0,0,0,7.19-3,12.8,12.8,0,0,0,3.59-8.1L93.37,39ZM71,20.41V12.05H39.64v8.36ZM61.87,58.64a4.74,4.74,0,1,1,9.47,0V93.72a4.74,4.74,0,1,1-9.47,0V58.64Z"/>
        </svg>
      </div>
      <p v-else class="empty-list">Список пустой</p>
    </div>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

li {
  list-style: none;
}

.add_user {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  gap: 30px;
  border: 3px solid #c2c2c2;
  border-radius: 20px;
  padding: 20px;
  max-width: 400px;
}

.block_1 {
  display: flex;
  justify-content: space-around;
  gap: 50px;
}

.form {
  position: relative;
  height: 45px;
  transition: all 0.3s ease;
  margin: 3px;
}

.form input {
  width: 100%;
}

label {
  position: absolute;
  color: #8d8d8d;
  pointer-events: none;
  background-color: transparent;
  left: 15px;
  transform: translateY(12px);
  transition: all 0.3s ease;
}

input {
  padding: 10px 15px;
  font-size: 18px;
  border-radius: 8px;
  border: solid 1px #8d8d8d;
  box-sizing: border-box;
  transition: all 0.5s ease;
  height: 100%;
}

.block_1 input {
  max-width: 150px;
}

.block_1 input:focus ~ label,
.block_1 input:not(:placeholder-shown) ~ label {
  transform: translateY(-10px) translateX(-20px) scale(0.8);
  background-color: #fff;
  padding: 0px 5px;
  color: #3071eb;
  font-weight: bold;
  letter-spacing: 1px;
  border: none;
  border-radius: 3px;
}

.add_user > .form input:focus ~ label,
.add_user > .form input:not(:placeholder-shown) ~ label {
  transform: translateY(-10px) translateX(-15px) scale(0.8);
  background-color: #fff;
  padding: 0px 5px;
  color: #3071eb;
  font-weight: bold;
  letter-spacing: 1px;
  border: none;
  border-radius: 3px;
}

input:focus,
input:not(:placeholder-shown) {
  outline: none;
  border: 2px solid #3071eb;
}

.add_user button {
  padding: 7px 40px;
  font-size: 18px;
  border-radius: 8px;
  border: solid 1px #8d8d8d;
  background-image: linear-gradient(#3071eb, #2664d8);
  transition: all 0.3s ease;
  color: #ebebeb;
  font-weight: bold;
  height: 45px;
  font-family: inherit;
}

.add_user button:hover {
  box-shadow: 0 0 5px #3071eb;
}

.is_empty {
  color: #e60000;
  font-size: 20px;
  font-weight: bold;
  text-align: center;
}

.user_list {
  margin-top: 20px;
  padding: 20px;
  border: 3px solid #c2c2c2;
  border-radius: 20px;
  background-color: #f0f0f0;
}

.user_list > div {
  display: flex;
  gap: 10px;
  justify-content: space-between;
  align-items: start;
}

.user_list ul {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.todo_info {
  font-weight: bold;
}

.empty-list {
  text-align: center;
  color: #8d8d8d;
  font-style: italic;
}

.user_list svg {
  transition: all 0.1s ease;
}

.user_list svg:hover {
  cursor: pointer;
  transform: scale(1.05);
}

.user_list li button {
  background: none;
  border: 2px solid #c2c2c2;
  padding: 2px 3px;
  border-radius: 5px;
  margin-right: 10px;
}

.user_list li button:hover {
  cursor: pointer;
}
</style>
