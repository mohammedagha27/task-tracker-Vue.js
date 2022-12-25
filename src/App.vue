<script>
import TheHeader from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import axios from "axios";
import swal from "sweetalert";
export default {
  name: "App",
  components: { TheHeader, Tasks, AddTask },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    showAddTaskForm() {
      this.showAddTask = !this.showAddTask;
    },
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

<template>
  <div class="container">
    <TheHeader
      @show-add-task="showAddTaskForm"
      :showAddTask="showAddTask"
      title="Task Tracker"
    />
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="onDelete"
      :tasks="tasks"
    />
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins";
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
