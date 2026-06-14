<template>
  <div class="main">
    <div class="header">
      <span
        >Total Todos: <b>{{ todos.length }}</b></span
      >
      <span
        >Completed Todos: <b>{{ completedTodos }}</b></span
      >
      <span
        >Pending Todos: <b>{{ pendingTodos }}</b></span
      >
    </div>
    <div class="todo-input">
      <input
        type="text"
        placeholder="Enter todo"
        v-model="newTodo"
        @keyup.enter="addTodo"
      />
      <button type="button" @click="addTodo">Add</button>
    </div>
    <div class="todos" v-if="todos.length">
      <p v-for="todo in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{ completed: todo.completed }">{{ todo.task }}</span
        >&nbsp;
        <button type="button" @click="deleteTodo(todo.id)">Delete</button>
      </p>
    </div>
    <p v-else>No todo available</p>
  </div>
</template>

<script setup>
import { ref, computed, watch } from "vue";

const newTodo = ref("");

const todos = ref(
    JSON.parse(localStorage.getItem("todos")) || []
)

const addTodo = () => {
  let inputTodo = newTodo.value.trim();
  if (!inputTodo) return;

  todos.value.push({ id: Date.now(), task: inputTodo, completed: false });
  newTodo.value = "";
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

const completedTodos = computed(() => {
  return todos.value.filter((todo) => todo.completed).length;
});

const pendingTodos = computed(() => {
  return todos.value.filter((todo) => !todo.completed).length;
});

watch(
    todos,
    (newTodos) => {
        localStorage.setItem("todos", JSON.stringify(newTodos))
    },
    {deep: true}
)

</script>
