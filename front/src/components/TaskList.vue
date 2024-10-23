<template>
  <div class="task-list">
    <h2>Task List</h2>
    <form @submit.prevent="addTask">
      <input v-model="newTaskName" placeholder="Enter new task" required/>
      <button type="submit">Add Task</button>
    </form>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{  task.name }}
        <input type="checkbox" :checked="task.completed" @change="toggleTask(task)"/>
        <button @click="deleteTask(task)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, toRefs, defineProps, defineEmits } from 'vue';

const props = defineProps({
  tasks: {
    type: Array,
    required: true
  }
});

const { tasks } = toRefs(props);

const emit = defineEmits(['add-task', 'toggle-task', 'delete-task']);

const newTaskName = ref('');

const addTask = () => {
  emit('add-task', newTaskName.value);
  newTaskName.value = "";
};

const toggleTask = (task) => {
  emit('toggle-task', task);
};

const deleteTask = (task) => {
  emit('delete-task', task);
};
</script>