<template>
  <div class="todo-container">
    <h2>Todo App</h2>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quia, autem?</p>
    <div class="input-container">
      <input type="text" placeholder="Enter todo" v-model="newTodo" @keyup.enter="addTodo"/>
      <button type="button" @click="addTodo">Add</button>
    </div>

    <div class="stats">
      <p>Total: {{ todos.length }}</p>
      <p>Completed: {{ computedCount }}</p>
      <p>Pending: {{ pendingCount }}</p>
    </div>

    <ul v-if="todos.length">
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.completed" />
        <span :class="{completed: todo.completed}">{{ todo.text }}</span>
        <button type="button" @click="deleteTodo(todo.id)">Delete</button>
      </li>
    </ul>
    <p v-else class="empty-message">No todos available</p>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");

const todos = ref([
  { id: 1, text: "Coding", completed: true },
  { id: 2, text: "Reading", completed: false },
]);

const addTodo = () => {
  const task = newTodo.value.trim();
  if (!task) return;

  todos.value.push({ id: Date.now(), text:task, completed: false });

  newTodo.value = "";
};

const deleteTodo = (id) => {
    todos.value = todos.value.filter((todo) => todo.id !== id)
}

const computedCount  = computed(() => {
    return todos.value.filter((todo) => todo.completed).length
})

const pendingCount = computed(() => {
    return todos.value.filter((todo) => !todo.completed).length
})

</script>

<style scoped>
.todo-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 25px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.input-container {
  display: flex;
  gap: 10px;
}

.input-container input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
}

.input-container button {
  padding: 10px 20px;
  cursor: pointer;
}

.stats {
  display: flex;
  justify-content: space-between;
  margin: 20px 0;
  font-weight: bold;
}

ul {
  list-style: none;
}

.todo-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
}

.todo-item span {
  flex: 1;
}

.completed {
  text-decoration: line-through;
  color: gray;
}

.delete-btn {
  background: crimson;
  color: white;
  border: none;
  padding: 6px 10px;
  cursor: pointer;
  border-radius: 4px;
}

.empty-message {
  text-align: center;
  margin-top: 20px;
  color: gray;
}
</style>
