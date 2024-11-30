<script lang="ts">
export default {
  name: 'Headline',
  props: {
    msg: {
      type: String,
      required: true,
    },
  },
};
</script>

<template>
  <div>
    <div class="text-4xl text-center my-4">{{ msg }}</div>
  </div>
</template>

<style></style>
