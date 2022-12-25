<!-- eslint-disable vue/multi-word-component-names -->
<script>
import TheButton from "./Button.vue";
export default {
  name: "TheHeader",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    TheButton,
  },
  computed: {
    showButton() {
      return this.$route.path === "/";
    },
  },
};
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <TheButton
      v-if="showButton"
      @click-button="$emit('show-add-task')"
      :title="showAddTask ? 'close' : 'add task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
