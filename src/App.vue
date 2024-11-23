<template>
  <div id="app" class="todo-container">
    <h1>ToDo List</h1>
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: { TodoList },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 20px;
  padding: 0;
}
.todo-container {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}
</style>
