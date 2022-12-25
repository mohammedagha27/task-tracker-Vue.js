<template>
  <h3 v-bind="$attrs">
    this is my first vue project ever! <br />to be honest i loved it more than
    react 🥳
  </h3>
  <h3 style="text-align: center; margin-top: 1rem">
    <router-link to="/">Go back</router-link>
  </h3>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "About",
};
</script>
