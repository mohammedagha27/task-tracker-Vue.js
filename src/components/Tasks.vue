<template>
  <div v-for="task in tasks" :key="task.id">
    <Task :task="task" />
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Tasks",
  components: {
    Task,
  },
  props: {
    tasks: Array,
  },
};
</script>

<style></style>
