<template>
  <AddTask v-if="showAddTask" @add-task="addTask" />
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="onDelete"
    :tasks="tasks"
  />
</template>

<script>
import axios from "axios";
import swal from "sweetalert";
import AddTask from "../components/AddTask.vue";
import Tasks from "../components/Tasks.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Home",
  components: {
    AddTask,
    Tasks,
  },
  data() {
    return {
      tasks: [],
    };
  },
  props: {
    showAddTask: Boolean,
  },
  methods: {
    async addTask(task) {
      try {
        const { data } = await axios.post("/api/tasks", task);
        this.tasks = [...this.tasks, data];
      } catch (err) {
        swal("error", "something went wrong", "error");
      }
    },
    async onDelete(id) {
      try {
        await axios.delete(`/api/tasks/${id}`);
        this.tasks = this.tasks.filter((t) => t.id !== id);
      } catch (err) {
        swal("error", "something went wrong", "error");
      }
    },
    async getTask(id) {
      try {
        const { data } = await axios.get(`/api/tasks/${id}`);
        return data;
      } catch (err) {
        swal("error", "something went wrong", "error");
      }
    },
    async toggleReminder(id) {
      const task = await this.getTask(id);
      const newTask = { ...task, reminder: !task.reminder };
      try {
        await axios.put(`/api/tasks/${id}`, newTask);
        this.tasks = this.tasks.map((t) =>
          t.id === id ? { ...t, reminder: !t.reminder } : t
        );
      } catch (err) {
        swal("error", "something went wrong", "error");
      }
    },
  },
  async created() {
    try {
      const { data } = await axios.get("/api/tasks");
      this.tasks = data;
    } catch (err) {
      swal("error", "something went wrong", "error");
    }
  },
};
</script>
