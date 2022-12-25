<!-- eslint-disable vue/multi-word-component-names -->
<script>
import TheButton from "./Button.vue";
export default {
  name: "TheHeader",
  props: {
    title: String,
  },
  components: {
    TheButton,
  },
};
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <TheButton title="add task" color="green" />
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
