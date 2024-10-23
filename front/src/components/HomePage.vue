<template>
  <div class="home">
    <h1>Task Manager</h1>
    <TaskFilter @filter-change="filterTasks"/>
    <TaskList
      :tasks="filteredTasks"
      @add-task="addTask"
      @toggle-task="toggleTask"
      @delete-task="deleteTask"
      />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import TaskList from './TaskList.vue';
import TaskFilter from './TaskFilter.vue';

const tasks = ref([]);
const filter = ref('all');

const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'completed':
      return tasks.value.filter(task => task.completed);
    case 'non-completed':
      return tasks.value.filter(task => !task.completed);
    default:
      return tasks.value;
  }
});

const addTask = (name) => {
  const newTask = {
    id: Date.now(),
    name,
    completed: false
  };
  tasks.value.push(newTask);
}

const toggleTask = (task) => {
  const index = tasks.value.findIndex(t => t.id === task.id);
  if (index !== -1) {
    tasks.value[index].completed = !tasks.value[index].completed;
  }
}

const deleteTask = (task) => {
  tasks.value = tasks.value.filter(t => t.id !== task.id);
}

const filterTasks = (newFilter) => {
  filter.value = newFilter;
};
</script>