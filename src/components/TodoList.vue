<template>
    <div>
      <!-- Форма для добавления задачи -->
      <form @submit.prevent="addTask" class="add-task-form">
        <input v-model="newTask" type="text" placeholder="Введите новую задачу" />
        <button type="submit">Добавить</button>
      </form>
  
      <!-- Список задач -->
      <ul class="task-list">
        <TodoItem
          v-for="task in tasks"
          :key="task.id"
          :task="task"
          @remove-task="removeTask"
          @toggle-task="toggleTask"
        />
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from "vue";
  import TodoItem from "./TodoItem.vue";
  
  export default {
    components: { TodoItem },
    setup() {
      const tasks = ref([]);
      const newTask = ref("");
      let nextId = 1;
  
      // Добавление новой задачи
      const addTask = () => {
        if (newTask.value.trim() !== "") {
          tasks.value.push({
            id: nextId++,
            text: newTask.value.trim(),
            completed: false, // Задача добавляется как невыполненная
          });
          newTask.value = "";
        }
      };
  
      // Удаление задачи
      const removeTask = (id) => {
        tasks.value = tasks.value.filter((task) => task.id !== id);
      };
  
      // Переключение состояния задачи (выполнена/не выполнена)
      const toggleTask = (id) => {
        const task = tasks.value.find((task) => task.id === id);
        if (task) {
          task.completed = !task.completed; // Инвертируем состояние completed
        }
      };
  
      return { tasks, newTask, addTask, removeTask, toggleTask };
    },
  };
  </script>
  
  <style scoped>
  .add-task-form {
    display: flex;
    margin-bottom: 20px;
  }
  .add-task-form input {
    padding: 10px;
    font-size: 16px;
    margin-right: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    flex-grow: 1;
  }
  .add-task-form button {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    background: #2ecc71;
    color: white;
    border-radius: 5px;
    cursor: pointer;
  }
  .add-task-form button:hover {
    background: #27ae60;
  }
  .task-list {
    list-style-type: none;
    padding: 0;
  }
  </style>
  