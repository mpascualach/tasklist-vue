<template>
  <div class="task-filter">
    <h3>Filter Tasks</h3>
    <select v-model="selectedFilter" @change="emitFilter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits(['filter-change']);

const selectedFilter = ref('all');

const emitFilter = () => {
  emit('filter-change', selectedFilter.value);
};
</script>