<script setup>
import { ref } from "vue";
const users = [];
function addUser(e) {
  users.push(e.value);
}
</script>

<template>
  <main>
    <div class="add_user">
      <div class="block_1">
        <div class="form">
          <input v-model="userName" id="name" type="text" placeholder="" />
          <label for="name">Введите имя</label>
        </div>
        <div class="form">
          <input v-model="date" id="date" type="text" placeholder="" />
          <label for="date">Время задачи</label>
        </div>
      </div>
      <div class="form">
          <input v-model="todo" id="todo" type="text" placeholder="" />
          <label for="todo">Задача</label>
      </div>
      <button @click="addUser">+</button>
      <div>Список пользователей</div>
    </div>
    <div class="user_list"></div>
  </main>
</template>

<style scoped>
.add_user {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  gap: 30px;
  border: 3px solid #c2c2c2;
  border-radius: 20px;
  padding: 20px;
}

.block_1 {
  display: flex;
  justify-content: space-between;
  gap: 50px;
}

.form {
  position: relative;
  height: 45px;
  transition: all 0.3s ease;
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
  font-size: 1rem;
  border-radius: 8px;
  border: solid 1px #8d8d8d;
  box-sizing: border-box;
  transition: all 0.3s ease;
  height: 100%;
}

input:hover,
input:focus {
  box-shadow: 0 0 5px #3071eb;
}

input:focus ~ label,
input:not(:placeholder-shown) ~ label {
  transform: translateY(-12px) translateX(-20px) scale(0.8);
  background-color: #fff;
  padding: 0px 5px;
  color: #3071eb;
  font-weight: bold;
  letter-spacing: 1px;
  border: none;
  border-radius: 100px;
}
input:focus,
input:not(:placeholder-shown) {
  outline: none;
  border: 2px solid #3071eb;
}

button {
  padding: 7px 40px;
  font-size: 24px;
  border-radius: 8px;
  border: solid 1px #8d8d8d;
  background-image: linear-gradient(#3071eb, #2664d8);
  transition: all 0.3s ease;
  color: #ebebeb;
  font-weight: bold;
  height: 45px;
}

button:hover {
  box-shadow: 0 0 5px #3071eb;
}
</style>
