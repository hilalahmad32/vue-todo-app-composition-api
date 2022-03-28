<script>
import { ref } from "vue";
export default {
  name: "TodoApp",
};
</script>

<script setup>
const name = ref("Todo app in composition api");

const todoName = ref("");

const todos = ref([]);

const addTodo = () => {
  if (!todoName.value) {
    alert("Please fill the field");
  } else {
    const todo = {
      id: Date.now().toString(),
      todo: todoName.value,
    };
    todos.value.push(todo);
    todoName.value = "";
  }
};

const deleteTodo = (id) => {
  const newTodo = todos.value.filter((item) => item.id !== id);
  todos.value = newTodo;
};

const deleteAllTodo = () => {
  todos.value = [];
};
</script>

<template >
  <div class="container">
    <h2>{{ name }}</h2>
    <div class="form">
      <input
        type="text"
        class="form__control"
        v-model="todoName"
        placeholder="Enter Your Todo"
      />
      <button class="btn" @click="addTodo">Add</button>
    </div>

    <div class="todos">
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <span>{{ todo.todo }}</span>
          <button @click="() => deleteTodo(todo.id)">Delete</button>
        </li>
      </ul>
    </div>

    <button @click="deleteAllTodo" class="delete__all">Delete All</button>
  </div>
</template>

<style lang="css">
body {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
.container {
  width: 70%;
  margin: 0 auto;
  text-align: center;
}
.container h2 {
  font-size: 2rem;
  font-weight: bold;
}
.form {
  width: 100%;
}
.form__control {
  width: 100%;
  padding: 10px 0px;
  font-size: 18px;
  /* border-radius: 10px; */
  outline: none;
  border: none;
  border-bottom: 1px solid cyan;
}
.btn {
  outline: none;
  border: none;
  padding: 10px 15px;
  margin: 10px 0px;
  font-size: 18px;
  border-radius: 10px;
  background-color: cyan;
  color: black;
  cursor: pointer;
}
.todos ul li {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.todos ul li span {
  font-size: 30px;
}
.todos ul li button {
  outline: none;
  border: none;
  padding: 10px 15px;
  margin: 10px 0px;
  /* font-size: 18px; */
  border-radius: 10px;
  background-color: rgb(214, 16, 16);
  color: white;
  cursor: pointer;
}
li {
  list-style: none;
}

.delete__all {
  outline: none;
  border: none;
  padding: 10px 15px;
  margin: 10px 0px;
  /* font-size: 18px; */
  border-radius: 10px;
  background-color: rgb(214, 16, 16);
  color: white;
  cursor: pointer;
}
</style>