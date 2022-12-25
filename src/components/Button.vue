<template>
  <button class="btn" @click="onClick()" :style="{ background: color }">
    {{ title }}
  </button>
</template>

<script>
export default {
  name: "TheButton",
  props: {
    title: String,
    color: String,
  },
  methods: {
    onClick() {
      this.$emit("click-button");
    },
  },
};
</script>

<style></style>
