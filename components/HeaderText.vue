<template>
  <div class="customContainer">
    <div class="customContainer__content">
      <h1 class="customContainer__h1">{{ title }}</h1>
      <p>{{ body }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeaderText',
  props: {
    title: {
      type: String,
      required: true,
    },
    body: {
      type: String,
      required: true,
    },
  },
}
</script>

<style lang="scss"></style>
