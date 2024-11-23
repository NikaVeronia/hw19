<template>
    <li :class="{ completed: task.completed }">
      <!-- Нажатие на текст задачи вызывает событие toggle-task -->
      <span @click="$emit('toggle-task', task.id)">{{ task.text }}</span>
      <!-- Кнопка для удаления задачи -->
      <button @click="$emit('remove-task', task.id)">Удалить</button>
    </li>
  </template>
  
  <script>
  export default {
    props: {
      task: {
        type: Object,
        required: true,
      },
    },
    emits: ['remove-task', 'toggle-task'],
  };
  </script>
  
  <style scoped>
  /* Зачёркивание текста для выполненных задач */
  .completed span {
    text-decoration: line-through;
    color: gray;
  }
  button {
    border: none;
    background: #e74c3c;
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
  }
  button:hover {
    background: #c0392b;
  }
  </style>
  