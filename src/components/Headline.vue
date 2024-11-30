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
    <h1 class="text-4xl text-center my-8">{{ msg }}</h1>
  </div>
</template>

<style></style>
